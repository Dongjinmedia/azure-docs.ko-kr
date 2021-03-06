---
title: "Azure MFA 및 AD FS를 사용하여 클라우드 리소스 보안 유지"
description: "클라우드에서 Azure MFA 및 AD FS 시작 방법을 설명하는 Azure Multi-Factor Authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/14/2016
ms.author: kgremban
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: 0a9ab0aca1a77245f360d0d8976aa9b8f59f15a0


---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지
조직이 Azure Active Directory와 페더레이션되어 있는 경우 Azure Multi-Factor Authentication 또는 Active Directory Federation Services를 사용하여 Azure AD에서 액세스하는 리소스를 보호합니다. Azure Multi-Factor Authentication 또는 Active Directory Federation Services를 사용하여 Azure Active Directory 리소스를 보호하려면 다음 절차를 따르세요.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>AD FS를 사용하여 Azure AD 리소스 보안 유지
클라우드 리소스를 보호하려면 먼저 사용자에 대한 계정을 설정한 다음 클레임 규칙을 설정합니다. 다음 단계를 수행하려면 이 절차를 따르세요.

1. [Multi-Factor Authentication 켜기](multi-factor-authentication-get-started-cloud.md#turn-on-two-step-verification-for-users)에 설명된 단계에 따라 사용자가 계정을 사용하도록 설정합니다.
2. AD FS 관리 콘솔을 시작합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/adfs1.png)
3. **신뢰 당사자 트러스트**로 이동한 후 신뢰 당사자 트러스트를 마우스 오른쪽 단추로 클릭합니다. **클레임 규칙 편집...**을 선택합니다.
4. **규칙 추가...**를 클릭합니다.
5. 드롭다운에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.
6. 클레임 규칙의 이름을 입력합니다.
7. 사용자 지정 규칙에 다음 텍스트를 추가합니다.

    ```
    => issue(Type = "http://schemas.microsoft.com/claims/authnmethodsreferences", Value = "http://schemas.microsoft.com/claims/multipleauthn");
    ```

    해당 클레임:

    ```
    <saml:Attribute AttributeName="authnmethodsreferences" AttributeNamespace="http://schemas.microsoft.com/claims">
    <saml:AttributeValue>http://schemas.microsoft.com/claims/multipleauthn</saml:AttributeValue>
    </saml:Attribute>
    ```
8. **확인** 및 **마침**을 차례로 클릭합니다. AD FS 관리 콘솔을 닫습니다.

그러면 사용자는 온-프레미스 방법(예: 스마트 카드)을 사용하여 로그인을 완료할 수 있습니다.

## <a name="trusted-ips-for-federated-users"></a>페더레이션 사용자를 위한 신뢰할 수 있는 IP
신뢰할 수 있는 IP를 사용하면 관리자가 특정 IP 주소 또는 자신의 인트라넷 내에서 시작된 요청을 가진 페더레이션 사용자에 대한 2단계 확인을 바이패스할 수 있습니다. 다음 섹션에서는 페더레이션 사용자 인트라넷에서 요청이 시작되는 경우 페더레이션 사용자로 Azure Multi-Factor Authentication 신뢰할 수 있는 IP를 구성하고 2단계 확인을 바이패스하는 방법을 설명합니다. 이 작업은 들어오는 클레임(회사 네트워크 내부 클레임 형식 사용) 통과 또는 필터링 템플릿을 사용하도록 AD FS를 구성하여 수행합니다.

이 예제는 신뢰 당사자 트러스트에 대해 Office 365를 사용합니다.

### <a name="configure-the-ad-fs-claims-rules"></a>AD FS 클레임 규칙 구성
가장 먼저 AD FS 클레임을 구성합니다. 두 클레임 규칙을 만드는데 하나는 회사 네트워크 내부 클레임 형식에 대한 규칙이고 다른 하나는 사용자의 로그인 상태를 유지하기 위한 규칙입니다.

1. AD FS 관리를 엽니다.
2. 왼쪽에서 **신뢰 당사자 트러스트**를 선택합니다.
3. **Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집...**를 선택합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. 발급 변환 규칙에서 **규칙 추가**를 클릭합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. 변환 클레임 규칙 추가 마법사의 드롭다운 목록에서 **들어오는 클레임 통과 또는 필터링**을 선택하고 **다음**을 클릭합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. 클레임 규칙 이름 옆에 있는 상자에 규칙의 이름을 지정합니다. 예를 들어 InsideCorpNet입니다.
7. 들어오는 클레임 형식 옆의 드롭다운 목록에서 **회사 네트워크 내부**를 선택합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. **마침**을 클릭합니다.
9. 발급 변환 규칙에서 **규칙 추가**를 클릭합니다.
10. 변환 클레임 규칙 추가 마법사의 드롭다운 목록에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.
11. 클레임 규칙 이름 아래에 있는 상자에 *로그인한 사용자 유지*를 입력합니다.
12. 사용자 지정 규칙 상자에서 다음을 입력합니다.

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. **Finish**를 클릭합니다.
14. **Apply**를 클릭합니다.
15. **Ok**를 클릭합니다.
16. AD FS 관리를 닫습니다.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>페더레이션 사용자로 Azure Multi-Factor Authentication 신뢰할 수 있는 IP 구성
이제 클레임이 적용되었으므로 신뢰할 수 있는 IP를 구성할 수 있습니다.

1. [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.
2. 왼쪽에서 **Active Directory**를 클릭합니다.
3. 디렉터리에서 신뢰할 수 있는 IP를 설정하려는 디렉터리를 선택합니다.
4. 선택한 디렉터리에서 **구성**을 클릭합니다.
5. Multi-Factor Authentication 섹션에서 **서비스 설정 관리**를 클릭합니다.
6. 서비스 설정 페이지의 신뢰할 수 있는 IP에서 **내 인트라넷에서 페더레이션 사용자의 요청에 대한 Multi-Factor Authentication 건너뛰기**를 선택합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
7. **저장**을 클릭합니다.
8. 업데이트를 적용하면 **닫기**를 클릭합니다.

끝났습니다. 이제 회사 인트라넷 외부에서 클레임이 시작하는 경우 Office 365 페더레이션 사용자만 MFA를 사용해야 합니다.



<!--HONumber=Dec16_HO2-->


