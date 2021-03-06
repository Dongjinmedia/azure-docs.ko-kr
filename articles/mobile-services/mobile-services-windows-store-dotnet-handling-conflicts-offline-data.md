---
title: 범용 Windows 앱에서 오프라인 데이터를 사용하여 충돌 처리 | Microsoft Docs
description: 범용 Windows 응용 프로그램에서 오프라인 데이터를 동기화할 때 Azure 모바일 서비스를 사용하여 충돌을 처리하는 방법에 대해 알아봅니다.
documentationcenter: windows
author: wesmc7777
manager: dwrede
editor: ''
services: mobile-services

ms.service: mobile-services
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 07/21/2016
ms.author: glenga

---
# 모바일 서비스에서 오프라인 데이터 동기화를 사용하여 충돌 처리
[!INCLUDE [mobile-service-note-mobile-apps](../../includes/mobile-services-note-mobile-apps.md)]

&nbsp;

[!INCLUDE [mobile-services-selector-offline-conflicts](../../includes/mobile-services-selector-offline-conflicts.md)]

## 개요
이 항목에서는 Azure 모바일 서비스의 오프라인 기능을 사용할 때 데이터를 동기화하고 충돌을 처리하는 방법을 보여 줍니다.

동영상을 시청하려는 경우 아래쪽의 클립은 이 자습서와 동일한 단계를 따릅니다.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Build-offline-apps-Azure-Mobile-Services/player]
> 
> 

이 자습서에서는 오프라인 동기화 충돌 처리를 지원하는 앱의 범용 Windows C# 솔루션을 다운로드합니다. 모바일 서비스를 앱과 통합한 후 Windows 스토어 8.1 및 Windows Phone 8.1 클라이언트를 실행하여 동기화 충돌을 생성하고 해결합니다.

이 자습서는 이전 자습서인 [오프라인 데이터 시작]의 단계 및 샘플 앱을 기반으로 합니다. 이 자습서를 시작하기 전에 먼저 [오프라인 데이터 시작]을 완료해야 합니다.

## 필수 조건
이 자습서를 사용하려면 Windows 8.1에서 실행 중인 Visual Studio 2013이 필요합니다.

## 샘플 프로젝트 다운로드
![][0]

이 자습서에서는 [Todo 오프라인 모바일 서비스 샘플]에서 로컬 오프라인 저장소와 Azure의 모바일 서비스 데이터베이스 간 동기화 충돌을 처리하는 방법을 연습합니다.

1. [모바일 서비스 샘플 Github 리포지토리] zip 파일을 다운로드하여 작업 디렉터리에 압축을 풉니다.
2. [오프라인 데이터 시작] 자습서에 언급된 대로 Windows 8.1용 SQLite 및 Windows Phone 8.1용 SQLite를 아직 설치하지 않은 경우 두 런타임을 모두 설치합니다.
3. Visual Studio 2013에서 *mobile-services-samples\\TodoOffline\\WindowsUniversal\\TodoOffline-Universal.sln* 솔루션 파일을 엽니다. **F5**를 눌러 프로젝트를 다시 빌드하고 실행합니다. NuGet 패키지가 복원되고 참조가 올바르게 설정되었는지 확인합니다.
   
   > [!NOTE]
   > [오프라인 데이터 시작] 자습서에 언급된 대로 SQLite 런타임에 대한 이전 참조를 삭제하고 업데이트된 참조로 바꿔야 할 수 있습니다.
   > 
   > 
4. 앱에서 **TodoItem 삽입**에 일부 텍스트를 입력한 후 **저장**을 클릭하여 일부 todo 항목을 로컬 저장소에 추가합니다. 그런 다음 앱을 닫습니다.

앱이 모바일 서비스에 아직 연결되어 있지 않으므로 **푸시** 및 **끌어오기** 단추를 누르면 예외가 발생합니다.

## 모바일 서비스에 대해 앱 테스트
이제 모바일 서비스에 대해 앱을 테스트합니다.

1. [Azure 클래식 포털]의 **대시보드** 탭 명령 모음에서 **키 관리**를 클릭하여 모바일 서비스의 응용 프로그램 키를 찾습니다. **응용 프로그램 키**를 복사합니다.
2. Visual Studio용 솔루션 탐색기의 클라이언트 샘플 프로젝트에서 App.xaml.cs 파일을 엽니다. 모바일 서비스 URL 및 응용 프로그램 키를 사용하도록 **MobileServiceClient** 초기화를 변경합니다.
   
         public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://your-mobile-service.azure-mobile.net/",
            "Your AppKey"
        );
3. Visual Studio에서 **F5**를 눌러 다시 앱을 빌드하고 실행합니다.
   
    ![][0]

## 백 엔드에서 데이터를 업데이트하여 충돌 생성
실제로 한 앱에서 업데이트를 데이터베이스의 레코드에 푸시한 후 다른 앱에서 해당 레코드의 이전 버전 필드를 사용하는 동일한 레코드에 업데이트를 푸시하려고 하면 동기화 충돌이 발생합니다. [오프라인 데이터 시작]의 내용을 상기한다면 버전 시스템 속성이 오프라인 동기화 기능을 지원해야 합니다. 이 버전 정보는 각 데이터베이스 업데이트를 통해 검사합니다. 앱의 인스턴스에서 이전 버전을 사용하여 레코드를 업데이트하려고 하면 충돌이 발생하고 앱에서 `MobileServicePreconditionFailedException`(으)로 catch됩니다. 앱에서 `MobileServicePreconditionFailedException`을(를) catch하지 않으면 결국 발생한 동기화 오류 수를 설명하는 `MobileServicePushFailedException`이(가) 발생합니다.

> [!NOTE]
> 오프라인 데이터 동기화를 사용하여 삭제된 레코드의 동기화를 지원하려면 [일시 삭제](mobile-services-using-soft-delete.md)를 사용하도록 설정해야 합니다. 그렇지 않으면 로컬 저장소에서 레코드를 수동으로 제거하거나를 `IMobileServiceSyncTable::PurgeAsync()` 호출하여 로컬 저장소를 삭제해야 합니다.
> 
> 

다음 단계에서는 샘플을 사용하여 동시에 실행되는 Windows Phone 8.1 및 Windows 스토어 8.1 클라이언트로 인해 충돌이 발생하고 이러한 충돌을 해결하는 방법을 보여 줍니다.

1. Visual Studio에서 Windows Phone 8.1 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭합니다. 그런 다음 **Ctrl+F5**를 눌러 디버깅 없이 Windows Phone 8.1 클라이언트를 실행합니다. 에뮬레이터에서 Windows Phone 8.1 클라이언트를 실행하고 난 후 **끌어오기** 단추를 클릭하여 로컬 저장소를 데이터베이스의 현재 상태와 동기화합니다.
   
    ![][3]
2. Visual Studio에서 Windows 8.1 런타임 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭하여 다시 시작 프로젝트로 설정합니다. 그런 다음 **F5**를 눌러 실행합니다. Windows 스토어 8.1 클라이언트를 실행하고 난 후 **끌어오기** 단추를 클릭하여 로컬 저장소를 데이터베이스의 현재 상태와 동기화합니다.
   
    ![][4]
3. 이때 두 클라이언트 모두 데이터베이스와 동기화됩니다. 또한 두 클라이언트의 코드는 모두 완료되지 않은 todo 항목만 동기화하도록 증분 동기화를 사용합니다. 완료된 todo 항목은 무시됩니다. 항목 중 하나를 선택하고 두 클라이언트의 동일한 항목 텍스트가 서로 다른 값이 되도록 편집합니다. **푸시** 단추를 클릭하여 두 변경 내용을 모두 서버의 데이터베이스와 동기화합니다.
   
    ![][5]
   
    ![][6]
4. 푸시가 마지막으로 실행된 클라이언트에서 충돌이 발생하고 사용자는 데이터베이스에 커밋할 값을 결정할 수 있습니다. 예외는 충돌 해결에 사용되는 올바른 버전 값을 제공합니다.
   
    ![][7]

## 동기화 충돌 처리를 위한 코드 검토
모바일 서비스에 오프라인 기능을 사용하려면 로컬 데이터베이스와 데이터 전송 개체 둘 다에 버전 열을 포함해야 합니다. 이 작업은 `TodoItem` 클래스를 다음 멤버로 업데이트하여 수행합니다.

        [Version]
        public string Version { get; set; }

`TodoItem` 클래스가 로컬 저장소를 정의하는 데 사용되는 경우 `__version` 열이 `OnNavigatedTo()` 메서드에서 로컬 데이터베이스에 포함됩니다.

코드에서 오프라인 동기화 충돌을 처리하려면 `IMobileServiceSyncHandler`을(를) 구현하는 클래스를 만듭니다. `MobileServiceClient.SyncContext.InitializeAsync()`에 대한 호출에서 이 유형의 개체를 전달합니다. 이는 샘플의 `OnNavigatedTo()` 메서드에서도 발생합니다.

     await App.MobileService.SyncContext.InitializeAsync(store, new SyncHandler(App.MobileService));

**SyncHandler.cs**의 `SyncHandler` 클래스는 `IMobileServiceSyncHandler`을(를) 구현합니다. `ExecuteTableOperationAsync` 메서드는 푸시 작업이 서버에 전송될 때마다 호출됩니다. `MobileServicePreconditionFailedException` 유형의 예외가 발생하면 항목의 로컬 버전과 원격 버전 사이에 충돌이 있는 것입니다.

로컬 항목을 기준으로 충돌을 해결하려면 작업을 다시 시도하면 됩니다. 충돌이 발생한 경우 로컬 항목이 서버 버전과 일치하도록 업데이트되므로, 작업을 다시 실행하면 서버 변경 내용을 로컬 변경 내용으로 덮어씁니다.

    await operation.ExecuteAsync();

서버 항목을 기준으로 충돌을 해결하려면 `ExecuteTableOperationAsync`에서 되돌립니다. 개체의 로컬 버전이 삭제되고 서버의 값으로 바뀝니다.

푸시 작업을 중지하고 대기 중인 변경 내용은 유지하려면 `AbortPush()` 메서드를 사용합니다.

    operation.AbortPush();

`AbortPush`이(가) `ExecuteTableOperationAsync`에서 호출되는 경우 현재 작업을 포함하여 현재 푸시 작업은 중지되지만 대기 중인 변경 내용은 모두 유지됩니다. 다음에 `PushAsync()`을(를) 호출하면 변경 내용이 서버에 전송됩니다.

푸시를 취소하면 `PushAsync`에서 `MobileServicePushFailedException`을(를) 내어 예외 속성인 `PushResult.Status`이(가) `MobileServicePushStatus.CancelledByOperation` 값을 포함합니다.

<!-- Images -->
[0]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/mobile-services-handling-conflicts-app-run1.png
[1]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/javascript-backend-database.png
[2]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/dotnet-backend-database.png
[3]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/wp81-view.png
[4]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/win81-view.png
[5]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/wp81-edit-text.png
[6]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/win81-edit-text.png
[7]: ./media/mobile-services-windows-store-dotnet-handling-conflicts-offline-data/conflict.png




<!-- URLs -->
[Handling conflicts code sample]: http://go.microsoft.com/fwlink/?LinkId=394787
[Get started with Mobile Services]: ../mobile-services-windows-store-get-started.md
[오프라인 데이터 시작]: mobile-services-windows-store-dotnet-get-started-offline-data.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkId=394776
[Azure 클래식 포털]: https://manage.windowsazure.com/
[Handling Database Conflicts]: mobile-services-windows-store-dotnet-handle-database-conflicts.md#test-app
[모바일 서비스 샘플 Github 리포지토리]: http://go.microsoft.com/fwlink/?LinkId=512865
[Todo 오프라인 모바일 서비스 샘플]: http://go.microsoft.com/fwlink/?LinkId=512866

<!---HONumber=AcomDC_0727_2016-->