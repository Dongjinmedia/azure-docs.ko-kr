---
title: "StorSimple 가상 배열 작업 보기 및 관리 | Microsoft Docs"
description: "StorSimple Manager 서비스 작업 페이지에 대해 설명하고 이 페이지를 사용하여 StorSimple 가상 배열에 대한 최근 및 현재 작업을 추적하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 789f7e04-7b3f-456d-be69-37ea48446e9b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/07/2016
ms.author: alkohli
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: d6a0d156e90bfbf16712f9093284e34edd493484


---
# <a name="use-the-storsimple-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a>StorSimple 관리자 서비스를 사용하여  StorSimple 가상 배열에 대한 작업 보기
## <a name="overview"></a>개요
**작업** 페이지에서는 StorSimple 관리자 서비스에 연결된 가상 배열(온-프레미스 가상 장치라고도 함)에서 시작한 작업을 보고 관리하기 위한 단일 중앙 포털을 제공합니다. 여러 가상 장치에 대한 실행, 완료 및 실패한 작업을 볼 수 있습니다. 결과는 표 형식으로 나타납니다. 

![작업 페이지](./media/storsimple-ova-manage-jobs/ovajobs1.png)

다음과 같이 필드에서 필터링하여 관심 있는 작업을 빠르게 찾을 수 있습니다.

* **상태** – 모두, 실행 중, 완료 또는 실패한 작업을 검색할 수 있습니다.
* **시작 및 종료** – 작업은 날짜 및 시간 범위에 따라 필터링할 수 있습니다.
* **유형** – 작업 유형은 모두, 백업, 복원, 장애 조치, 업데이트 다운로드 또는 업데이트 설치일 수 있습니다.
* **장치** – 작업은 서비스에 연결된 특정 장치에서 시작됩니다. 필터링된 작업은 다음과 같은 특성을 기반으로 표로 정리됩니다.
  
  * **유형** – 작업 유형은 모두, 백업, 복원, 장애 조치, 업데이트 다운로드 또는 업데이트 설치일 수 있습니다.
  * **상태** - 작업은 모두, 실행 중, 완료 또는 실패일 수 있습니다.
  * **엔터티** – 작업은 볼륨, 공유 또는 장치에 연관될 수 있습니다. 
  * **장치** – 작업이 시작된 장치의 이름입니다.
  * **시작 시간** – 작업이 시작된 시간입니다.
  * **진행률** – 실행 중인 작업의 완료율입니다. 완료된 작업의 경우 항상 100%여야 합니다.

작업 목록은 30초마다 새로 고쳐집니다.

## <a name="view-job-details"></a>작업 세부 정보 보기
다음 단계에 따라 작업 세부 정보를 봅니다.

#### <a name="to-view-job-details"></a>작업 세부 정보 보는 방법
1. **작업** 페이지에서 적절한 필터와 함께 쿼리를 실행하여 관심 있는 작업을 표시합니다. 완료되거나, 실행 중인 작업을 검색할 수 있습니다.
2. 작업 테이블 형식 목록에서 작업을 선택합니다.
3. 페이지 맨 아래에서 **세부 정보**를 클릭합니다.
4. **세부 정보** 대화 상자에서 상태, 세부 정보 및 시간 통계를 볼 수 있습니다. 다음 그림은 **백업 작업 세부 정보** 대화 상자의 예를 보여 줍니다.
   
    ![작업 세부 정보 페이지](./media/storsimple-ova-manage-jobs/ovajobs2.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a>가상 컴퓨터가 하이퍼바이저에서 일시 중지되는 경우 작업 실패
StorSimple 가상 배열에서 작업이 진행 중인 경우 장치(하이퍼바이저에 프로비전된 가상 컴퓨터)가 15분 넘게 일시 중지되면 작업이 실패합니다. 이는 StorSimple 가상 배열 시간과 Microsoft Azure 시간이 동기화 해제되기 때문입니다. 복원 작업 실패에 대한 예제는 다음 스크린샷에 나와 있습니다.

![복원 작업 실패](./media/storsimple-ova-manage-jobs/restorejobfailure.png)

이러한 실패는 백업, 복원, 업데이트 및 장애 조치(failover) 작업에 적용됩니다. 가상 컴퓨터가 Hyper-V에 프로비전된 경우 이 컴퓨터는 최종적으로 하이퍼바이저와 시간을 동기화합니다. 이러한 동기화 후 작업을 다시 시작할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
[로컬 웹 UI를 사용하여 StorSimple 가상 배열을 관리하는 방법을 알아봅니다.](storsimple-ova-web-ui-admin.md)




<!--HONumber=Nov16_HO3-->


