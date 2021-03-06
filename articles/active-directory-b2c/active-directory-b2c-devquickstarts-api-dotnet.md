---
title: Azure AD B2C | Microsoft Docs
description: "Azure Active Directory B2C를 사용하여 .NET Web API를 빌드하는 방법이며 인증을 위해 OAuth 2.0 액세스 토큰을 사용하여 보호됩니다."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/22/2016
ms.author: dastrock
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: 1062af9abfd167dd251621a43943dea399aed027


---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: .NET Web API 빌드
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Azure AD(Azure Active Directory) B2C로 OAuth 2.0 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다. 이 토큰을 통해 클라이언트 앱이 Azure AD B2C를 사용하여 API에 인증할 수 있습니다. 이 문서에서는 사용자에게 CRUD 작업을 허용하는 .NET MVC(모델-뷰-컨트롤러) "할 일 모음" API를 만드는 방법을 보여 줍니다. Web API는 Azure AD B2C를 사용하여 보호되며 사용자가 해당 할 일 목록을 관리하도록 인증할 수 있습니다.

## <a name="create-an-azure-ad-b2c-directory"></a>Azure AD B2C 디렉터리 만들기
Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다. 디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다. 아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.

## <a name="create-an-application"></a>응용 프로그램 만들기
다음으로 B2C 디렉터리에서 앱을 만들어야 합니다. 앱과 안전하게 통신하는 데 필요한 Azure AD 정보를 제공합니다. 앱을 만들려면 [다음 지침](active-directory-b2c-app-registration.md)에 따릅니다. 다음을 수행해야 합니다.

* 응용 프로그램에서 **웹앱** 또는 **Web API**를 포함합니다.
* 웹앱의 경우 **URI(Uniform Resource Identifier) 리디렉션** `https://localhost:44316/`을 사용합니다. 이 코드 샘플에 대한 웹앱 클라이언트의 기본 위치입니다.
* 앱에 할당된 **응용 프로그램 ID** 를 복사합니다. 나중에 필요합니다.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>정책 만들기
Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다. 이 코드 샘플의 클라이언트는 등록, 로그인 및 편집 프로필 등 세 가지 ID 환경을 포함합니다. [정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 각 형식에 대한 정책을 만들어야 합니다. 세 가지 정책을 만들 때 다음을 확인합니다.

* ID 공급자 블레이드에서 **사용자 ID 등록** 또는 **메일 등록** 중 하나를 선택합니다.
* 등록 정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.
* 모든 정책에 대한 응용 프로그램 클레임으로 **표시 이름** 및 **개체 ID** 클레임을 선택합니다. 물론 다른 클레임을 선택할 수 있습니다.
* 각 정책을 만든 후에 **이름** 을 복사합니다. 이러한 정책 이름이 나중에 필요합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

세 가지 정책을 성공적으로 만들면 앱을 빌드할 준비가 되었습니다.

## <a name="download-the-code"></a>코드 다운로드
이 자습서에 대한 코드는 [GitHub에서 유지 관리됩니다](https://github.com/AzureADQuickStarts/B2C-WebAPI-DotNet). 진행하면서 샘플을 빌드하기 위해 [골격 프로젝트를 .zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-WebAPI-DotNet/archive/skeleton.zip)할 수 있습니다. 구조를 복제할 수도 있습니다.

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-DotNet.git
```

완성된 앱도 [.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-WebAPI-DotNet/archive/complete.zip)하거나 동일한 리포지토리의 `complete` 분기에서 사용할 수 있습니다.

샘플 코드를 다운로드한 후 Visual Studio .sln 파일을 열어 시작합니다. 이제 솔루션에는 `TaskWebApp`과 `TaskService`, 2개의 프로젝트가 있습니다. `TaskWebApp` 은 사용자와 상호 작용하는 MVC 웹 응용 프로그램입니다. `TaskService` 는 각 사용자의 할 일 모음을 저장하는 앱의 백 엔드 Web API입니다.

## <a name="configure-the-task-web-app"></a>작업 웹앱 구성
사용자가 `TaskWebApp`을 조작할 때 클라이언트는 Azure AD로 요청을 보내고 `TaskService` Web API를 호출하는 데 사용할 수 있는 토큰을 받습니다. 사용자를 로그인하고 토큰을 가져오기 위해 응용 프로그램에 대한 정보와 함께 `TaskWebApp` 을 제공해야 합니다. `TaskWebApp` 프로젝트에서 프로젝트 루트에 있는 `web.config` 파일을 열고 `<appSettings>` 섹션의 값을 바꿉니다.  `AadInstance`, `RedirectUri` 및 `TaskServiceUrl` 값을 있는 그대로 둘 수 있습니다.

```
  <appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="ida:Tenant" value="fabrikamb2c.onmicrosoft.com" />
    <add key="ida:ClientId" value="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6" />
    <add key="ida:AadInstance" value="https://login.microsoftonline.com/{0}/v2.0/.well-known/openid-configuration?p={1}" />
    <add key="ida:RedirectUri" value="https://localhost:44316/" />
    <add key="ida:SignUpPolicyId" value="b2c_1_sign_up" />
    <add key="ida:SignInPolicyId" value="b2c_1_sign_in" />
    <add key="ida:UserProfilePolicyId" value="b2c_1_edit_profile" />
    <add key="api:TaskServiceUrl" value="https://localhost:44332/" />
  </appSettings>
```

이 문서에서는 `TaskWebApp` 클라이언트를 구축하는 방법을 다루지 않습니다.  Azure AD B2C를 사용하여 웹앱을 구축하는 방법을 알아보려면 [.NET 웹앱 자습서](active-directory-b2c-devquickstarts-web-dotnet.md)를 참조하세요.

## <a name="secure-the-api"></a>API 보호
사용자를 대신해서 API를 호출하는 클라이언트가 있는 경우 OAuth 2.0 전달자 토큰을 사용하여 `TaskService` 보안을 유지할 수 있습니다. API는 Microsoft OWIN(Open Web Interface for .NET)을 사용하여 토큰을 허용하고 유효성을 검사할 수 있습니다.

### <a name="install-owin"></a>OWIN 설치
OWIN OAuth 인증 파이프라인을 설치하여 시작합니다.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

### <a name="enter-your-b2c-details"></a>B2C 세부 정보 입력
`TaskService` 프로젝트의 루트에 있는 `web.config` 파일을 열고 `<appSettings>` 섹션의 값을 바꿉니다. 이러한 값은 API 및 OWIN 라이브러리 전체에서 사용됩니다.  `AadInstance` 값을 변경하지 않고 둘 수 있습니다.

```
  <appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="ida:AadInstance" value="https://login.microsoftonline.com/{0}/v2.0/.well-known/openid-configuration?p={1}" />
    <add key="ida:Tenant" value="fabrikamb2c.onmicrosoft.com" />
    <add key="ida:ClientId" value="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6" />
    <add key="ida:SignUpPolicyId" value="b2c_1_sign_up" />
    <add key="ida:SignInPolicyId" value="b2c_1_sign_in" />
    <add key="ida:UserProfilePolicyId" value="b2c_1_edit_profile" />
  </appSettings>
```

### <a name="add-an-owin-startup-class"></a>OWIN 시작 클래스 추가
`Startup.cs`라는 `TaskService` 프로젝트에 OWIN 시작 클래스를 추가합니다.  프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** 및 **새 항목**을 선택한 다음 OWIN을 검색합니다.

```C#
// Startup.cs

// Change the class declaration to "public partial class Startup" - we’ve already implemented part of this class for you in another file.
public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a>OAuth 2.0 인증 구성
`App_Start\Startup.Auth.cs` 파일을 열고 `ConfigureAuth(...)` 메서드를 구현합니다.

```C#
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // These values are pulled from web.config
    public static string aadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
    public static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
    public static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    public static string signUpPolicy = ConfigurationManager.AppSettings["ida:SignUpPolicyId"];
    public static string signInPolicy = ConfigurationManager.AppSettings["ida:SignInPolicyId"];
    public static string editProfilePolicy = ConfigurationManager.AppSettings["ida:UserProfilePolicyId"];

    public void ConfigureAuth(IAppBuilder app)
    {   
        app.UseOAuthBearerAuthentication(CreateBearerOptionsFromPolicy(signUpPolicy));
        app.UseOAuthBearerAuthentication(CreateBearerOptionsFromPolicy(signInPolicy));
        app.UseOAuthBearerAuthentication(CreateBearerOptionsFromPolicy(editProfilePolicy));
    }

    public OAuthBearerAuthenticationOptions CreateBearerOptionsFromPolicy(string policy)
    {
        TokenValidationParameters tvps = new TokenValidationParameters
        {
            // This is where you specify that your API only accepts tokens from its own clients
            ValidAudience = clientId,
            AuthenticationType = policy,
        };

        return new OAuthBearerAuthenticationOptions
        {
            // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
            AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(aadInstance, tenant, policy))),
        };
    }
}
```

### <a name="secure-the-task-controller"></a>작업 컨트롤러 보호
앱을 OAuth 2.0 인증을 사용하도록 구성한 후 작업 컨트롤러에 `[Authorize]` 태그를 추가하여 Web API를 보호할 수 있습니다. 할 일 모음 조작이 발생하는 컨트롤러이므로 클래스 수준에서 전체 컨트롤러를 보호해야 합니다. 보다 세분화한 제어를 위해 개별 작업에 `[Authorize]` 태그를 추가할 수도 있습니다.

```C#
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a>토큰에서 사용자 정보 가져오기
`TasksController` 는 데이터베이스에 작업을 저장하며, 여기서 각 작업에는 작업을 "소유"하는 연결된 사용자가 있습니다. 소유자는 사용자의 **개체 ID**로 식별됩니다. (따라서 모든 정책에 응용 프로그램 클레임으로 개체 ID를 추가해야 했습니다.)

```C#
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

## <a name="run-the-sample-app"></a>샘플 앱 실행
마지막으로 `TaskWebApp`과 `TaskService`를 모두 빌드하고 실행합니다. 메일 주소 또는 사용자 이름을 사용하여 앱에 등록합니다. 사용자의 할 일 모음에 일부 작업을 만들고 클라이언트를 중지하고 다시 시작한 후에 API에서 어떻게 유지할지 확인합니다.

## <a name="edit-your-policies"></a>청책 편집
Azure AD B2C를 사용하여 API를 보호한 후 앱의 정책을 시험해 보고 API에서 효과(또는 부족)를 확인할 수 있습니다. 정책에서 응용 프로그램 클레임을 조작하고 Web API에서 사용할 수 있는 사용자 정보를 변경할 수 있습니다. 이 문서의 앞에서 설명한 것처럼 추가한 모든 클레임은 `ClaimsPrincipal` 개체의 .NET MVC Web API에서 사용할 수 있습니다.

<!--

## Next steps

You can now move onto more advanced B2C topics. You may try:

[Call a web API from a web app]()

[Customize the UX of your B2C app]()

-->



<!--HONumber=Dec16_HO2-->


