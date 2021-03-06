---
title: "Azure SQL Database Azure 사례 연구 - Snelstart | Microsoft Docs"
description: "어떻게 SnelStart가 Azure를 사용하여 매월 1,000개의 새 Azure SQL 데이터베이스 규모로 비즈니스 서비스를 빠르게 확장했는지 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: app development case study; app development
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/08/2016
ms.author: carlrab
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: 66360bc0a8618d250cc07e3e806af6c9a157afaf


---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Azure를 사용하여 SnelStart는 매월 1,000개의 새 Azure SQL 데이터베이스 규모로 비즈니스 서비스를 빠르게 확장했습니다.
![SnelStart 로고](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart는 네덜란드에서 인기리에 사용되는 SMB(중소기업)을 위한 재무 및 비즈니스 관리 소프트웨어를 제작합니다. 이 회사의 55,000여 고객은 IT 직원 35명을 포함하여 110명의 직원에게 서비스를 받습니다. SnelStart는 데스크톱 소프트웨어에서 Azure에서 구축되는 SaaS(software-as-a-service) 제품으로 전환하면서, 기본 제공 서비스를 활용하고, C#의 친숙한 환경을 사용하여 관리를 자동화하고, 탄력적 데이터베이스 풀을 통해 비즈니스의 과도한 프로비전 또는 부족한 프로비전 없이 성능 및 확장성을 최적화했습니다. SnelStart는 Azure를 사용하여 온-프레미스와 클라우드 간에 고객을 유연하게 이동할 수 있습니다.

> [!비디오 https://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-the-desktop-to-the-cloud"></a>SnelStart가 데스크톱에서 클라우드로 서비스를 확장한 이유
> "Azure를 사용하게 되면서 소프트웨어를 더 빠르게 전달하고, 고객 요구에 신속하게 대응하고, 요구가 증가할 때 솔루션을 확장할 수 있게 되었습니다."
> 
> - 소프트웨어 설계자 Henry Been
> 
> 

SnelStart는 전통적인 개발 모델인 코드, 패키지, 배송 및 반복을 사용하여 수년 동안 소프트웨어 비즈니스를 성공적으로 실행했습니다. 시간이 지나면서 변화의 속도는 점점 더 빨라지고 있습니다. 규정은 자주 변경되고, 고객은 재무 레코드를 처리하고, 변경에 맞게 회계사 및 정부와 협력할 수 있는 보다 쉬운 방법을 요구했습니다.

"고객에게 소프트웨어를 배송하는 일은 비용이 많이 들고 제한 요소도 많이 있습니다. 프로덕션, 패키지 및 배송 비용 때문에 우리가 소프트웨어를 출시하는 빈도에도 제한이 적용되었습니다. 우리는 정기적인 배송을 위해 업데이트를 패키지로 작성해야 했지만 고객의 변화하는 요구를 충족하는 것은 어려운 일이었습니다. 우리 고객이 최신 버전으로 제품으로 업그레이드했는지 보장할 수 없습니다. 따라서 여러 버전을 지원해야 했으며, 지원 작업을 잘 처리하는 것이 매우 어려웠습니다."

"우리는 가속화된 속도로 업데이트를 프로그래밍하고 릴리스하는 방법을 원했습니다. 따라서 더 빠르게 혁신하고 고객을 위한 새 서비스를 만들 수 있었습니다. 또한 우리는 고객의 비즈니스 관리 요구를 단순화하기 위해 더 많은 프로세스를 자동화하는 방법도 원했습니다."라고 Been은 덧붙였습니다.

SnelStart의 경우 이러한 솔루션은 클라우드 기반 SaaS 공급자가 되어서 해당 서비스를 확장하는 것이었습니다. Azure SQL 데이터베이스 플랫폼은 IaaS(infrastructure-as-a-service) 솔루션에 필요할 수 있는 주요 IT 오버헤드를 발생하지 않도록 도와주었습니다.

또한 클라우드 모델에서는 SnelStart가 버그를 수정하고 새 기능을 빠르게 제공할 수 있으므로 고객이 소프트웨어를 다운로드하거나 업그레이드할 필요가 없습니다. Been에 따르면 “Azure 클라우드 서비스를 사용하면 타사의 변화하는 요구에 빠르게 대응할 수 있습니다. 새 버전을 수천 명의 고객에게 제공하지 않고, 데스크톱 응용 프로그램에서 전송된 정보를 타사가 요구하는 새로운 형식으로 조정할 수 있습니다."

## <a name="a-modern-company-with-traditional-roots"></a>전형적인 기반의 현재 기업
SnelStart는 1964에서 다소 초라하게 시작한 기민한 현대식 하이테크 기업입니다. 당시에 설립자들은 악기 부품 제조업체로 이 회사를 시작했습니다. SnelStart 소프트웨어 비즈니스의 핵심은 실제로 개인용 컴퓨터가 급증했던 1980년대에 태동하기 시작했습니다. 이 회사는 사용하던 회계 소프트웨어보다 나은 대체 프로그램이 필요했습니다. 따라서 자체적으로 일을 추진하기 시작했습니다. 1982년에는 SnelStart 회계 소프트웨어의 기틀이 마련되었습니다. 처음부터 이 소프트웨어는 간편성과 속도를 추구했습니다. 결과적으로 이 기업은 소프트웨어 개발로 방향을 선회하고 소프트웨어 업체로 거듭나게 되었습니다.

1995년에 SnelStart는 최초의 Windows용 부기 응용 프로그램을 출시했습니다. Microsoft Visual Basic 1.0 및 Microsoft Access 데이터베이스를 기반으로 구축된 이 응용 프로그램을 통해 고객 기반이 5,000명 이상으로 확장될 수 있었습니다.

오늘날, SnelStart는 네덜란드의 중소기업 및 자영 사업가를 대상으로 하는 LOB(기간 업무) 및 비즈니스 관리 응용 프로그램의 주요 공급자입니다. “우리의 목표는 고객을 위한 비즈니스 관리 서비스를 100% 자동화하는 것입니다."라고 IT 설계자인 Carlo Kuip은 말했습니다.

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>탄력적 풀을 통해 성능 및 비용 최적화
SnelStart는 탄력적 데이터베이스 풀을 대규모로 일찌감치 활용했습니다. 탄력적 풀은 이 회사에서 비용을 제한하고 성능 요구를 보다 효율적으로 관리하도록 지원합니다. Been에 따르면 "탄력적 데이터베이스 풀을 사용하여 과도 프로비전 없이, 고객의 요구에 따라 성능을 최적화할 수 있습니다. 최대 부하를 토대로 프로비전해야 한다면 훨씬 비용이 많이 들 것입니다. 대신, 사용률이 낮은 여러 데이터베이스 간에 리소스를 공유할 수 있는 옵션을 통해 성능이 뛰어나고 비용 효과적인 솔루션을 작성할 수 있게 되었습니다."

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Azure SQL 데이터베이스는 격리 및 보안을 위해 데이터를 컨테이너에 보관하도록 지원합니다.
Azure SQL 데이터베이스를 사용하여 SnelStart는 고객의 온-프레미스 비즈니스 관리 데이터를 Azure에 쉽고 투명하게 이동할 수 있습니다. Azure SQL 데이터베이스는 인증, 권한 부여, 손쉬운 백업 및 복원 기능을 위해 격리, 경계를 제공하는 편리한 컨테이너입니다. 데이터베이스는 비즈니스 관리에 적합한 개념적 모델을 제공합니다. IT 설계자인 Carlo Kuip에 따르면, "이 컨테이너 경계 내의 항목에는 비즈니스에 중요한 데이터가 포함되어 있으며 이러한 항목을 격리된 데이터베이스에 저장하면 적절히 보호할 수 있습니다. 우리는 데이터베이스 수준에서 권한 부여를 관리할 수 있으며, DBA(데이터베이스 관리자) 없이도 관리를 자동화하고 데이터베이스를 확장할 수 있습니다.”

또한 Azure SQL 데이터 웨어하우스는 기업에서 침입 감지, 사용자 작업 로깅 및 연결 등의 원격 분석 데이터를 수집할 수 있도록 지원하여 SnelStart 보안 및 관리 영역에서 중요한 역할을 합니다.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure는 오버헤드를 제거하여 개발자가 가치를 전달하는 데 더 많은 시간을 투입할 수 있게 합니다.
Azure 플랫폼 모델은 인프라 오버헤드를 제거하며, SnelStart가 C# 관리 라이브러리를 사용하여 배포를 자동화할 수 있도록 했습니다. "우리는 고객을 위해 확장성, 속도 및 재해 복구 옵션을 높이면서 동시에 소수의 직원으로 현재 업무를 성장시킬 수 있었습니다. 서비스 개발로 전환하면서, 새로운 규정 또는 세금 코드에 맞게 기존 코드를 단순히 업데이트하지 않고 새로운 서비스 및 기능에 집중할 수 있게 리소스를 확보했습니다."라고 Kuip은 언급했습니다. "관리를 자동화하고 SaaS 제품을 사용하여 운영 직원에 큰 비용을 투자할 필요 없이 고객에게 더 나은 가치를 제공할 수 있습니다.”라고 덧붙였습니다. 예를 들어 Azure 및 탄력적 데이터베이스 풀을 사용하여 SnelStart는 은행, 새로운 청구 서비스, 중소기업 신원 조사 및 전자 메일 서비스와의 보다 강력한 고객 데이터 통합을 포함하여 다양한 새 기능을 추가할 수 있게 되었습니다.

> "2016년이 되고 처음 몇 달 만에, Azure SQL 데이터베이스 배포를 약 5,500건에서 12,000건 이상으로 확장했으며, 현재 매월 약 1,000개의 데이터베이스를 추가하고 있습니다."
> 
> - 소프트웨어 설계자 Henry Been
> 
> 

탄력적 작업 기능을 사용하여 데이터베이스 관리가 추가로 자동화됩니다. "우리는 SQL DB의 [서버] 인스턴스에서 제공되는 데이터베이스의 자동 검색 기능이 매우 감탄했습니다."라고 Kuip는 말했습니다. 이 기능을 통해 SnelStart는 추가 오버헤드 없이 동적으로 증가되는 고객 기반에서 관리 작업을 실행할 수 있습니다.

또한 SnelStart는 고객 데이터와 타사 소프트웨어 파트너에서 제작한 앱 간에 브로커 역할을 하는 API를 개발하고 있습니다. "이 API가 있으면 다른 공급업체에서 송장 및 기타 문서에 대한 데이터 항목 제거와 같은 기능을 우리 소프트웨어에 추가할 수 있습니다."라고 Kuip는 말했습니다. 고객은 더 이상 중소기업 회계 소프트웨어에 청구서를 수동으로 입력할 필요가 없습니다. SnelStart 소프트웨어가 필요한 정보를 직접 교환하기 때문입니다. 따라서 고객은 업계의 디지털 변환에서 발생하는 정보의 에코시스템으로 비즈니스 관리 작업에 참여할 수 있습니다.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Azure 서비스에서 SnelStart에서 SaaS를 사용하도록 설정하는 방법
SnelStart는 Azure를 사용하여 좀 더 원활하게 고객 및 해당 회계사에게 서비스를 제공할 수 있습니다. 예를 들어 고객과 회계사가 Azure에 호스트된 SnelStart의 클라이언트 API에 직접 액세스하여 정보를 공유할 수 있습니다. "이러한 재사용이 가능한 서비스는 고객 지향 웹앱에서 사용할 수 있으며, 고객을 위한 비즈니스 관리와 고객이 사용하는 타사 소프트웨어에 액세스할 수 있도록 하는 일반적인 인프라 및 기능을 제공합니다. 예로 제품 구성 기능 제공, 방화벽 규칙 관리 및 백업과 같은 장기 실행 프로세스 관리를 들 수 있습니다.

> 우리의 목표는 고객을 위한 비즈니스 관리 서비스를 100% 자동화하는 것입니다." 
> 
> - IT 설계자, Carlo Kuip
> 
> 

또한 SnelStart 웹 서비스는 고객 및 회계사가 Azure SQL 데이터베이스의 탄력적 풀에 있는 데이터에 쉽게 액세스할 수 있도록 합니다. 데이터베이스 탄력성 및 Azure 리소스 관리자와 결합된 이 SaaS 모델은 모든 Azure 배포를 보완하는 확장성 기능을 SnelStart에 제공합니다. 구현은 C# 관리 라이브러리를 사용하여 완전하게 자동화되었습니다.

![SnelStart 아키텍처](./media/sql-database-implementation-snelstart/figure1.png)

그림 1. 2016년 6월을 기준으로 SnelStart는 11,000개가 넘는 데이터베이스와 50개가 넘는 탄력적 데이터베이스 풀을 보유하고 있습니다.

## <a name="simplicity-from-the-cloud"></a>클라우드를 통해 간소화 구현
Azure 클라우드 기반 솔루션으로 전환한 이후로, SnelStart는 혁신적인 기능 및 서비스를 제공하면서 빠른 고객 성장을 지원할 수 있게 되었습니다. Been에 따르면 "Azure를 사용하여 우리는 운영 직원을 확장하지 않고도 고객에게 거의 지속적인 업데이트를 전달할 수 있습니다. 또한 확장성 및 재해 복구와 같은 기타 유용한 Azure 기능도 함께 사용할 수 있게 되었습니다."

> "우리가 레드먼드에 있을 때 네덜란드에 있는 개발자가 특정 문제 때문에 전화를 했습니다. 우리는 Microsoft에 우리 문제 해결을 위해 48시간 내에 프로덕션 환경에 변경 내용을 제공할 것을 요청할 수 있었습니다."
> 
> - 소프트웨어 설계자 Henry Been
> 
> 

SnelStart는 또한 Microsoft Azure SQL DB 팀과 함께 발전시킨 강력한 파트너십에도 고마움을 느끼고 있습니다. Kuip는 "우리는 양측의 의견을 고려해서 기능 및 기술 사용 방법에 대해 논의했습니다."라고 말했습니다.
SnelStart의 즉각적인 목표는 만족을 주는 고객 기반을 지속적으로 확충하는 것입니다. Been이 언급한 것처럼 "ISV로서 우리가 직면했던 기술 및 리소스 제한이 없어지면서 우리의 성장 잠재력에도 제한이 사라졌습니다."

## <a name="more-information"></a>자세한 정보
* Azure의 탄력적 데이터베이스 풀에 대한 자세한 내용은 [탄력적 데이터베이스 풀](sql-database-elastic-pool.md)을 참조하세요.
* 웹 역할 및 작업자 역할에 대한 자세한 내용은 [작업자 역할](../fundamentals-introduction-to-azure.md#compute)을 참조하세요.    
* Azure SQL 데이터 웨어하우스에 대한 자세한 내용은 [SQL 데이터 웨어하우스](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* SnelStart에 대해 자세히 알아보려면 [SnelStart](http://www.snelstart.nl)를 참조하세요.




<!--HONumber=Nov16_HO3-->


