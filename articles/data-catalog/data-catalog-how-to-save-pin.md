---
title: "검색을 저장하고 데이터 자산을 고정하는 방법 | Microsoft Docs"
description: "데이터 원본을 저장하기 위한 Azure 데이터 카탈로그 및 나중에 다시 사용하기 위한 데이터 자산의 기능을 강조 표시하는 방법 문서입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 10/10/2016
ms.author: maroche
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: f017776480466979d7f2f9edec2b3ac5caca2321


---
# <a name="how-to-save-searches-and-pin-data-assets"></a>검색을 저장하고 데이터 자산을 고정하는 방법
## <a name="introduction"></a>소개
Microsoft Azure 데이터 카탈로그는 데이터 원본 검색에 대한 기능을 제공합니다. 사용자는 신속하게 검색하고 카탈로그를 필터링하여 쉽게 당면한 작업에 대한 적절한 데이터를 찾을 수 있도록 데이터 원본을 찾고 원래 용도를 이해합니다.

그러나 사용자가 동일한 데이터를 정기적으로 사용해야 하는 경우에는 어떨까요? 사용자가 카탈로그에서 동일한 데이터 원본에 지식을 정기적으로 제공하는 경우에는 어떨까요? 이러한 상황에서 동일한 검색을 반복적으로 실행하면 비효율적일 수 있습니다. 저장된 검색 및 고정된 데이터 자산이 도움이 될 수 있습니다.

## <a name="saved-searches"></a>저장된 검색
Azure 데이터 카탈로그에 저장된 검색은 재사용 가능한 사용자 단위 검색 정의입니다. 사용자가 검색 용어, 태그 및 기타 필터를 포함한 검색을 정의하면 나중에 사용하기 위해 저장할 수 있습니다. 저장된 검색 정의는 나중에 다시 실행되어 해당 검색 조건과 일치하는 데이터 자산을 반환할 수 있습니다.

### <a name="creating-a-saved-search"></a>저장된 검색 만들기
저장된 검색을 만들려면 먼저 다시 사용할 검색 조건을 입력합니다. Azure 데이터 카탈로그 포털에서 "현재 검색" 상자에 있는 "저장" 링크를 클릭합니다.

 !['저장'을 선택하여 현재 검색 설정 저장](./media/data-catalog-how-to-save-pin/01-save-option.png)

대화 상자가 나타나면 저장된 검색에 이름을 입력합니다. 검색에 의해 반환되는 데이터 자산 중에 의미가 있고 설명이 포함된 이름을 선택합니다.

 ![저장된 검색에 이름 제공](./media/data-catalog-how-to-save-pin/02-name.png)

### <a name="managing-saved-searches"></a>저장된 검색 관리
사용자가 하나 이상의 검색을 저장하면 "저장된 검색" 옵션은 "현재 검색" 상자에서 Azure 데이터 카탈로그 포털에 표시됩니다. 확장하면 전체 저장 검색 목록이 표시됩니다.

 ![저장된 검색의 목록](./media/data-catalog-how-to-save-pin/03-list.png)

목록에서 저장된 검색을 선택하면 검색이 실행됩니다.

드롭다운 메뉴를 선택하면 관리 옵션의 집합을 제공합니다.

 ![저장된 검색 관리에 대한 옵션](./media/data-catalog-how-to-save-pin/04-managing.png)

"이름 바꾸기"를 선택하면 저장된 검색에 새 이름을 입력하라는 메시지가 표시됩니다. 검색 정의는 변경되지 않습니다.

"삭제"를 선택하면 사용자에게 확인을 묻는 메시지가 표시된 다음 저장된 검색을 사용자의 목록에서 제거합니다.

"기본으로 저장"을 선택하면 사용자에 대한 기본 검색으로 선택한 저장된 검색을 표시합니다. 사용자가 Azure 데이터 카탈로그 홈 페이지에서 "빈" 검색을 수행하는 경우 사용자의 기본 검색이 실행됩니다. 또한 기본값으로 표시된 검색은 저장된 검색 목록 맨위에 나타납니다.

### <a name="organizational-saved-searches"></a>조직 저장된 검색
모든 사용자는 자신의 사용에 대한 검색을 저장할 수 있습니다. 데이터 카탈로그 관리자는 조직 내의 모든 사용자에 대한 검색을 저장할 수도 있습니다. 검색을 저장할 때 관리자에게 회사 내에서 저장된 검색을 공유하는 옵션이 제공됩니다. 이 옵션을 선택하는 경우 저장된 검색이 모든 사용자에 대해 사용할 수 있는 검색 목록에 포함됩니다.

 ![조직 저장된 검색](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>고정된 데이터 자산
저장된 검색을 사용하면 사용자가 검색 정의를 저장하고 다시 사용할 수 있습니다. 검색에서 반환된 데이터 자산은 카탈로그의 내용이 변경되면 시간에 따라 변경될 수 있습니다. 고정된 데이터 자산을 사용하면 사용자가 검색을 사용할 필요 없이 쉽게 액세스할 수 있게 하는 특정 데이터 자산을 명시적으로 식별할 수 있습니다.

고정된 데이터 자산은 간단합니다. 사용자는 데이터 자산에 대한 "고정" 아이콘을 클릭하기만 하여 고정된 목록에 추가합니다. 이 아이콘은 Azure 데이터 카탈로그 포털의 목록 뷰 중 가장 왼쪽 열에 있는 타일 뷰에서 자산 타일의 모퉁이에 나타납니다.

![데이터 자산 고정](./media/data-catalog-how-to-save-pin/05-pinning.png)

자산의 고정을 해제하는 것도 동일하게 간단합니다. 사용자가 "고정" 아이콘을 다시 클릭하여 선택한 자산에 대한 설정을 전환하면 됩니다.

![데이터 자산 고정 해제](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="my-assets"></a>“내 자산”
Azure 데이터 카탈로그 포털 홈 페이지는 현재 사용자에 대한 관심 자산을 표시하는 "내 자산" 섹션을 포함합니다. 이 섹션은 고정된 자산 및 저장된 검색을 모두 포함합니다.

![홈 페이지에서 '내 자산'](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>요약
Azure 데이터 카탈로그는 사용자가 필요한 데이터 원본을 쉽게 검색할 수 있는 기능을 제공하므로 데이터를 찾는 시간이 줄고 작업하는 시간은 늘어나게 됩니다. 저장된 검색 및 고정된 데이터 자산은 이러한 핵심 기능을 작성하므로 사용자가 반복해서 작업할 데이터 원본을 쉽게 식별할 수 있습니다.




<!--HONumber=Nov16_HO3-->


