---
title: "Service Fabric 클러스터 리소스 관리자: 이동 비용 | Microsoft Docs"
description: "Service Fabric 서비스의 이동 비용 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/19/2016
ms.author: masnider
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: 54cdfee64360543e0d1011f04c9b79400e912582


---
# <a name="service-movement-cost-for-influencing-cluster-resource-manager-choices"></a>클러스터 리소스 관리자 선택에 영향을 주는 서비스 이동 비용
클러스터를 변경하려고 할 때 고려해야 할 중요 요소와 솔루션의 점수가 해당 솔루션의 전체 비용입니다.

서비스 인스턴스 또는 복제본을 이동할 때는 최소한 CPU 시간 및 네트워크 대역폭이 필요합니다. 상태 저장 서비스의 경우에는 오래된 복제본을 종료하기 전에 상태 복사본을 만드는 데 필요한 디스크 공간의 양도 비용으로 포함됩니다. 어떤 경우이든 Azure Service Fabric 클러스터 리소스 관리자에서 제공하는 솔루션의 비용을 최소화하는 것이 목표입니다. 그와 동시에 클러스터에서 리소스 할당 효율성을 크게 개선하는 솔루션도 빠짐없이 고려해야 합니다.

클러스터 리소스 관리자는 다른 목표에 따라 클러스터를 관리하려는 경우에도 비용을 계산하고 제한하는 두 가지 방법을 제공합니다. 첫 번째 방법에서는 클러스터 리소스 관리자가 클러스터에 대한 새 레이아웃을 계획할 때 모든 이동 횟수를 계산합니다. 간단한 예로 전체 최종 균형(점수)이 거의 같은 두 개의 솔루션이 있는 경우 비용(총 이동 수)이 더 낮은 솔루션을 선택하는 경우가 있습니다.

이 방식은 매우 효율적으로 작동합니다. 하지만 복잡한 시스템에서도 기본 또는 정적 부하와 마찬가지로 모든 이동이 동일할 가능성은 거의 없습니다. 즉, 비용이 훨씬 높은 이동도 있습니다.

## <a name="changing-a-replicas-move-cost-and-factors-to-consider"></a>복제본의 이동 비용 및 고려해야 할 요소 변경
클러스터 리소스 관리자의 또 다른 기능인 부하 보고를 사용할 때와 마찬가지로, 특정 시간에 서비스를 이동하는 비용을 서비스가 자체적으로 보고하는 방법을 제공할 수 있습니다.

코드:

```csharp
this.ServicePartition.ReportMoveCost(MoveCost.Medium);
```

MoveCost에는 0, 낮음, 중간, 높음의 4개 수준이 있습니다. 이러한 수준은 0을 제외하고는 서로 상대적입니다. 0 수준에서는 복제본 이동이 무료이며 솔루션 점수 계산에 포함되지 않습니다. 이동 비용이 많이 들도록 설정해도 복제본이 절대 이동되지 않는다는 것이 *아니라* 합당한 이유가 있는 경우에만 이동한다는 의미입니다.

![이동할 복제본 선택 시의 요인으로 사용되는 이동 비용][Image1]

MoveCost를 사용하면 전체적으로 중단을 최소화며 가장 쉽게 적용할 수 있는 동시에 동등한 균형을 제공하는 솔루션을 찾을 수 있습니다. 서비스의 비용 개념은 다양한 요인을 기준으로 할 수 있습니다. 이동 비용 계산에서 가장 일반적으로 사용되는 요인은 다음과 같습니다.

* 서비스에서 이동해야 하는 상태 또는 데이터의 양
* 클라이언트 연결 끊기 비용 주 복제본 이동 비용이 대개 보조 복제본 이동 비용보다 높습니다.
* 처리 중인 작업을 중단하는 비용 데이터 저장소 수준의 일부 작업 또는 클라이언트 호출에 대한 응답으로 수행되는 작업의 경우 비용이 많이 소요됩니다. 이러한 작업은 특정 시점이 지나면 필요한 경우를 제외하고는 중지되지 않아야 합니다. 따라서 작업 기간에 비용을 늘려 서비스 복제본 또는 인스턴스가 이동할 가능성을 줄여야 합니다. 작업이 완료되면 비용을 다시 정상 수준으로 설정합니다.

## <a name="next-steps"></a>다음 단계
* Service Fabric 클러스터 리소스 관리자는 메트릭을 사용하여 클러스터의 리소스 사용량 및 용량을 관리합니다. 메트릭 및 메트릭 구성 방법에 대한 자세한 내용은 [Service Fabric에서 메트릭을 사용하여 리소스 사용량 및 부하 관리](service-fabric-cluster-resource-manager-metrics.md)를 참조하세요.
* 클러스터 리소스 관리자가 클러스터의 부하를 관리하고 분산하는 방법을 알아보려면 [Service Fabric 클러스터 부하 분산](service-fabric-cluster-resource-manager-balancing.md)을 참조하세요.

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png



<!--HONumber=Nov16_HO3-->


