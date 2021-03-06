---
title: "Linux 가상 컴퓨터에 태그를 지정하는 방법 | Microsoft Docs"
description: "리소스 관리자 배포 모델을 사용하여 만든 Linux 가상 컴퓨터에 태그를 지정하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: 6e39b13de1808ebb1d0571ab0c1c620261046d0d


---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a>Azure에서 Linux 가상 컴퓨터에 태그를 지정하는 방법
이 문서에서는 리소스 관리자 배포 모델을 통해 Azure의 Linux 가상 컴퓨터에 태그를 지정하는 다양한 방법에 대해 설명합니다. 태그는 리소스 또는 리소스 그룹에 직접 배치할 수 있는 사용자 정의 키/값 쌍입니다. Azure는 현재 리소스 및 리소스 그룹당 최대 15개의 태그를 지원합니다. 태그를 만들 때 리소스에 배치하거나 기존 리소스에 추가할 수 있습니다. 태그는 리소스 관리자 배포 모델을 통해 만든 리소스에 대해서만 지원됩니다.

[!INCLUDE [virtual-machines-common-tag](../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Azure CLI를 사용하여 태그 지정
시작하려면 [Azure CLI를 설치 및 구성](../xplat-cli-azure-resource-manager.md)하고 Resource Manager 모드(`azure config mode arm`)에 있는지 확인합니다.

다음 명령을 사용하여 태그를 비롯한 지정된 가상 컴퓨터의 모든 속성을 볼 수 있습니다.

        azure vm show -g MyResourceGroup -n MyTestVM

Azure CLI를 통해 새 VM 태그를 추가하려면 태그 매개 변수 **-t**와 함께 `azure vm set` 명령을 사용할 수 있습니다.

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

`azure vm set` 명령에 **–T** 매개 변수를 사용하여 모든 태그를 제거할 수 있습니다.

        azure vm set – g MyResourceGroup –n MyTestVM -T


Azure CLI 및 포털을 통해 리소스에 태그를 적용했으므로 이제 사용량 세부 정보를 확인하여 청구 포털에서 태그를 살펴보겠습니다.

[!INCLUDE [virtual-machines-common-tag-usage](../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>다음 단계
* Azure 리소스에 태그를 지정하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요][Azure Resource Manager 개요] 및 [태그를 사용하여 Azure 리소스 구성][태그를 사용하여 Azure 리소스 구성]을 참조하세요.
* 태그로 Azure 리소스의 사용을 관리하는 방법은 [Azure 청구서 이해][Azure 청구서 이해] 및 [Microsoft Azure 리소스 소비에 대한 정보 얻기][Microsoft Azure 리소스 소비에 대한 통찰력 얻기]를 참조하세요.

[Azure CLI 환경]: ./xplat-cli-azure-resource-manager.md
[Azure Resource Manager 개요]: ../azure-resource-manager/resource-group-overview.md
[태그를 사용하여 Azure 리소스 구성]: ../resource-group-using-tags.md
[Azure 청구서 이해]: ../billing/billing-understand-your-bill.md
[Microsoft Azure 리소스 소비에 대한 통찰력 얻기]: ../billing-usage-rate-card-overview.md



<!--HONumber=Nov16_HO3-->


