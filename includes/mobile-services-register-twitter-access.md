

새 Twitter v1.1 API에서는 앱이 리소스에 액세스하기 전에 인증해야 합니다. 먼저 OAuth 2.0을 사용하여 액세스를 요청하는 데 필요한 자격 증명을 가져와야 합니다. 그런 다음 모바일 서비스의 앱 설정에 자격 증명을 안전하게 저장합니다.

1. 아직 그렇게 하지 않은 경우 [모바일 서비스에 Twitter 로그인을 사용하기 위해 앱 등록](../articles/mobile-services/mobile-services-how-to-register-twitter-authentication.md) 항목의 단계를 완료합니다. 
   
      Twitter에서는 Twitter v1.1 API에 액세스하는 데 필요한 자격 증명을 생성합니다. Twitter 개발자 웹 사이트에서 세 가지 자격 증명을 가져올 수 있습니다.
2. [Twitter 개발자](http://go.microsoft.com/fwlink/p/?LinkId=268300) 웹 사이트로 이동하고 Twitter 계정 자격 증명을 사용하고 Twitter 앱을 선택합니다.
3. 앱의 **키 및 액세스 토큰** 탭에서 다음 값을 기록해 둡니다.
   
   * **소비자 키**
   * **소비자 암호**
   * **액세스 토큰**
   * **액세스 토큰 암호**
4. [Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인하고 **모바일 서비스**를 클릭한 후 모바일 서비스를 클릭합니다.
5. **ID** 탭을 클릭하고 Twitter에서 가져온 **Consumer key** 및 **Consumer secret** 값을 입력하고 **저장**을 클릭합니다.
   
    ![](./media/mobile-services-register-twitter-access/mobile-identity-tab-twitter-only.png)
6. **구성** 탭을 클릭하고 **앱 설정**까지 아래로 스크롤하여 다음에 대해 Twitter 사이트에서 가져온 각 **이름** 및 **값** 쌍을 입력한 후 **저장**을 클릭합니다.
   
   * `TWITTER_ACCESS_TOKEN`
   * `TWITTER_ACCESS_TOKEN_SECRET`
     
     ![](./media/mobile-services-register-twitter-access/mobile-schedule-job-app-settings.png)
     
     그러면 앱 설정에 Twitter 액세스 토큰이 저장됩니다. **ID** 탭의 소비자 자격 증명과 같이 액세스 자격 증명도 앱 설정에 암호화되어 저장되며, 스크립트 파일에서 해당 자격 증명을 하드 코드하지 않고도 서버 스크립트에서 액세스할 수 있습니다. 자세한 내용은 [앱 설정]을 참조하세요.

<!-- URLs. -->
[Mobile Services server script reference]: http://go.microsoft.com/fwlink/?LinkId=262293
[Register your apps for Twitter login with Mobile Services]: ../articles/mobile-services/mobile-services-how-to-register-twitter-authentication.md
[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[앱 설정]: http://msdn.microsoft.com/library/azure/b6bb7d2d-35ae-47eb-a03f-6ee393e170f7

<!---HONumber=AcomDC_0218_2016-->