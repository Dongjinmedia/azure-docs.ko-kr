---
title: "Azure Storage Blob과 Azure Data Lake Store 비교 | Microsoft 문서"
description: "Azure Storage Blob과 Azure Data Lake Store 비교"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b199525b-84de-4f79-9eb6-69a613b8b217
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/28/2016
ms.author: nitinme
translationtype: Human Translation
ms.sourcegitcommit: 267b281c33049e65e82a5e5b2453ff1a80983453
ms.openlocfilehash: 744e5a093cb99463224d42a69711f41f6132a2ee


---
# <a name="comparing-azure-data-lake-store-and-azure-blob-storage"></a>Azure Data Lake Store와 Azure Blob 저장소 비교
이 문서의 테이블은 빅 데이터 처리의 일부 주요 측면을 따라 Azure Data Lake Store와 Azure Blob 저장소 간의 차이점을 요약합니다. Azure Blob 저장소는 다양한 저장소 시나리오를 위해 설계된 확장성 있는 범용 개체 저장소입니다. Azure Data Lake Store는 빅 데이터 분석 워크로드에 대해 최적화된 하이퍼 스케일 리포지토리입니다.

|  | Azure Data Lake Store | 데이터 이동 |
| --- | --- | --- |
| 목적 |빅 데이터 분석 워크로드에 대해 최적화된 저장소 |다양한 저장소 시나리오에 대한 범용 개체 저장소 |
| 사용 사례 |배치, 대화형, 스트리밍 분석 및 로그 파일, IoT 데이터, 클릭 스트림, 대형 데이터 집합 등과 같은 기계 학습 데이터 |응용 프로그램 백 엔드, 백업 데이터, 스트리밍용 미디어 저장소 및 범용 데이터 등과 같은 모든 종류의 텍스트 또는 이진 데이터 |
| 주요 개념 |Data Lake Store 계정은 폴더를 포함하며, 이 폴더는 파일로 저장된 데이터를 포함함 |저장소 계정은 컨테이너를 가지며, 이 컨테이너는 blob 형식의 데이터를 가짐 |
| 구조 |계층적 파일 시스템 |단일 구조 네임스페이스를 가진 개체 저장소 |
| API |HTTPS를 통한 REST API |HTTP/HTTPS를 통한 REST API |
| 서버 쪽 API |[WebHDFS 호환 REST API](https://msdn.microsoft.com/library/azure/mt693424.aspx) |[Azure Blob 저장소 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx) |
| Hadoop 파일 시스템 클라이언트 |예 |예 |
| 데이터 작업 - 인증 | [Azure Active Directory ID](../active-directory/active-directory-authentication-scenarios.md) |공유 비밀 기반 - [계정 액세스 키](../storage/storage-create-storage-account.md#manage-your-storage-account) 및 [공유 액세스 서명 키](../storage/storage-dotnet-shared-access-signature-part-1.md) |
| 데이터 작업 - 인증 프로토콜 |OAuth 2.0. 호출은 Azure Active Directory가 발급한 유효한 JWT(JSON Web Token)를 포함해야 함 |해시 기반 메시지 인증 코드(HMAC)입니다. 호출은 HTTP 요청 일부를 통해 Base64 인코딩된 SHA-256 해시를 포함해야 합니다. |
| 데이터 작업 - 인증 |POSIX 액세스 제어 목록(ACL)입니다.  Azure Active Directory ID에 따른 ACL은 파일 및 폴더 수준에서 설정할 수 있습니다. |계정 수준 인증의 경우 - [계정 액세스 키](../storage/storage-create-storage-account.md#manage-your-storage-account) 사용.<br>계정, 컨테이너 또는 Blob 권한 부여의 경우 - [공유 액세스 서명 키](../storage/storage-dotnet-shared-access-signature-part-1.md) 사용. |
| 데이터 작업 - 감사 |사용 가능. 자세한 내용은 [여기](data-lake-store-diagnostic-logs.md) 를 참조하세요. |사용 가능 |
| 미사용 암호화 데이터 |투명한, 서버 쪽(출시 예정)<ul><li>서비스 관리 키 사용</li><li>Azure KeyVault의 고객 관리 키 사용</li></ul> |<ul><li>투명한, 서버 쪽</li> <ul><li>서비스 관리 키 사용</li><li>Azure KeyVault의 고객 관리 키 사용(출시 예정)</li></ul><li>클라이언트 쪽 암호화</li></ul> |
| 관리 작업(예: 계정 만들기) |[역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) ) |[역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) ) |
| 개발자 SDK |.NET, Java, Node.js |.NET, Java, Python, Node.js, c + +, Ruby |
| 분석 워크로드 성능 |병렬 분석 워크로드에 대해 최적화된 성능입니다. 높은 처리량 및 IOPS. |분석 워크로드에 대해 최적화되지 않음 |
| 크기 한도 |계정 크기, 파일 크기 또는 파일 수에 한도가 없음 |문서화된 특정 한도 [여기](../azure-subscription-service-limits.md#storage-limits) |
| 지리적 중복 |로컬 중복(Azure 하위 지역에 있는 데이터의 여러 복사본) |로컬 중복(LRS), 전역 중복(GRS), 읽기 액세스 전역 중복(RA-GRS). 자세한 내용은 [여기](../storage/storage-redundancy.md) 참조 |
| 서비스 상태 |일반 공급 |일반 공급 |
| 국가별 가용성 |자세한 내용은 [여기](https://azure.microsoft.com/regions/#services) |자세한 내용은 [여기](https://azure.microsoft.com/regions/#services) |
| 가격 |자세한 내용은 [가격 책정](https://azure.microsoft.com/pricing/details/data-lake-store/) |자세한 내용은 [가격 책정](https://azure.microsoft.com/pricing/details/storage/) |

### <a name="next-steps"></a>다음 단계
* [Azure Data Lake Store 개요](data-lake-store-overview.md)
* [Data Lake 저장소 시작](data-lake-store-get-started-portal.md)




<!--HONumber=Nov16_HO5-->


