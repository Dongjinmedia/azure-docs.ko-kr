---
title: "국가별 Azure CDN 콘텐츠에 대한 액세스 제한 | Microsoft Docs"
description: "[지역 필터링] 기능을 사용하여 Azure CDN 콘텐츠에 대한 액세스를 제한하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: rli
translationtype: Human Translation
ms.sourcegitcommit: 2ee72c31072fb5201e057f4c3567d33ce53e4fbc
ms.openlocfilehash: 1dfd5833d8637232b7998b7fdc7f39679645e1f7


---
# <a name="restrict-access-to-your-content-by-country---akamai"></a>국가별로 콘텐츠에 대한 액세스 제한 - Akamai
> [!div class="op_single_selector"]
> * [Verizon](cdn-restrict-access-by-country.md)
> * [Akamai Standard](cdn-restrict-access-by-country-akamai.md)
> 
> 

## <a name="overview"></a>개요
기본적으로 사용자가 콘텐츠를 요청하는 경우 사용자가 이 요청을 수행하는 위치에 관계 없이 콘텐츠 페이지가 제공됩니다. 경우에 따라 국가별로 콘텐츠에 액세스를 제한 할 수 있습니다. 이 항목에서는 국가별로 액세스를 허용하거나 차단하도록 서비스를 구성하기 위해 **지역 필터링** 기능을 사용하는 방법을 설명합니다.

> [!IMPORTANT]
> Verizon 및 Akamai 제품은 동일한 지역 필터링 기능을 제공하지만 사용자 인터페이스가 다릅니다. 이 문서는 **Akamai의 Azure CDN Standard**에 대한 인터페이스를 설명합니다. **Verizon의 Azure CDN Standard/Premium**에서 지역 필터링 사용은 [국가별로 콘텐츠에 대한 액세스 제한 - Verizon](cdn-restrict-access-by-country.md)을 참조하세요.
> 
> 

이 유형의 제한 구성에 적용되는 고려 사항에 대한 자세한 내용은 항목의 끝에 있는 [고려 사항](cdn-restrict-access-by-country.md#considerations) 섹션을 참조하세요.  

![국가 필터링](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a>1 단계: 디렉터리 경로 정의
포털 안에서 끝점을 선택하고 왼쪽 탐색에서 지역 필터링 탭을 찾아 이 기능을 확인합니다.

국가 필터를 구성하는 경우 사용자에게 액세스를 허용하거나 거부하는 위치에 대한 상대 경로를 지정해야 합니다. 디렉터리 경로 "/pictures/"를 지정하여 "/" 또는 선택된 폴더를 사용하여 모든 파일에 대해 지역 필터링을 적용할 수 있습니다. 마지막 슬래시를 생략하고 파일을 지정하여 "/pictures/city.png"로 단일 파일에 지역 필터링을 적용할 수도 있습니다.

예제 디렉터리 경로 필터:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a>2 단계: 차단 또는 허용 동작을 정의
**차단** : 지정한 국가의 사용자는 해당 재귀 경로에서 요청된 자산에 대해 액세스가 거부됩니다. 해당 위치에 대해 다른 국가 필터링 옵션이 구성되지 않은 경우에는 다른 모든 사용자는 액세스가 허용 됩니다

**허용** : 지정한 국가의 사용자만 해당 재귀 경로에서 요청된 자산에 대해 액세스가 허용됩니다.

## <a name="step-3-define-the-countries"></a>3 단계: 국가 정의하기
경로에 대해 차단 또는 허용하기 원하는 국가를 선택합니다. 자세한 내용은 [Akamai 국가 코드의 Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx)을 참조하세요.

예를 들어 /Photos/Strasbourg/ 차단 규칙은 다음을 포함하는 파일을 필터링합니다.

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


## <a name="country-codes"></a>국가 코드
**지역 필터링** 기능은 국가 코드를 사용하여 보안된 디렉터리에 대해 요청이 허용 또는 차단될 국가를 정의합니다. [Akamai 국가 코드의 Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx)에서 국가 코드를 찾을 수 있습니다. 

## <a name="a-idconsiderationsaconsiderations"></a><a id="considerations"></a>고려 사항
* 지리 필터링 구성에 대한 변경이 적용되려면 몇 분 정도 걸릴 수 있습니다.
* 이 기능은 와일드카드 문자를 지원하지 않습니다 (예: '*').
* 상대 경로와 관련된 지역 필터링 구성은 해당 경로에 재귀적으로 적용됩니다.
* 동일한 상대 경로에 하나의 규칙만 적용할 수 있습니다. (동일한 상대 경로를 가리키는 여러 국가 필터를 만들 수 없습니다  그러나 폴더에는 여러 국가 필터가 있을 수 있습니다. 이는 국가 필터의 재귀적 특성 때문입니다. 즉, 이전에 구성된 폴더의 하위 폴더에 다른 국가 필터를 할당할 수 있습니다.




<!--HONumber=Nov16_HO3-->


