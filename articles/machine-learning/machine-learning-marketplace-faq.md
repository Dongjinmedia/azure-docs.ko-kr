---
title: "FAQ: Azure Marketplace에서 Machine Learning 앱 서비스 게시 및 사용 | Microsoft Docs"
description: "질문과 대답"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2016
ms.author: bharaths
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: f8ae758a406dfed48968531ae20a9bbd2383db92


---
# <a name="publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a>Azure 마켓플레이스에서 기계 학습 앱 게시 및 사용: FAQ
## <a name="questions-about-consuming-from-marketplace"></a>마켓플레이스에서의 사용 관련 질문
**1. 웹 서비스에 입력한 후에 다음과 같은 오류 메시지가 표시되는 이유는 무엇인가요?**

**요청으로 인해 백 엔드 시간 초과 또는 백 엔드 오류가 발생했습니다. 해당 팀에서 이 문제를 조사하고 있습니다. 불편을 드려 죄송합니다. (500)**

입력 매개 변수가 특정 웹 서비스에 필요한 형식을 준수하지 않은 것일 수 있습니다. 이 웹 서비스의 입력 매개 변수에 대한 올바른 형식 및 제한을 찾으려면 해당 설명서 링크를 참조하세요.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. “이 데이터 집합 탐색” 페이지에 표시된 웹 서비스의 API 링크를 복사하여 다른 브라우저 창에 붙여 넣는 경우 결과에 액세스하는 데 사용해야 하는 자격 증명은 무엇이며, 결과를 보는 방법은 무엇인가요?**

마켓플레이스 계정을 사용자 이름으로 사용하고 기본 계정 키를 암호로 사용해야 합니다. 기본 계정 키는 **이 데이터 집합 탐색** 페이지의 웹 서비스 설명에서 찾을 수 있습니다(**표시** 단추 클릭). 사용 중인 브라우저에 따라 결과가 브라우저에 표시되거나 다운로드할 수 있습니다.

**3. 웹 서비스의 “이 데이터 집합 탐색" 페이지에 입력한 후에 다음과 같은 오류 메시지가 표시되는 이유는 무엇인가요?** 

**요청을 처리하는 동안 예기치 않은 오류가 발생했습니다. 나중에 다시 시도하세요.**

마켓플레이스 **이 데이터 집합 탐색** 페이지에서 웹 서비스를 사용할 때 웹 서비스의 하나 이상의 입력 매개 변수가 길이 제한을 초과했을 수 있습니다. HTTP POST 메서드를 사용하여 좀 더 길게 입력하여 서비스를 호출할 수 있습니다. 예제를 보려면 [기계 학습에서 R을 사용하고 마켓플레이스에 게시되는 샘플 솔루션](machine-learning-r-csharp-web-service-examples.md)을 참조하세요.

**4. Azure 클래식 포털의 스토어에서 "API 탐색기" 탭에 아무 내용도 표시되지 않는 이유는 무엇인가요?** 

이것은 Azure 클래식 포털 마켓플레이스의 알려진 문제입니다. 이 문제 해결을 위한 작업이 진행되고 있습니다. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>마켓플레이스에 있는 Azure 기계 학습에서의 게시에 대한 질문
**1. 내 웹 서비스에 대해 내 로고 또는 이미지 트랜잭션 수가 새로 고쳐지지 않는 이유는 무엇인가요?** 

로고 및 이미지는 게시 포털에 캐싱되며 포털에서 새 로고 또는 이미지가 업데이트되기까지 최대 10일이 걸릴 수 있습니다.

**2. 마켓플레이스에서 내 웹 서비스의 "세부 정보" 탭에 오류 메시지가 표시되는 이유는 무엇인가요?**

서비스 세부 정보를 확인하기 위해 Azure 기계 학습에 연결할 때 알려진 마켓플레이스 문제가 있습니다. 이 문제 해결을 위한 작업이 진행되고 있습니다.

**3. Azure 기계 학습 웹 서비스의 R 샘플 코드가 마켓플레이스에서의 웹 서비스 사용에 대해 작동하지 않는 이유는 무엇인가요?**

Azure 기계 학습 웹 서비스에 직접 연결하는 경우와 마켓플레이스를 통해 이러한 웹 서비스에 연결하는 경우의 인증 시스템이 서로 다릅니다. 마켓플레이스의 서비스는 OData 서비스이며 GET 또는 POST 메서드를 사용하여 호출할 수 있습니다. 

**4. 내 웹 서비스 제품의 지원 링크가 일부 내 제품에 대해 올바르게 업데이트되지 않는 이유는 무엇인가요?**

지원 링크는 제품당 전역이 아니라 게시자당 전역입니다. 

**5. 마켓플레이스에서 일괄 처리 입력 모드를 통해 웹 서비스를 게시하는 방법은 무엇인가요?**

현재 마켓플레이스 웹 서비스에서는 일괄 처리 입력 모드가 지원되지 않습니다.

**6. 데이터 게시자가 되는 것에 대한 질문이 있거나 게시 중에 문제가 있는 경우 도움을 얻기 위해 문의해야 하는 사람은 누구인가요?**

자세한 내용은 <mailto:datamarketbd@microsoft.com>에서 Azure Marketplace 팀에 문의하세요.




<!--HONumber=Nov16_HO3-->


