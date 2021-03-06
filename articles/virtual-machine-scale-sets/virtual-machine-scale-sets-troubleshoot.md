---
title: "가상 컴퓨터 크기 집합을 이용하여 자동 크기 조정 문제 해결 | Microsoft Docs"
description: "가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결 일반적으로 발생하는 문제와 해결 방법에 대해 이해합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
translationtype: Human Translation
ms.sourcegitcommit: 5919c477502767a32c535ace4ae4e9dffae4f44b
ms.openlocfilehash: 7d122d04dfd9cb1f565e86b60f2180f9534588c9


---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결
**문제** – VM Scale Sets을 사용하여 Azure Resource Manager에 자동 크기 조정 인프라를 만들었습니다. 예를 들어 https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale과 같은 템플릿을 배포했습니다. 크기 조정 규칙을 정의했으며 VM에 적용되는 부하의 양에 관계없이 크기가 자동으로 조정되지 않는 점을 제외하고 원활하게 작동합니다.

## <a name="troubleshooting-steps"></a>문제 해결 단계
다음은 몇 가지 고려해야 할 사항입니다.

* 각 VM에 얼마나 많은 코어가 있고 각 코어를 로드하고 있나요?
  위의 Azure 빠른 시작 템플릿 예제에는 단일 코어를 로드하는 do_work.php 스크립트가 있습니다. Standard_A1 또는 D1과 같은 단일 코어 VM 크기보다 큰 VM을 사용하는 경우 이 부하를 여러 번 실행해야 합니다.  [Azure에서 Windows 가상 컴퓨터 크기](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* VM 규모 집합에 얼마나 많은 VM이 있고 각각에서 작업을 수행하고 있나요?
  
    크기 조정 이벤트는 자동 크기 조정 규칙에서 내부 정의된 시간 동안 규모 집합에 있는 **모든** VM에 대해서 평균 CPU가 임계값을 초과했을 경우에만 수행됩니다.
* 누락된 크기 조정 이벤트가 있나요?
  
    Azure 포털에서 크기 조정 이벤트에 대한 감사 로그를 확인합니다. 누락된 규모 확장 및 축소가 있을 수 있습니다. "크기 조정"으로 필터링할 수 있습니다.
  
    ![감사 로그][audit]
* 규모 축소 및 확장 임계값 차이가 충분한가요?
  
    평균 CPU가 5분 이상 50%보다 클 때 규모를 확장하고 50%보다 작을 때 규모를 축소하도록 설정했다고 가정합니다. 이 경우 CPU 사용량이 임계값에 가까워질 때 크기 조정 작업이 지속적으로 집합의 크기를 늘리고 줄이기를 반복하면서 “플래핑” 문제가 발생됩니다. 이 때문에 자동 크기 조정 서비스는 크기를 조정하지 않는 것으로 나타날 수 있는 “플래핑”을 방지하려고 합니다. 그러므로 크기 조정 사이에 일부 간격을 허용하도록 규모 확장 및 축소 임계값의 차이가 충분한지 확인합니다.
* 사용자 고유의 JSON 템플릿을 작성했나요?
  
    실수하기 쉬우므로 작업에 증명된 위와 같은 템플릿으로 시작하고 조금씩 증분합니다. 
* 수동으로 규모를 축소 또는 확장할 수 있나요?
  
    VM 수를 수동으로 변경하려면 다른 "용량" 설정을 사용하여 VM 규모 집합 리소스를 다시 배포합니다. https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing 예제 템플릿에서 이를 수행합니다. 크기 집합에서 사용하는 크기와 동일한 컴퓨터 크기를 사용하도록 템플릿을 편집해야 할 수 있습니다. 성공적으로 VM 수를 수동으로 변경할 수 있으면 자동 크기 조정에 문제의 원인이 있는 것입니다.
* Microsoft.Compute/virtualMachineScaleSet 및 [Azure 리소스 탐색기](https://resources.azure.com/)
  
    이는 Azure Resource Manager 리소스의 상태를 보여 주는 필수적인 문제 해결 도구입니다. 구독을 클릭하고 문제를 해결하려는 리소스 그룹을 살펴봅니다. 계산 리소스 공급자 아래에서, 만든 VM 규모 집합을 살펴보고 배포 상태를 보여 주는 인스턴스 보기를 확인합니다. 또한 VM 규모 집합에서 VM 인스턴스 보기를 확인합니다. 그런 다음 Microsoft.Insights 리소스 공급자로 이동하여 자동 크기 조정 규칙이 올바른지 확인합니다.
* 진단 확장이 작동 중이고 성능 데이터를 내보내고 있나요?
  
    **업데이트:** 더 이상 진단 확장을 설치하지 않아도 되는 호스트 기반 메트릭 파이프라인을 사용하도록 Azure 자동 크기 조정 기능이 향상되었습니다. 즉, 새 파이프라인을 사용하여 자동 크기 조정 응용 프로그램을 만들 경우 다음 단락의 내용은 더 이상 적용되지 않습니다. 호스트 파이프라인을 사용하도록 변환된 Azure 템플릿의 예는 https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale, https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-lapstack-autoscale을 포함합니다. 
  
    자동 크기 조정을 위한 호스트 기반 메트릭을 사용하는 것이 좋은 이유는 다음과 같습니다.
  
  * 진단 확장을 설치하지 않아도 되기 때문에 이동하는 부분이 더 적습니다.
  * 템플릿이 간단합니다. 기존 크기 집합 템플릿에 insights 자동 크기 조정 규칙만 추가됩니다.
  * 새 VM에 대한 더 신뢰할 수 있는 보고 및 빠른 시작이 가능합니다.
    
    진단 확장을 계속 사용하려는 유일한 이유는 메모리 진단 보고/크기 조정이 필요한 경우입니다. 호스트 기반 메트릭은 메모리를 보고하지 않습니다.
    
    이 점을 고려하여 자동 크기 조정을 위한 진단 확장을 여전히 사용하는 경우 이 문서의 나머지 부분만을 수행합니다.
    
    Azure Resource Manager에서 자동 크기 조정은 진단 확장이라는 VM 확장을 통해 작동할 수 있지만 필수는 아닙니다. 이 방법은 템플릿에서 정의한 저장소 계정으로 성능 데이터를 내보냅니다. 그런 다음 Azure Monitor 서비스에 의해 이 데이터가 집계됩니다.
    
    Insights 서비스가 VM에서 데이터를 읽을 수 없는 경우 사용자에게 메일을 보낸다고 가정합니다. 예를 들어 VM이 다운된 경우 Azure 계정을 만들 때 지정한 메일을 확인합니다.
    
    직접 이동하여 데이터를 살펴볼 수도 있습니다. 클라우드 탐색기를 사용하여 Azure 저장소 계정을 찾습니다. 예를 들어 [Visual Studio 클라우드 탐색기](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2)를 사용하여 로그인하고 사용 중인 Azure 구독과 배포 템플릿의 진단 확장 정의에서 참조된 진단 저장소 계정을 선택합니다.
    
    ![Cloud Explorer][explorer]
    
    각 VM의 데이터가 저장되는 여러 테이블이 표시됩니다. 예를 들어 Linux 및 CPU 메트릭에서 가장 최근 행을 살펴봅니다. Visual Studio 클라우드 탐색기는 쿼리 언어를 지원하므로 “Timestamp gt datetime’2016-02-02T21:20:00Z’”와 같은 쿼리를 실행하여 가장 최근의 이벤트를 가져옵니다(가정 시간은 UTC 기준). 확인한 데이터가 설정한 크기 조정 규칙과 일치하나요? 아래 예제에서는 컴퓨터 20에 대한 CPU가 지난 5분 동안 100%로 증가하기 시작했습니다.
    
    ![저장소 테이블][tables]
    
    데이터가 없는 경우 VM에서 실행 중인 진단 확장에 문제가 있음을 의미합니다. 데이터가 있는 경우에는 크기 조정 규칙 또는 Insights 서비스에 문제가 있음을 의미합니다. [Azure 상태](https://azure.microsoft.com/status/)를 확인합니다.
    
    이러한 단계를 수행한 후 여전히 자동 크기 조정 문제가 발생하는 경우 [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp)의 포럼 또는 [스택 오버플로](http://stackoverflow.com/questions/tagged/azure)를 확인하거나 지원을 요청할 수 있습니다. 템플릿 및 성능 데이터 보기를 공유하도록 준비합니다.

[감사]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[탐색기]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[테이블]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png



<!--HONumber=Nov16_HO3-->


