---
title: Azure Active Directory B2B 공동 작업 미리 보기에 대한 외부 사용자 토큰 형식 | Microsoft Docs
description: Azure Active Directory B2B는 비즈니스 파트너가 회사 응용 프로그램을 선택적으로 액세스할 수 있도록 하여 사용자 회사 간 관계를 지원합니다.
services: active-directory
documentationcenter: ''
author: viv-liu
manager: cliffdi
editor: ''
tags: ''

ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/09/2016
ms.author: viviali

---
# Azure AD B2B 공동 작업 미리 보기: 외부 사용자 토큰 형식
표준 Azure AD 토큰에 대한 클레임은 azure.microsoft.com의 [지원 토큰 및 클레임 유형](active-directory-token-and-claims.md) 기사에서 설명됩니다.

인증된 B2B 공동 작업 외부 사용자가 다른 클레임은 다음과 같습니다.<br/>

* **OID:** 리소스 테넌트의 개체 ID<br/>
* **TID:** 리소스 테넌트의 테넌트 ID<br/>
* **발급자**: 리소스 테넌트<br/>
* **IDP**: 사용자의 홈 테넌트<br/>
* **AltSecId**: 불투명한 대체 보안 ID<br/>

## 관련 문서
Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [작동 방법](active-directory-b2b-how-it-works.md)
* [자세한 연습](active-directory-b2b-detailed-walkthrough.md)
* [CSV 파일 형식 참조](active-directory-b2b-references-csv-file-format.md)
* [외부 사용자 개체 특성 변경](active-directory-b2b-references-external-user-object-attribute-changes.md)
* [현재 미리 보기 제한 사항](active-directory-b2b-current-preview-limitations.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

<!---HONumber=AcomDC_0511_2016-->