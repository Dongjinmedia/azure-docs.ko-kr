---
title: Site Recovery를 사용하여 Amazon Web Services의 Windows 가상 컴퓨터를 Azure로 마이그레이션 | Microsoft Docs
description: 이 문서에서는 Azure Site Recovery를 사용하여 Amazon 웹 서비스(AWA)를 실행하는 Windows 가상 컴퓨터를 Azure로 마이그레이션하는 방법을 설명합니다.
services: site-recovery
documentationcenter: ''
author: rayne-wiselman
manager: jwhit
editor: ''

ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 08/22/2016
ms.author: raynew

---
# Azure Site Recovery를 사용하여 AWS(Amazon Web Services)의 Windows 가상 컴퓨터를 Azure로 마이그레이션
## 개요
Azure Site Recovery에 오신 것을 환영합니다. 이 문서에서는 Site Recovery를 사용하여 AWS에서 실행 중인 Windows 인스턴스를 Azure로 마이그레이션합니다. 시작하기 전에 다음 사항에 주의하세요.

* Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 Azure Resource Manager 배포 모델과 클래식 배포 모델이 있습니다. 또한 Azure에는 두 가지 포털이 있는데, 하나는 클래식 배포 모델을 지원하는 Azure 클래식 포털이고 다른 하나는 두 가지 배포 모델을 모두 지원하는 Azure 포털입니다. Resource Manager 또는 클래식 중 어느 곳에서 Site Recovery를 구성하든 마이그레이션의 기본 단계는 동일합니다. 그러나 이 문서의 UI 지침과 스크린샷은 Azure 포털과 관련된 것입니다.
* **현재 AWS에서 Azure로만 마이그레이션할 수 있습니다. AWS에서 Azure로 장애 조치(failover)할 수 있으나 다시 장애 복구(failback)할 수 없습니다. 진행 중인 복제가 없습니다.**
* 이 문서의 마이그레이션 지침은 물리적 컴퓨터를 Azure에 복제하기 위한 지침을 기준으로 합니다. 여기에는 Azure 포털의 물리적 서버 복제 방법을 설명하는 [VMware VM 또는 물리적 서버를 Azure로 복제](site-recovery-vmware-to-azure.md)에 나오는 단계에 대한 링크가 포함됩니다.
* 클래식 포털에서 Site Recovery를 설정하는 경우 [이 문서](site-recovery-vmware-to-azure-classic.md)의 자세한 지침을 따르세요. 이 [레거시 문서](site-recovery-vmware-to-azure-classic-legacy.md)의 지침은 **더 이상 사용하지 마세요**.

이 문서의 하단 또는 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.

## 필수 조건
이 배포에 대해 필요한 사항은 다음과 같습니다.

* **구성 서버**: 구성 서버 역할을 하는 Windows Server 2012 R2를 실행 중인 온-프레미스 VM입니다. 이 VM에 다른 Site Recovery 구성 요소(프로세스 서버 및 마스터 대상 서버 포함)도 설치합니다. 자세한 내용은 [시나리오 아키텍처](site-recovery-vmware-to-azure.md#scenario-architecture) 및 [구성 서버 필수 구성 요소](site-recovery-vmware-to-azure.md#configuration-server-prerequisites)를 참조하세요.
* **EC2 VM 인스턴스**: 마이그레이션하려는 Windows를 실행하는 인스턴스입니다.

## 배포 단계
이 섹션에서는 새 Azure 포털의 배포 단계를 설명합니다. 클래식 포털에서 Site Recovery에 대해 이러한 배포 단계가 필요한 경우 [이 문서](site-recovery-vmware-to-azure-classic.md)를 참조하세요.

1. [자격 증명 모음을 만듭니다](site-recovery-vmware-to-azure.md#create-a-recovery-services-vault).
2. [구성 서버를 배포합니다](site-recovery-vmware-to-azure.md#step-2-set-up-the-source-environment).
3. 배포한 후에 구성 서버가 마이그레이션할 VM과 통신할 수 있는지 유효성을 검사합니다.
4. [복제 설정을 지정합니다](site-recovery-vmware-to-azure.md#step-4-set-up-replication-settings). 복제 정책을 만들고 구성 서버에 할당합니다.
5. [모바일 서비스를 설치합니다](site-recovery-vmware-to-azure.md#step-6-replication-application). 보호하려는 각 VM은 모바일 서비스가 설치되어야 합니다. 이 서비스는 프로세스 서버에 데이터를 보냅니다. 모바일 서비스를 수동으로 설치 또는 푸시하고 VM에 대한 보호를 사용하는 경우 프로세스 서버에서 자동으로 설치합니다. EC2 인스턴스에서 마이그레이션할 방화벽 규칙을 구성하여 이 서비스의 강제 설치를 허용해야 합니다. EC2 인스턴스에 대한 보안 그룹에는 다음과 같은 규칙이 있어야 합니다.
   
    ![방화벽 규칙](./media/site-recovery-migrate-aws-to-azure/migrate-firewall.png)
6. [복제를 활성화합니다](site-recovery-vmware-to-azure.md#enable-replication). 마이그레이션할 VM에 대해 복제를 사용하도록 설정합니다. EC2 콘솔에서 얻을 수 있는 개인 IP 주소를 사용하여 EC2 인스턴스를 검색할 수 있습니다.
7. [계획되지 않은 장애 조치를 실행합니다](site-recovery-failover.md#run-an-unplanned-failover). 초기 복제가 완료된 후 각 VM에 대해 AWS에서 Azure로 계획되지 않은 장애 조치를 실행할 수 있습니다. 선택적으로 복구 계획을 만들고 장애 조치를 실행하여 AWS에서 Azure에 여러 가상 컴퓨터를 마이그레이션할 수 있습니다. 복구 계획을 [자세히 알아봅니다](site-recovery-create-recovery-plans.md).

## 다음 단계
[Azure Site Recovery란?](site-recovery-overview.md)의 다른 복제 시나리오에 대해 알아봅니다.

<!---HONumber=AcomDC_0824_2016-->