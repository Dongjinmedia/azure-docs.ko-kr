---
title: "Azure Active Directory B2C: 프로덕션 규모와 B2C 테넌트 미리 보기 비교 | Microsoft Docs"
description: "Azure Active Directory B2C 테넌트 유형에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
translationtype: Human Translation
ms.sourcegitcommit: 4b13c040a15bef2f04d2cd2126e2270d061898bd
ms.openlocfilehash: a37992cd2bfe346fd171bde15b6180c56527289b


---
# <a name="azure-active-directory-b2c-production-scale-vs-preview-b2c-tenants"></a>Azure Active Directory B2C: 프로덕션 규모와 B2C 테넌트 미리 보기 비교
Azure Active Directory (Azure AD) B2C에서 프로덕션 앱을 작성하려는 경우 테넌트 "형식"이 올바른지 확인해야 바로 사용할 수 있습니다. 현재 환경을 보려면 다음 단계에 따라 Azure 포털의 [B2C 기능 블레이드로 이동](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) 하여 **테넌트 형식**을 확인합니다.

## <a name="summary"></a>요약
Azure AD B2C는 북아메리카의 **프로덕션 규모** B2C 테넌트에서만 프로덕션 앱을 지원합니다.

| 테넌트 형식 | 국가/지역 | 일반적으로 사용 가능합니까? |
| --- | --- | --- |
| **프로덕션 규모 테넌트** |북아메리카 국가/지역 |예 |
| **프로덕션 규모 테넌트** |북아메리카를 제외한 모든 국가/지역 |아니요 |
| **테넌트 미리 보기** |모든 국가/지역 |아니요 |

> [!NOTE]
> Azure AD B2C 테넌트(소비자용)은 Azure AD 테넌트(직원용)를 사용할 수 있는 국가나 지역에서는 현재 사용할 수 없습니다. 더 자세한 내용은 다음 섹션을 읽어 보세요.
> 
> 

## <a name="production-scale-b2c-tenant-in-north-america"></a>북아메리카의 프로덕션 규모 B2C 테넌트
북아메리카에서 [B2C 테넌트를 만든](active-directory-b2c-get-started.md) 경우 다음 국가 또는 지역 중 한 곳입니다. 미국, 캐나다, 코스타리카, 도미니카 공화국, 엘살바도르, 과테말라, 멕시코, 파나마, 푸에르토리코, 트리니다드토바고 등이고, B2C 관리자 UI의 **테넌트 유형**은 **프로덕션 규모**라고 하며, 테넌트는 프로덕션 앱에 대해 사용될 수 있습니다.

> [!NOTE]
> 프로덕션 규모 테넌트는 소비자 ID를 테넌트당 수억 명까지 확장할 수 있습니다.
> 
> 

![프로덕션 규모 테넌트의 스크린 샷](./media/active-directory-b2c-reference-tenant-type/production-scale-b2c-tenant.png)

## <a name="preview-b2c-tenant-in-any-countryregion"></a>모든 국가/지역에서 B2C 테넌트 미리 보기
Azure AD B2C 미리 보기 기간 동안 B2C 테넌트를 만든 경우 **테넌트 유형**은 **미리 보기 테넌트**라고 할 가능성이 있습니다. 이런 경우 테넌트를 개발 및 테스트 목적에만 사용하고 프로덕션 앱용으로 사용하지 말아야 합니다.

> [!IMPORTANT]
> 미리 보기 B2C 테넌트로부터 프로덕션 규모 B2C 테넌트로의 마이그레이션 경로가 없습니다. 미리 보기 B2C 테넌트를 삭제하고 동일한 도메인 이름으로 프로덕션 규모 B2C 테넌트를 다시 만들어야 하는 경우 알려진 문제가 발생합니다. 다른 도메인 이름으로 프로덕션 규모 B2C 테넌트를 만들어야 합니다.
> 
> 

![미리 보기 테넌트의 스크린 샷](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)

## <a name="production-scale-b2c-tenant-outside-of-north-america"></a>북아메리카 이외 지역의 프로덕션 규모 B2C 테넌트
Azure AD B2C는 현재 북아메리카 이외 지역에서 일반적으로 사용 가능하지 않습니다. 하지만 다음 국가나 지역에서 개발 및 테스트 목적으로 프로덕션 규모 테넌트를 만들어 사용할 수 있습니다. 알제리, 오스트리아, 아제르바이잔, 바레인, 벨로루시, 벨기에, 불가리아, 크로아티아, 키프로스, 체코, 덴마크, 이집트, 에스토니아, 핀란드, 프랑스, 독일, 그리스, 헝가리, 아이슬란드, 아일랜드, 이스라엘, 이탈리아, 요르단, 카자흐스탄, 케냐, 쿠웨이트, 라트비아, 레바논, 리히텐슈타인, 리투아니아, 룩셈부르크, 마케도니아 공화국, 몰타, 몬테네그로, 모로코, 네덜란드, 나이지리아, 노르웨이, 오만, 파키스탄, 폴란드, 포르투갈, 카타르, 루마니아, 러시아, 사우디아라비아, 세르비아, 슬로바키아, 슬로베니아, 남아프리카 공화국, 스페인, 스웨덴, 스위스, 튀니지, 터키, 우크라이나 아랍에미리트 및 영국.

Azure AD B2C가 위의 국가 또는 지역에서 일반 공급을 발표하면 계속해서 이러한 프로덕션 규모 테넌트를 사용하고 데이터 손실 없이 프로덕션 앱을 가동할 수 있습니다.

## <a name="availability-of-b2c-tenants"></a>B2C 테넌트의 가용성
B2C 테넌트는 다음 국가 또는 지역에서 현재 사용할 수 없습니다. 아프가니스탄, 아르헨티나, 오스트레일리아, 브라질, 칠레, 콜롬비아, 에콰도르, 홍콩 특별 행정구, 인도, 인도네시아, 이라크, 일본, 한국, 말레이시아, 뉴질랜드, 파라과이, 페루, 필리핀, 싱가포르, 스리랑카, 대만, 태국, 우루과이 및 베네수엘라. 나중에 포함시킬 계획입니다.




<!--HONumber=Dec16_HO5-->


