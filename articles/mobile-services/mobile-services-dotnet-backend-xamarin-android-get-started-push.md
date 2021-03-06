---
title: Xamarin Android 앱용 모바일 서비스 시작 | Microsoft Docs
description: Azure 모바일 서비스와 알림 허브를 사용하여 Xamarin Android 앱에 푸시 알림을 보내는 방법에 대해 알아봅니다.
services: mobile-services
documentationcenter: xamarin
author: ggailey777
manager: dwrede
editor: mollybos

ms.service: mobile-services
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/21/2016
ms.author: glenga

---
# 모바일 서비스 앱에 푸시 알림 추가
[!INCLUDE [mobile-services-selector-get-started-push](../../includes/mobile-services-selector-get-started-push.md)]

&nbsp;

[!INCLUDE [mobile-service-note-mobile-apps](../../includes/mobile-services-note-mobile-apps.md)]

> 이 항목에 해당하는 모바일 앱 버전은 [Xamarin.Android 앱에 푸시 알림 추가](../app-service-mobile/app-service-mobile-xamarin-android-get-started-push.md)를 참조하세요.
> 
> 

## 개요
이 항목에서는 Azure 모바일 서비스를 사용하여 Xamarin.Android 앱에 푸시 알림을 보내는 방법을 보여 줍니다. 이 자습서에서는 GCM(Google Cloud Messaging)을 사용하여 [모바일 서비스 시작] 프로젝트에 푸시 알림을 추가합니다. 이 작업을 완료하면 레코드가 삽입될 때마다 모바일 서비스에서 푸시 알림을 전송합니다.

이 자습서를 사용하려면 다음이 필요합니다.

* 활성 Google 계정.
* [Google Cloud Messaging 클라이언트 구성 요소]. 자습서에 이 구성 요소가 추가됩니다.

[모바일 서비스 시작]을 완료하면 프로젝트에 Xamarin.Android 및 [Azure 모바일 서비스][Azure Mobile Services Component] 구성 요소가 설치되어 있어야 합니다.

## <a id="register"></a>Google Cloud Messaging 사용
[!INCLUDE [GCM 사용](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a id="configure"></a>푸시 요청을 전송하도록 모바일 서비스 구성
[!INCLUDE [mobile-services-android-configure-push](../../includes/mobile-services-android-configure-push.md)]

## <a id="update-server"></a>푸시 알림을 전송하도록 모바일 서비스 업데이트
[!INCLUDE [mobile-services-dotnet-backend-android-push-update-service](../../includes/mobile-services-dotnet-backend-android-push-update-service.md)]

## <a id="configure-app"></a>푸시 알림에 대한 기존 프로젝트 구성
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>앱에 푸시 알림 코드 추가
[!INCLUDE [mobile-services-xamarin-android-push-add-to-app](../../includes/mobile-services-xamarin-android-push-add-to-app.md)]

## <a name="test-app"></a>게시된 모바일 서비스에 대해 앱 테스트
USB 케이블로 Android 휴대폰을 직접 연결하거나 에뮬레이터에서 가상 장치를 사용하여 앱을 테스트할 수 있습니다.

### <a id="local-testing"></a> 로컬 테스트에 푸시 알림 사용
[!INCLUDE [mobile-services-dotnet-backend-configure-local-push](../../includes/mobile-services-dotnet-backend-configure-local-push.md)]

[!INCLUDE [mobile-services-android-push-notifications-test](../../includes/mobile-services-android-push-notifications-test.md)]

<!-- URLs. -->
[모바일 서비스 시작]: mobile-services-dotnet-backend-xamarin-android-get-started.md
[Google Cloud Messaging 클라이언트 구성 요소]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/

<!---HONumber=AcomDC_0727_2016-->