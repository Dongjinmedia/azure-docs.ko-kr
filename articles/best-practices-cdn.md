---
title: "CDN(콘텐츠 배달 네트워크) 지침 | Microsoft Docs"
description: "Azure에서 호스팅되는 고대역폭 콘텐츠를 제공하는 콘텐츠 배달 네트워크(CDN)에 대한 지침을 제공합니다."
services: cdn
documentationcenter: na
author: dragon119
manager: christb
editor: 
tags: 
ms.assetid: 57df0e00-d540-46e2-930e-f800c2301bf4
ms.service: best-practice
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: masashin
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: ea811d7315298132a45a8d1873da8a2bf5600c1c


---
# <a name="content-delivery-network-cdn-guidance"></a>콘텐츠 배달 네트워크(CDN) 지침
[!INCLUDE [pnp-header](../includes/guidance-pnp-header-include.md)]

## <a name="overview"></a>개요
Microsoft Azure 콘텐츠 배달 네트워크(CDN)는 개발자에게 Azure 또는 기타 위치에서 호스트되는 고대역폭 콘텐츠를 제공하기 위한 글로벌 솔루션을 제공합니다. CDN을 사용하여 Azure Blob 저장소, 웹 응용 프로그램, 가상 컴퓨터, 응용 프로그램 폴더 또는 기타 HTTP/HTTPS 위치에서 로드된 공개적으로 사용 가능한 개체를 캐시할 수 있습니다. 전략적 위치에 CDN 캐시를 보유하여 사용자에게 콘텐츠를 배달하기 위해 최대 대역폭을 제공할 수 있습니다. CDN은 일반적으로 이미지, 스타일 시트, 문서, 파일, 클라이언트쪽 스크립트 및 HTML 페이지와 같은 정적 콘텐츠를 제공하기 위해 사용됩니다.

또한 지정된 입력을 기반으로 하는 PDF 보고서 또는 그래프와 같은 동적 콘텐츠를 제공하기 위해 CDN을 캐시로 사용할 수 있습니다. 여러 사용자가 동일한 입력 값을 제공하는 경우 결과는 동일해야 합니다.

CDN을 사용하는 주요 이점은 대기 시간이 짧고 응용 프로그램이 호스팅되는 데이터 센터와 관련하여 지리적 위치에 관계 없이 사용자에게 콘텐츠를 빠르게 제공할 수 있다는 점입니다.  

![CDN 다이어그램](./media/best-practices-cdn/CDN.png)

CDN를 사용하면 콘텐츠에 액세스하고 콘텐츠를 전달하는 데 필요한 프로세스를 줄여주므로 응용 프로그램에 대한 부하를 줄입니다. 이렇게 부하가 감소하므로 특정 수준의 성능 및 가용성을 달성하는 데 필요한 처리 리소스를 줄여 호스팅 비용을 최소화할 뿐만 아니라 응용 프로그램의 성능과 확장성도 높일 수 있습니다.

## <a name="how-and-why-a-cdn-is-used"></a>CDN 사용 방법 및 사용 이유
일반적인 CDN의 용도는 다음과 같습니다.  

* 웹 사이트에서 종종 클라이언트 응용 프로그램에 대한 정적 리소스를 제공합니다. 이미지, 스타일 시트, 문서, 파일, 클라이언트쪽 스크립트, HTML 페이지, HTML 조각 또는 서버가 각 요청에 대해 수정할 필요가 없는 기타 콘텐츠 등이 이러한 리소스에 해당할 수 있습니다. 응용 프로그램이 런타임 시 항목을 만들고 CDN에서 사용할 수 있게 만들 수 있지만(현재 뉴스 헤드라인 목록 작성을 통해) 각 요청에 대해서는 그렇게 할 수 없습니다.
* 휴대폰 및 태블릿 컴퓨터와 같은 장치에 공용 정적 및 공유 콘텐츠를 전달합니다. 응용 프로그램 자체는 다양한 장치에서 실행되는 클라이언트에 API를 제공하는 웹 서비스입니다. 또한 클라이언트가 CDN 클라이언트 UI를 생성하는 데 사용할 정적 데이터 집합을 (웹 서비스를 통해) 제공할 수 있습니다. 예를 들어, CDN은 JSON 또는 XML 문서를 배포하는 데 사용할 수 있습니다.
* 어떠한 전용 계산 리소스 필요 없이 공용 정적 콘텐츠만으로 구성된 전체 웹 사이트를 클라이언트에 제공합니다.
* 주문 시 비디오 파일을 클라이언트에 스트리밍합니다. 비디오는 CDN 연결을 제공하는 전역적으로 위치한 데이터 센터에서 짧은 대기 시간 및 안정적인 연결 이점을 얻을 수 있습니다.
* 일반적으로 사용자, 특히 응용 프로그램을 호스팅하는 데이터 센터에서 멀리 떨어진 사용자의 환경을 개선합니다. 이러한 사용자는 대기 시간이 길어지는 문제가 생길 수 있습니다. 웹 응용 프로그램에 있는 콘텐츠의 총 크기에서 상당 부분이 정적으로, 여러 데이터 센터에 응용 프로그램을 배포하기 위한 요구 사항을 제거하면서 성능 및 전반적인 사용자 환경을 유지 관리하는 데 CDN 사용이 도움이 됩니다.
* IoT(사물 인터넷) 솔루션을 지원하는 응용 프로그램에 대한 부하 증가를 처리합니다. 응용 프로그램이 각 장치에 대해 브로드캐스트 메시지를 처리하고 펌웨어 업데이트 배포를 직접 관리해야 하는 경우 관련된 수많은 장치 및 어플라이언스의 해당 응용 프로그램에 과부하가 걸릴 수 있습니다.
* 응용 프로그램을 확장할 필요 없이 필요 시 최대치 및 급격한 증가에 대처하여 그에 따른 실행 비용의 증가를 방지합니다. 예를 들어 특정 라우터 모델과 같은 하드웨어 장치 또는 스마트 TV와 같은 소비자 장치에 대한 운영 체제 업데이트를 릴리스할 때는 짧은 기간 동안 수백만 명의 사용자 및 장치가 이를 다운로드하므로 최고치의 수요가 발생하게 됩니다.

다음 목록에서는 여러 지리적 위치에서 첫 번째 바이트까지의 중간 시간 값의 예를 보여줍니다. 대상 웹 역할은 Azure West US에 배포됩니다. CDN으로 인한 대폭적인 증가와 CDN 노드까지의 근접도 간에는 큰 상관관계가 있습니다. Azure CDN 노드 위치의 전체 목록은 [Azure CDN(Content Delivery Network) 노드 위치](cdn/cdn-pop-locations.md)를 참조하세요.

|  | 첫 번째 바이트(원점)까지 시간(ms) | 첫 번째(CDN)까지 시간(ms) | %CDN 시간 개선 |
| --- | --- | --- | --- |
| \*산호세, 캘리포니아 |47.5 |46.5 |2% |
| \*\*덜레스, 버지니아 |109 |40.5 |169% |
| 부에노스아이레스, AR |210 |151 |39% |
| \*런던, 영국 |195 |44 |343% |
| 상하이, 중국 |242 |206 |17% |
| \*싱가포르 |214 |74 |189% |
| \*도쿄, 일본 |163 |48 |204% |
| 서울, 한국 |190 |190 |0% |

\* 동일한 도시에 Azure CDN 노드가 있습니다.  
\*\* 인접한 도시에서는 Azure CDN 노드를 가집니다.  

## <a name="challenges"></a>과제
CDN을 사용하려고 계획할 때 고려해야 할 몇 가지 과제가 있습니다.  

* 배포를 참조하세요. CDN이 콘텐츠를 가져올 원본 위치 및 둘 이상의 저장소 시스템에 콘텐츠를 배포해야 하는지 여부(예: CDN과 대체 위치)를 결정해야 합니다 .
  
  응용 프로그램 배포 메커니즘은 ASPX 페이지 등과 같은 응용 프로그램 파일 배포 뿐만 아니라 정적 콘텐츠 및 리소스 배포를 위한 프로세스도 고려해야 합니다. 예를 들어 Azure Blob 저장소에 콘텐츠를 로드하는 별도의 단계를 구현해야 할 수 있습니다.
* **버전 관리 및 캐시 제어**. 정적 콘텐츠를 업데이트하고 새 버전을 배포하는 방법을 고려해야 합니다. 새 버전의 자산을 사용할 수 있게 되면 Azure 포털을 사용하여 CDN 콘텐츠를 [삭제](cdn/cdn-purge-endpoint.md) 할 수 있습니다. 이는 웹 브라우저에서 발생하는 것과 같이 클라이언트 쪽 캐싱을 관리하는 작업과 비슷한 문제입니다.
* **테스트**. 로컬로 또는 스테이징 환경에서 응용 프로그램을 개발하고 테스트를 수행할 때 CDN 설정의 로컬 테스트를 수행하는 것은 어려울 수 있습니다.
* **검색 엔진 최적화(SEO)**. CDN을 사용하는 경우 이미지 및 문서와 같은 콘텐츠는 다른 도메인에서 제공됩니다. 이 콘텐츠에 대한 SEO에 영향을 미칠 수 있습니다.
* **콘텐츠 보안**. Azure CDN 등의 많은 CDN 서비스가 현재 콘텐츠에 대해 모든 종류의 액세스 제어를 제공하는 것은 아닙니다.
* **클라이언트 보안**. 클라이언트가 CDN의 리소스에 대한 액세스를 허용하지 않는 환경에서 연결될 수 있습니다. 알려진 원본 집합만 액세스하도록 제한되거나, 페이지 원본 이외의 위치에서는 리소스를 로드할 수 없는 제한된 보안 환경일 수 있습니다. 이러한 경우를 처리하는 데 대체 구현이 필요합니다.
* **복원력**. CDN은 응용 프로그램에 대한 단일 오류 지점이 될 수 있습니다. 가용성 SLA가 BLOB 저장소(콘텐츠를 직접 제공하는 데 사용 가능)보다 더 낮기 때문에 중요한 콘텐츠에 대해 대체 메커니즘을 구현하는 것을 고려해야 할 수 있습니다.
  
  Azure Portal에서 [실시간](cdn/cdn-real-time-stats.md)으로 [집계 보고서](cdn/cdn-analyze-usage-patterns.md)를 통해 CDN 콘텐츠 가용성, 대역폭, 전송된 데이터, 적중 항목, 캐시 적중률 및 캐시 메트릭을 모니터링할 수 있습니다.

다음과 같은 시나리오에서는 CDN이 그다지 유용하지 않을 수 있습니다.  

* 콘텐츠에 적중률이 낮으면 유효할 동안 몇 번만 액세스될 수 있습니다.(TTL(Time-To-Live) 설정에 따라 결정됨) 항목을 처음 다운로드하면 원본에서 CDN까지, 그리고 CDN에서 고객까지 두 개의 트래잭션 비용이 발생합니다.
* 대기업 또는 공급망 에코시스템 등과 같이 데이터가 비공개인 경우입니다.

## <a name="general-guidelines-and-good-practices"></a>일반적인 지침과 모범 사례
CDN 사용은 응용 프로그램에 대한 부하를 최소화하고 가용성과 성능을 극대화하는 좋은 방법입니다. 따라서 응용 프로그램이 사용하는 모든 적절한 콘텐츠 및 리소스에서 이 전략을 채택할지를 고려해야 합니다. CDN을 사용하는 전략을 설계할 때 다음 섹션에 있는 요소를 고려합니다.  

### <a name="origin"></a>원본
CDN을 통해 콘텐츠를 배포하려면 CDN 서비스가 콘텐츠에 액세스하고 콘텐츠를 캐시하는 데 사용하는 HTTP 및/또는 HTTPS 끝점을 지정해야 합니다.

끝점은 CDN을 통해 전달하려는 정적 콘텐츠를 보유하는 Azure Blob 저장소 컨테이너를 지정할 수 있습니다. 컨테이너는 공용으로 표시되어야 합니다. 공용 읽기 액세스 권한이 있는 공용 컨테이너의 BLOB만 CDN을 통해 사용할 수 있습니다.

끝점은 응용 프로그램의 계산 계층(예: 웹 역할 또는 가상 컴퓨터) 중 하나의 루트에 **cdn** 이라는 폴더를 지정할 수 있습니다. ASPX 페이지 등의 동적 리소스를 포함한 리소스에 대한 요청의 결과가 CDN에 캐시됩니다. 캐시 시간은 최소 300초입니다. 시간이 짧아지면 콘텐츠가 CDN에 배포되지 않도록 방지합니다(자세한 내용은 *캐시 제어* 제목 참조).

Azure 웹앱을 사용하는 경우 CDN 인스턴스를 만들 때 사이트를 선택하면 해당 사이트의 루트 폴더로 끝점이 설정됩니다. 사이트의 모든 콘텐츠는 CDN을 통해 사용할 수 있습니다.

대부분의 경우 응용 프로그램의 계산 계층 중 하나에 있는 폴더의 CDN 끝점을 가리키면 더 많은 유연성과 제어 기능이 제공됩니다. 예를 들어, 현재와 미래의 라우팅 요구 사항을 쉽게 관리할 수 있게 해주며 축소판 이미지와 같은 정적 콘텐츠를 동적으로 생성할 수 있습니다.

ASPX 페이지와 같은 동적 원본에서 콘텐츠를 제공할 때 캐시에서 개체를 구별하기 위해 [쿼리 문자열](cdn/cdn-query-string.md)을 사용할 수 있습니다. 그러나 이 동작은 CDN 끝점을 지정할 때 Azure 포털에서 설정을 통해 비활성화할 수 있습니다. BLOB 저장소에서 콘텐츠를 제공하는 경우 쿼리 문자열은 문자열 리터럴로 처리됩니다. 따라서 이름이 같지만 쿼리 문자열이 서로 다른 두 항목은 CDN에 개별 항목으로 저장됩니다.

스크립트 및 기타 콘텐츠 등의 리소스에 대한 URL 다시 쓰기를 활용하면 CDN 원본 폴더에 파일이 이동되지 않도록 할 수 있습니다.

Azure 저장소 BLOB을 사용하여 CDN에 사용할 콘텐츠를 보관하면 BLOB에 있는 리소스의 URL은 컨테이너 및 BLOB 이름에 대해 대/소문자를 구분합니다.

사용자 지정 원본 또는 Azure 웹앱을 사용하는 경우 리소스에 대한 링크에서 CDN 인스턴스의 경로를 지정합니다. 예를 들어, 다음은 CDN을 통해 제공될 사이트의 **Images** 폴더에 있는 이미지 파일을 지정합니다.

```XML
<img src="http://[your-cdn-endpoint].azureedge.net/Images/image.jpg" />
```

### <a name="deployment"></a>배포
정적 콘텐츠가 응용 프로그램 배포 패키지 또는 프로세스에 포함되지 않은 경우 응용 프로그램과 별도로 프로비전 및 배포해야 할 수 있습니다. 따라서 이 작업이 응용 프로그램 구성 요소와 정적 리소스 콘텐츠를 관리하는 데 사용할 버전 관리 방법에 어떤 영향을 주게 될지 고려해야 합니다.

스크립트 및 CSS 파일에 대한 묶음(파일 하나에 여러 파일 결합) 및 축소(공백, 줄바꿈 문자, 설명 및 기타 문자 등의 불필요한 문자 제거)를 처리하는 방법을 고려해야 합니다. 클라이언트에서 로드 시간을 줄일 수 있으며 CDN을 통한 콘텐츠 제공과 호환되는 일반적으로 사용되는 기법입니다. 자세한 내용은 [묶음 및 축소](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)를 참조하세요.

추가적인 위치에 콘텐츠를 배포해야 하는 경우이 작업이 배포 프로세스의 추가 단계가 됩니다. 일정한 간격으로 또는 이벤트에 대한 응답으로 응용 프로그램이 CDN에 대해 콘텐츠를 업데이트하는 경우 CDN의 끝점을 비롯한 추가적인 위치에 업데이트된 콘텐츠를 저장해야 합니다.

Visual Studio의 로컬 Azure 에뮬레이터에 있는 응용 프로그램에는 CDN 끝점을 설정할 수 없습니다. 이 제한은 단위 테스트, 기능 테스트 및 최종 배포 전 테스트에 적용됩니다. 따라서 대체 메커니즘을 구현하여 이를 허용해야 합니다. 예를 들어 사용자 지정 응용 프로그램 또는 유틸리티를 사용하여 CDN에 콘텐츠를 미리 배포하고 캐시된 기간 동안 테스트를 수행할 수 있습니다. 또는 컴파일 지시문이나 전역 상수를 사용하여 응용 프로그램이 리소스를 로드하는 위치를 제어합니다. 예를 들어, 디버그 모드에서 실행 중일 때는 클라이언트 쪽 스크립트 번들 또는 로컬 폴더의 기타 콘텐츠 등과 같은 로컬 리소스를 로드하고 릴리스 모드에서 실행 중일 때는 CDN을 사용할 수 있습니다.

CDN이 지원하기를 원하는 압축 방식을 고려합니다.

* 원본 서버에서 [압축을 사용하도록 설정](cdn/cdn-improve-performance.md)할 수 있습니다. 이 경우 CDN이 기본적으로 압축을 지원하며 클라이언트에 zip 또는 gzip 형식으로 압축된 콘텐츠를 전달합니다. 응용 프로그램 폴더를 CDN 끝점으로 사용할 때 서버는 자동으로 웹 브라우저 또는 다른 유형의 클라이언트에 직접 제공할 때와 동일한 방식으로 일부 콘텐츠를 압축할 수 있습니다. 형식은 클라이언트에서 보낸 요청의 **Accept-Encoding** 헤더 값에 따라 다릅니다. Azure에서 기본 메커니즘은 CPU 사용률이 50% 미만일 때 자동으로 콘텐츠를 압축하는 것입니다. 클라우드 서비스를 사용하여 응용 프로그램을 호스트하는 경우 설정을 변경하면 IIS에서 동적 출력의 압축을 사용하는 시작 작업을 사용해야 할 수 있습니다. 자세한 내용은 [웹 역할을 통해 Microsoft Azure CDN에서 gzip 압축 사용](http://blogs.msdn.com/b/avkashchauhan/archive/2012/03/05/enableing-gzip-compression-with-windows-azure-cdn-through-web-role.aspx)을 참조하세요.
* CDN 에지 서버에서 직접 압축을 사용하도록 설정할 수 있습니다. 이 경우 CDN이 파일을 압축하여 최종 사용자에게 제공합니다. 자세한 내용은 [Azure CDN 압축](cdn/cdn-improve-performance.md)을 참조하세요.

### <a name="routing-and-versioning"></a>라우팅 및 버전 관리
다양한 시간에 여러 CDN 인스턴스를 사용해야 합니다. 예를 들어 응용 프로그램의 새 버전을 배포할 때 새 CDN을 사용하고 이전 버전에 대한 이전 CDN(이전 형식의 콘텐츠 포함)를 유지하려 할 수 있습니다. Azure BLOB 저장소를 콘텐츠 원본으로 사용하는 경우 간단하게 별도의 저장소 계정 또는 컨테이너를 만들고 CDN 끝점이 이를 가리키도록 할 수 있습니다. 응용 프로그램 내에서 *cdn* 루트 폴더를 CDN 끝점으로 사용하는 경우 URL 다시 쓰기 기술을 사용하여 다른 폴더로 요청을 지정할 수 있습니다.

Azure Blob 저장소에서 콘텐츠를 검색할 때 쿼리 문자열이 리소스 이름(Blob 이름)의 일부이므로 CDN의 리소스에 대한 링크에서 응용 프로그램의 서로 다른 버전을 표시하기 위해 쿼리 문자열을 사용하지 않습니다. 이 방법은 클라이언트가 리소스를 캐시하는 방법에도 영향을 줄 수 있습니다.

CDN에 이전 리소스가 캐시된 경우에는 응용 프로그램을 업데이트할 때 정적 콘텐츠의 새 버전을 배포하는 것이 어려울 수 있습니다. 자세한 내용은 *캐시 제어* 섹션을 참조하세요.

국가별로 CDN 콘텐츠 액세스를 제한하는 것이 좋습니다. Azure CDN을 사용하면 원본의 국가에 따라 요청을 필터링하고 전달되는 내용을 제한할 수 있습니다. 자세한 내용은 [국가별로 콘텐츠에 대한 액세스 제한](cdn/cdn-restrict-access-by-country.md)을 참조하세요.

### <a name="cache-control"></a>캐시 제어
시스템 내에서 캐싱을 관리하는 방법을 고려합니다. 예를 들어, 폴더를 CDN 원점으로 사용하는 경우 콘텐츠를 생성하는 페이지의 캐시 가능성 및 특정 폴더의 모든 리소스에 대해 콘텐츠 만료 시간을 지정할 수 있습니다. 표준 HTTP 헤더를 사용하여 CDN 및 클라이언트에 대한 캐시 속성을 지정할 수도 있습니다. 서버와 클라이언트에서 이미 캐싱을 관리 중이어도 CDN을 사용하면 콘텐츠 캐시 방법과 위치를 더 잘 파악하는 데 도움이 됩니다.

개체를 CDN에서 사용할 수 없도록 하려면 원본(Blob 컨테이너 또는 응용 프로그램 *cdn* 루트 폴더)에서 삭제하거나 CDN 끝점을 제거 또는 삭제하거나, Blob 저장소인 경우 컨테이너 또는 Blob를 비공개로 만들 수 있습니다. 그러나 항목은 해당 TTL(Time-to-Live)이 만료된 경우에만 CDN에서 제거됩니다. 캐시 만료 시간을 지정하지 않으면(예: Blob 저장소에서 콘텐츠를 로드할 때) 최대 7일 동안 CDN에 캐시됩니다.  수동으로 [CDN 끝점을 삭제](cdn/cdn-purge-endpoint.md)할 수도 있습니다.

웹 응용 프로그램에서 web.config 파일의 *system.webServer/staticContent* 섹션에 있는 *clientCache* 요소를 사용하여 모든 콘텐츠에 대한 캐싱 및 만료를 설정할 수 있습니다. 폴더에 web.config 파일을 배치하면 해당 폴더의 파일 및 모든 하위 폴더의 파일에 적용됩니다.

동적으로 CDN에 대한 콘텐츠를 만드는 경우(예를 들어 응용 프로그램 코드에서) 각 페이지에서 *Cache.SetExpires* 속성을 지정하도록 합니다. CDN은 *공용*의 기본 캐시 가능성 설정을 사용하는 페이지의 출력을 캐시하지 않습니다.  콘텐츠가 취소되지 않고 아주 짧은 간격으로 응용 프로그램에서 다시 로드되지 않도록 캐시 만료 기간을 적절한 값으로 설정합니다.  

### <a name="security"></a>보안
CDN은 CDN에서 제공하는 인증서를 사용하여 HTTPS(SSL)를 통해 콘텐츠를 제공할 수 있지만 HTTP를 통해서도 가능합니다. CDN의 항목에 대한 HTTP 액세스를 차단할 수 없습니다. HTTPS를 통해 로드된 페이지에 표시되는 정적 콘텐츠(예: 장바구니)를 요청하려면 혼합 콘텐츠에 대한 브라우저 경고를 방지하기 위해 HTTPS를 사용해야 할 수 있습니다.

Azure CDN은 액세스 제어를 위한 기능을 제공하지 않아서 콘텐츠에 대한 액세스를 보호합니다. CDN에서 공유 액세스 서명(SAS)을 사용할 수 없습니다.

CDN을 사용하여 클라이언트쪽 스크립트를 제공하는 경우 이러한 스크립트에서 *XMLHttpRequest* 호출을 사용하여 다른 도메인에 있는 데이터, 이미지 또는 글꼴 등과 같은 다른 리소스에 대한 HTTP 요청을 수행하면 문제가 발생할 수 있습니다. 적절한 응답 헤더를 설정하도록 웹 서버를 구성하지 않으면 많은 웹 브라우저에서 크로스-원본 자원 공유(CORS)를 차단합니다. CORS를 지원하도록 CDN을 구성할 수 있습니다.

* 콘텐츠를 제공하고 있는 원본이 Azure Blob 저장소인 경우 *CorsRule* 을 서비스 속성에 추가할 수 있습니다. 규칙에서는 CORS 요청에 허용되는 원본, GET 등의 허용되는 메서드 및 규칙의 최대 보존 기간(초) (클라이언트가 원본 콘텐츠를 로드한 후 연결된 리소스를 요청해야 하는 기간)을 지정할 수 있습니다. 자세한 내용은 [Azure 저장소 서비스에 대한 크로스-원본 자원 공유(CORS) 지원](http://msdn.microsoft.com/library/azure/dn535601.aspx)을 참조하세요.
* 콘텐츠를 제공하고 있는 원본이 *cdn* 루트 폴더 등과 같이 응용 프로그램 내의 폴더인 경우, 응용 프로그램 구성 파일에서 *Access-Control-Allow-Origin* 헤더를 설정하는 아웃바운드 규칙을 구성할 수 있습니다. 다시 쓰기 규칙 사용에 대한 자세한 내용은 [URL 다시 쓰기 모듈](http://www.iis.net/learn/extensions/url-rewrite-module)을 참조하세요.

### <a name="custom-domains"></a>사용자 지정 도메인
Azure CDN을 사용하면 [사용자 지정 도메인 이름](cdn/cdn-map-content-to-custom-domain.md) 을 지정하고 그 이름을 사용하여 CDN을 통해 리소스에 액세스할 수 있습니다. 또한 DNS에서 *CNAME* 레코드를 사용하여 사용자 지정 하위 도메인 이름을 설정할 수도 있습니다. 이 방법을 사용하면 추가적인 계층을 추상화 및 제어할 수 있습니다.

*CNAME*을 사용하는 경우 CDN이 자체 단일 SSL 인증서를 사용하기 때문에 SSL을 사용할 수 없고 이 인증서는 사용자 지정 도메인/하위 도메인 이름이 일치하지 않습니다.

### <a name="cdn-fallback"></a>CDN 대체
응용 프로그램이 CDN의 오류 또는 일시적인 중단에 대처하는 방법을 고려해야 합니다. 클라이언트 응용 프로그램은 이전 요청 중에 로컬로 캐시(클라이언트에)된 리소스의 복사본을 사용하거나, CDN을 사용할 수 없는 경우 오류를 감지하고 대신 원본(리소스가 있는 응용 프로그램 폴더 또는 Azure Blob 컨테이너)의 리소스를 요청하는 코드를 포함할 수 있습니다.

### <a name="search-engine-optimisation"></a>검색 엔진 최적화
SEO가 응용 프로그램에서 중요하게 여겨지는 경우 다음 작업을 수행합니다.

* 각 페이지 또는 리소스에 *Rel* canonical 헤더를 포함합니다.
* *CNAME* 하위 도메인 레코드를 사용하고 이 이름을 사용하여 리소스에 액세스합니다.
* 응용 프로그램 자체의 국가 또는 지역과 다른 CDN의 IP 주소가 미치는 영향을 고려해야 합니다.
* Azure BLOB 저장소를 원본으로 사용하는 경우 CDN의 리소스를 응용 프로그램 폴더에 있는 것과 동일한 파일 구조로 유지합니다.

### <a name="monitoring-and-logging"></a>모니터링 및 로깅
CDN을 응용 프로그램 모니터링 전략의 일부로 포함시켜 오류 또는 대기 시간 연장 문제의 발생을 감지 및 측정합니다.  모니터링은 Azure 포털 사이트에 있는 CDN 프로필 관리자에서 사용할 수 있습니다.

CDN에 로깅을 사용하고 이 로그를 일상적인 작업의 일부로 모니터링합니다.

사용 패턴에 대한 CDN 트래픽을 분석하는 것이 좋습니다. Azure 포털은 다음을 모니터링할 수 있는 도구를 제공합니다.

* 대역폭,
* 전송된 데이터,
* 적중 횟수(상태 코드),
* 캐시 상태,
* 캐시 적중률 및
* IPV4/IPV6 요청 비율

자세한 내용은 [CDN 사용 패턴 분석](cdn/cdn-analyze-usage-patterns.md)을 참조하세요.

### <a name="cost-implications"></a>비용 영향
CDN에서의 아웃바운드 데이터 전송 요금이 청구됩니다.  또한 Blob 저장소를 사용하여 자산을 호스트하는 경우 CDN이 응용 프로그램에서 데이터를 로드할 때 저장소 트랜잭션에 대한 요금이 청구됩니다. 콘텐츠의 유효성을 보장할 수 있는 현실적인 캐시 만료 기간을 설정해야 하지만 기간이 너무 짧아서 응용 프로그램 또는 BLOB 저장소에서 CDN으로 콘텐츠를 반복적으로 다시 로드하지 않도록 해야 합니다.

거의 다운로드하지 않는 항목은 서버 부하가 눈에 띄게 감소되지 않으면서 두 개의 트랜잭션 비용이 발생하게 됩니다.

### <a name="bundling-and-minification"></a>묶음 및 축소
묶음 및 축소를 사용하여 CDN에 저장된 JavaScript 코드 및 HTML 페이지와 같은 리소스의 크기를 줄입니다. 이 전략은 클라이언트에 이러한 항목을 다운로드하는 데 걸리는 시간을 줄이는 데 도움이 됩니다.

묶음 및 축소는 ASP.NET을 통해 처리할 수 있습니다. MVC 프로젝트에서 *BundleConfig.cs*에 번들을 정의합니다. 축소된 스크립트 번들에 대한 참조는 일반적으로 뷰 클래스의 코드에 있는 *Script.Render* 메서드를 호출하여 작성합니다. 이 참조에는 번들의 콘텐츠를 바탕으로 하는 해시가 포함된 쿼리 문자열이 들어 있습니다. 번들 콘텐츠가 변경되면 생성된 해시도 변경됩니다.  

기본적으로 Azure CDN 인스턴스는 *쿼리 문자열 상태* 설정이 비활성화되어 있습니다. 업데이트된 스크립트 번들을 CDN에서 적절히 처리하도록 하기 위해서는 CDN 인스턴스에 대해 *쿼리 문자열 상태* 설정을 사용해야 합니다. 설정이 적용되기 전에 한 시간 이상이 걸릴 수 있습니다.

## <a name="example-code"></a>예제 코드
이 섹션에는 CDN을 사용하는 데 필요한 코드 및 기술에 대한 몇 가지 예가 나와 있습니다.  

### <a name="url-rewriting"></a>URL 다시 쓰기
아래에서는 클라우드 서비스 호스팅 응용 프로그램의 루트에 있는 Web.config 파일 외에 CDN을 사용할 때 [URL 다시 쓰기](https://technet.microsoft.com/library/ee215194.aspx) 를 수행하는 방법을 보여줍니다. 캐시된 콘텐츠에 대한 CDN의 요청은 리소스 유형(예: 스크립트 및 이미지)에 따라 응용 프로그램 루트 내의 특정 폴더로 리디렉션됩니다.  

```XML
<system.webServer>
  ...
  <rewrite>
    <rules>
      <rule name="VersionedResource" stopProcessing="false">
        <match url="(.*)_v(.*)\.(.*)" ignoreCase="true" />
        <action type="Rewrite" url="{R:1}.{R:3}" appendQueryString="true" />
      </rule>
      <rule name="CdnImages" stopProcessing="true">
        <match url="cdn/Images/(.*)" ignoreCase="true" />
        <action type="Rewrite" url="/Images/{R:1}" appendQueryString="true" />
      </rule>
      <rule name="CdnContent" stopProcessing="true">
        <match url="cdn/Content/(.*)" ignoreCase="true" />
        <action type="Rewrite" url="/Content/{R:1}" appendQueryString="true" />
      </rule>
      <rule name="CdnScript" stopProcessing="true">
        <match url="cdn/Scripts/(.*)" ignoreCase="true" />
        <action type="Rewrite" url="/Scripts/{R:1}" appendQueryString="true" />
      </rule>
      <rule name="CdnScriptBundles" stopProcessing="true">
        <match url="cdn/bundles/(.*)" ignoreCase="true" />
        <action type="Rewrite" url="/bundles/{R:1}" appendQueryString="true" />
      </rule>
    </rules>
  </rewrite>
  ...
</system.webServer>
```

다시 쓰기 규칙은 다음 리디렉션을 수행합니다.

* 첫 번째 규칙을 사용하면 리소스의 파일 이름에 버전을 포함할 수 있으며, 그런 다음 이 이름은 무시됩니다. 예를 들어 *Filename_v123.jpg*를 *Filename.jpg*로 다시 씁니다.
* 다음 4개의 규칙에서는 웹 역할의 루트에 있는 *cdn** 폴더에 리소스를 저장하지 않을 경우 요청을 리디렉션하는 방법을 보여줍니다. 규칙이 *cdn/Images*, *cdn/Content*, *cdn/Scripts*, *cdn/bundles* URL을 웹 역할의 해당 루트 폴더에 매핑합니다.

URL 다시 쓰기를 사용하면 리소스 묶음에 대한 변경을 수행해야 합니다.   

## <a name="more-information"></a>자세한 정보
* [Azure CDN](https://azure.microsoft.com/services/cdn/)
* [Azure 콘텐츠 배달 네트워크(CDN) 설명서](https://azure.microsoft.com/documentation/services/cdn/)
* [Azure CDN 사용](cdn/cdn-create-new-endpoint.md)
* [Azure CDN과 클라우드 서비스 통합](cdn/cdn-cloud-service-with-cdn.md)
* [Microsoft Azure 콘텐츠 배달 네트워크 모범 사례](https://azure.microsoft.com/blog/2011/03/18/best-practices-for-the-windows-azure-content-delivery-network/)




<!--HONumber=Nov16_HO3-->


