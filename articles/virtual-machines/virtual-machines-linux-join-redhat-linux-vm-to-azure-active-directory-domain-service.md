---
title: "Azure Active Directory DS에 RedHat Linux VM 조인 | Microsoft Docs"
description: "Azure Active Directory Domain Service에 기존 RedHat Enterprise Linux 7 VM을 조인하는 방법입니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: v-livech
translationtype: Human Translation
ms.sourcegitcommit: 4e764e0d115c787f78593116f29c89e7c1e0e527
ms.openlocfilehash: 0c596b630c44ff68a01c7dbd3173c192fafac125


---

# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a>Azure Active Directory Domain Service에 RedHat Linux VM 조인

이 문서에서는 Red Hat Enterprise Linux(RHEL) 7 가상 컴퓨터를 AADDS(Azure Active Directory Domain Services) 관리되는 도메인에 조인하는 방법을 보여 줍니다.  요구 사항은 다음과 같습니다.

- [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)

- [SSH 공용 및 개인 키 파일](virtual-machines-linux-mac-create-ssh-keys.md)

- [Azure Active Directory Domain Services DC](../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>빠른 명령

모든 예제를 고유한 설정으로 바꿉니다.

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a>azure-cli를 클래식 배포 모드로 전환

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>RHEL 버전 및 이미지 검색

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Redhat Linux VM 만들기

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p P@ssw0rd! \
-z "Small" \
-e \
-l "West US"
```

### <a name="ssh-to-the-vm"></a>VM에 SSH

```bash
ssh -i ~/.ssh/id_rsa ahmet@
```

### <a name="update-yum-packages"></a>YUM 패키지 업데이트

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>필요한 패키지 설치

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

이제 필요한 패키지를 Linux 가상 컴퓨터에 설치했고 다음 작업은 가상 컴퓨터를 관리되는 도메인에 가입하는 것입니다.

### <a name="discover-the-aad-domain-services-managed-domain"></a>AAD Domain Services 관리되는 도메인 검색

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>kerberos 초기화

'AAD DC 관리자' 그룹에 속한 사용자를 지정해야 합니다. 이러한 사용자만 관리되는 도메인에 컴퓨터를 가입할 수 있습니다.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a>도메인에 컴퓨터 조인

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a>도메인에 컴퓨터가 조인되었는지 확인

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>다음 단계

* [Azure에서 주문형 Red Hat Enterprise Linux VM에 대한 RHUI(Red Hat Update Infrastructure)](virtual-machines-linux-update-infrastructure-redhat?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Resource Manager에서 가상 컴퓨터에 대한 Key Vault 설정](virtual-machines-linux-key-vault-setup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Resource Manager 템플릿 및 Azure CLI를 사용하여 가상 컴퓨터 배포 및 관리](virtual-machines-linux-cli-deploy-templates?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)



<!--HONumber=Nov16_HO5-->


