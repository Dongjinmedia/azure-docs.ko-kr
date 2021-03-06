---
title: "Resource Manager 및 PowerShell을 사용하여 ExpressRoute용 가상 네트워크에 VNet 게이트웨이 추가 | Microsoft 문서"
description: "이 문서에서는 Express 경로에 대해 이미 만들어진 Resource Manager VNet에 Vnet 게이트웨이를 추가하는 과정을 안내합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: charwen
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 61817e1bd5b4af9aa9e3fda2043acc1036b7268a


---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-resource-manager-and-powershell"></a>리소스 관리자 및 PowerShell을 사용하여 Express 경로에 대한 가상 네트워크 게이트웨이 구성
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-add-gateway-resource-manager.md)
> * [PowerShell - 클래식](expressroute-howto-add-gateway-classic.md)
> 
> 

이 문서에서는 기존 VNet에 대한 가상 네트워크(VNet) 게이트웨이를 추가하고, 크기를 조정하고, 제거하는 단계를 안내합니다. 이 구성 단계는 특히 **Resource Manager 배포 모델** 을 사용하여 만들었으며 Express 경로 구성에서 사용할 VNet을 위한 단계입니다. 

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>시작하기 전에
이 구성에 필요한 Azure PowerShell cmdlet을 설치했는지 확인합니다(1.0.2 이상). Cmdlet을 설치하지 않은 경우 구성 단계를 시작하기 전에 설치해야 합니다. Azure PowerShell 설치에 관한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](../powershell-install-configure.md)을 참조하세요.

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>다음 단계
VNet 게이트웨이를 만든 후 VNet을 Express 경로 회로에 연결할 수 있습니다. [가상 네트워크를 Express 경로 회로에 연결](expressroute-howto-linkvnet-arm.md)을 참조하세요.




<!--HONumber=Nov16_HO3-->


