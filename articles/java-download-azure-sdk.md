---
title: "Java용 Azure SDK 다운로드"
description: "Java용 Azure SDK를 다운로드하는 방법을 Maven 프로젝트에 제공된 샘플 코드 및 Eclipse용 Azure 도구 키트 설치 단계를 통해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 4b8f8fe6-1b26-4bb4-9be9-6ae757a59e66
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2016
ms.author: robmcm
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 25b7e591172ea810ce370f946eb46258c801ba36


---
# <a name="download-the-azure-sdk-for-java"></a>Java용 Azure SDK 다운로드
이 문서는 Java용 Azure 라이브러리를 다운로드하고 설치하기 위한 지침이 포함되어 있습니다.

**참고:** Java용 Azure 라이브러리는 [Apache 라이선스 버전 2.0][license](영문)에 따라 배포됩니다.

## <a name="azure-libraries-for-java---manual-download"></a>Java용 Azure 라이브러리 - 수동 다운로드
Java용 Azure 라이브러리를 수동으로 설치하려면 <http://go.microsoft.com/fwlink/?LinkId=690320>을 클릭하여 모든 라이브러리와 종속성이 포함된 ZIP 파일을 다운로드합니다.

ZIP 파일을 컴퓨터에 다운로드했으면 콘텐츠를 추출하고 다음 옵션 중 하나를 사용하여 프로젝트에 JAR 파일을 추가합니다.

* Eclipse의 Java 프로젝트에 JAR 파일을 가져옵니다.
* Eclipse의 Java 프로젝트에 대한 **빌드 경로** 를 구성하여 JAR 파일에 경로를 포함시킵니다.

Eclipse에서 빌드 경로 설정에 대한 자세한 내용은 Eclipse 웹 사이트에서 [Java 빌드 경로] 문서를 참조하세요.

**참고:** 라이선스 및 기타 정보는 ZIP에 포함된 license.txt 및 ThirdPartyNotices.txt 파일을 참조하세요.

## <a name="azure-libraries-for-java---building-with-maven"></a>Java용 Azure 라이브러리 - Maven을 사용하여 빌드
### <a name="step-1---set-up-your-project-to-use-maven-for-build"></a>1단계 - 빌드에 Maven을 사용하도록 프로젝트 설정
Java용 Azure 라이브러리를 사용하는 Eclipse에서 Maven 프로젝트를 만들려면 [Java용 Azure 관리 라이브러리 시작][maven-getting-started] 문서에 나와 있는 지침을 따르세요. 

### <a name="step-2---configure-your-maven-settings-with-the-requisite-dependencies"></a>2단계 - Maven 설정에서 필수 종속성 구성
빌드에 Maven을 사용하도록 프로젝트를 구성했으면 다음 예제와 같은 구문을 사용하여 pom.xml 파일에 필수 종속성을 추가할 수 있습니다. 다음 예제에 나열되어 있는 모든 종속성을 추가할 필요는 없습니다. 프로젝트에 필요한 특정 종속성만 추가하면 됩니다.

> [!NOTE]
> 다음 샘플의 각 `<version>` 요소 내에서 이 예제의 "n.n.n" 자리 표시자를 유효한 버전 번호로 바꿉니다. 버전 번호는 [Maven의 Azure 라이브러리 리포지토리]에서 얻을 수 있습니다.
> 
> 

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-compute</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-network</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-sql</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-storage</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-websites</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-media</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-servicebus</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-serviceruntime</artifactId>
        <version>n.n.n</version>
    </dependency>

## <a name="installing-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트 설치
이 섹션에는 Eclipse용 Azure 도구 키트를 설치하기 위한 기본 지침이 나와 있습니다. 자세한 내용은 [Eclipse용 Azure 도구 키트 설치]를 참조하세요.

### <a name="prerequisites"></a>필수 조건
1. [Eclipse용 Azure 도구 키트의 새로운 기능] 문서에 나열된 Windows 운영 체제입니다.
2. [Eclipse용 Azure 도구 키트의 새로운 기능] 문서에 나열된 Macintosh 또는 Linux 운영 체제입니다.
3. Eclipse IDE for Java EE Developers, Indigo 이상. <http://www.eclipse.org/downloads/>에서 다운로드할 수 있습니다.

### <a name="basic-installation-steps"></a>기본 설치 단계
1. Eclipse의 **도움말** 메뉴에서 **새 소프트웨어 설치**를 선택합니다.
2. <http://dl.microsoft.com/eclipse> 사이트 위치를 입력하고 **Enter** 키를 누릅니다.
3. 설치할 항목을 선택하고 **Finish**를 클릭합니다.

Eclipse용 Azure 도구 키트는 최신 버전의 Azure SDK를 사용합니다. 이 SDK는 <http://go.microsoft.com/fwlink/?LinkID=252838>에서 WebPI(웹 플랫폼 설치 관리자)를 사용하여 다운로드할 수 있습니다. 그러나 설치되어 있지 않은 경우 첫 번째 Azure 배포 프로젝트를 만들 때 Eclipse용 Azure 도구 키트에서 해당 버전의 Azure SDK를 자동으로 설치합니다.

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트]

[Eclipse용 Azure 도구 키트 설치] 

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.

<!-- URL List -->

[Azure Java 개발자 센터]: http://go.microsoft.com/fwlink/?LinkID=699547
[Maven의 Azure 라이브러리 리포지토리]: http://go.microsoft.com/fwlink/?LinkID=286274
[Eclipse용 Azure 도구 키트]: http://go.microsoft.com/fwlink/?LinkID=699529
[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]: http://go.microsoft.com/fwlink/?LinkID=699533
[Eclipse용 Azure 도구 키트 설치]: http://go.microsoft.com/fwlink/?LinkId=699546
[Java 빌드 경로]: http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Freference%2Fref-properties-build-path.htm
[license]: http://www.apache.org/licenses/LICENSE-2.0.html
[maven-getting-started]: http://go.microsoft.com/fwlink/?LinkID=622998
[zip-download]: http://go.microsoft.com/fwlink/?LinkId=690320
[Eclipse용 Azure 도구 키트의 새로운 기능]: http://go.microsoft.com/fwlink/?LinkId=690333



<!--HONumber=Nov16_HO3-->


