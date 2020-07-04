---
layout: post
title: "[Maven 도입하기] Maven을 알아보자"
date: 2020-07-04 21:47:51 +0900
categories: jekyll update
---




> 안녕하세요. kyunni 입니다.
>
> 이 곳에는 개발 업무를 진행하면서 알게되었거나 IT Trend와 같은 내용들을 차곡차곡 정리해나갈 예정입니다.
>
> 그 시작으로 요즘 회사에서 진행 중인 Maven 도입에 관련하여 Maven이란 무엇인가에 대하여 자세히 포스팅하고자 합니다.





## Maven이란?

![img](http://maven.apache.org/images/maven-logo-black-on-white.png)



Maven은 Apache에서 제공하는 자바 프로젝트 관리 도구로 Apache Ant 대안으로 만들어졌으며, Apache License로 배포되는 오픈 소스 소프트웨어입니다. Maven은 pom(Project Object Model) 개념을 기반으로 프로젝트의 build, reporting 및 문서 관리 등이 가능합니다.



## Maven 특징

* **Build Lifecycle 관리**

  프로젝트의 전체적인 Lifecycle을 관리하는 도구이며 WAR, JAR 등의 프로젝트 산출물로 패키징해주는 build tool로서의 역할을 합니다. 

* **배포 관리**

  소스관리시스템(SVN, Git 등)과 통합하여 특정 tag를 기반으로 프로젝트 배포 관리가 가능합니다.
  배포툴(jenkins 등)에서 Maven을 통해 build가 진행되고 이를 통해 배포서버에 산출물(war 등)이 배포되는 형태입니다.

* **dependency(의존성) 관리**

  Maven에서는 jar 등 라이브러리를 관리하는 중앙repository를 사용하는 것을 권장합니다. 주로 NEXUS와 같은 사설 repository를 사용하며, 중앙 repository에서 필요 라이브러리를 다운받을 수 있는 메커니즘을 제공합니다. 

* **손 쉬운 plug-in 관리** 

  Java 또는 스크립팅 언어로 plug-in 관리가 쉽고 확장성이 좋습니다.

* **모델 기반 build**
   별도 build scripting 없이 metadata 기반으로 JAR, WAR 등의 형태로 배포가 가능합니다.

  

## Build Tool 종류

조사한 Ant, Maven, Gradle 모두 Apache License 기반입니다. 순서대로 Ant를 개선한 툴이 Maven, Maven을 개선한 툴이 Gradle입니다.

물론 아래 세 가지 종류 외에도 다양한 build Tool 또한 존재 합니다.



* **Ant**

  빌드스크립트 기반으로 빌드가 가능하여, 개발자가 원하는 방향으로 개발이 가능하다는 유연성에  큰 장점이 있습니다.

  * 각 프로젝트에 대한 XML 기반 빌드 스크립트 개발

  * 형식적 규칙이 없음: 결과물을 넣을 위치를 정확히 정의해야하며, 프로젝트에 특화된 Target과 Dependency를 이용해 모델링

  * 절차지향적: 명확한 빌드 절차 정의가 필요

  * 생명주기를 갖지 않기 때문에 각각의 target에 대한 의존관계와 일련의 작업을 정의해주어야 함

  * (단점) 유연성이 높으나 프로젝트가 복잡해질 경우, 각각의 Build 과정을 이해하기 어려움

  * (단점) XML, Remote Repository를 가져올 수 없음 

  * (단점) 스크립트 재사용이 어려움

    

* **Maven**

  프로젝트에 필요한 모든 Dependency를 리스트의 형태로  Maven에 정의하여 관리하는 방식입니다.

  * (장점) Dependency를 관리하고, 표준화된 프로젝트(Standardized Project) 제공

  * (장점) XML, remote repostitory를 가져올 수 있음 : 개발에 필요한 종속되는 'jar', 'class path'를 다운로드할 필요 없이 선언만으로 사용 가능

  * (장점) 상속형 : 하위 XML이 필요 없는 속성도 모두 표기

  * (단점) 라이브러리가 서로 종속할 경우 XML이 복잡해짐

  * (단점) 계층적인 데이터를 표현하기에 좋지만, 플로우나 조건부 상황을 표현하기엔 어려움

  * (단점) 편리하나 맞춤화된 로직 실행이 어려움

    

* **Gradle**

  build 자동화에 대한 요구 증가에 의해 보완된 build Tool입니다. `Gradle`은  JVM 기반의 빌드 도구로 기존 Ant, Maven을 보완하였습니다. 따라서 Java 혹은 Groovy를 이용하 logic을 개발자의 의도에 따라 설계가 가능합니다.

  * 오픈 소스 기반의 build 자동화 시스템으로 Groovy 기반 DSL(Domain-Specific Language)로 작성

  * Build-by-convention을 바탕으로 함 : 스크립트 규모가 작고 읽기 쉬움

  * Multi 프로젝트 빌드를 지원하기 위해 설계

  * 설정 주입 방식 (Configuration Injection)

    

## Maven Build Lifecycle

Maven에서는 미리 정의하고 있는 build 순서가 있습니다. 이 일련의 build 과정을 `Lifecycle`이라고 하며, 총 3 가지 종류의 Lifecycle을 제공합니다.



* **Default(Build) Lifecycle**

  소스 코드를 compile, test, package, deploy를 담당하는 기본 Lifecycle입니다.

  | Phase     | Description                                                  |
  | --------- | ------------------------------------------------------------ |
  | `compile` | 소스 파일 컴파일                                             |
  | `test`    | Junit, TestNG와 같은 단위 테스트 프레임워크로 단위 테스트 진행<br />기본 설정은 단위 테스트가 실패하면 build 실패로 간주 |
  | `package` | 단위 테스트 성공 시, pom.xml의 <packaging /> 엘리먼트 값 (jar, war, ear 등)에 따라 패키징 진행 |
  | `install` | 로컬 저장소에 패키징 파일 배포 (개발자 PC)                   |
  | `deploy`  | 원격 저장소에 패키징 파일 배포 (Maven 저장소)                |

  

 *  **Clean Lifecycle**

    build한 결과물을 제거하기 위한 clean Lifecycle입니다.

    | Phase   | Description                                                  |
    | ------- | ------------------------------------------------------------ |
    | `clean` | 이전 build를 통하여 생성된 모든 산출물 삭제<br />Maven에서는 기본 build 시, target directory에 모든 결과물을 생성하므로 target directory 자체 삭제 |

    

* **Site Lifecycle**

  프로젝트 문서 사이트를 생성하는 Site Lifecycle

  | Phase         | Description                                     |
  | ------------- | ----------------------------------------------- |
  | `site`        | Maven 설정 파일 정보 기반 문서 사이트 생성 지원 |
  | `site-deploy` | 생성 문서 사이트를 설정되어 있는 서버에 배포    |

  

## Phase & Goal

`Phase`는 빌드 단계와 각 단계의 순서를 정의하고 있는 개념입니다. 그리고 phase와 플러그인으로 연결되어 실행시킬 명령이 `Goal`입니다.

즉, Lifecycle 내에서 phase를 통해 goal을 실행하면 해당 단계에 맞는 작업이 실행되는 개념입니다.





![img](https://mblogthumb-phinf.pstatic.net/MjAxNzAyMDhfOTIg/MDAxNDg2NTQ3NTMxMTk4.NgcoWXTJRvVaPijCs2MmK6yqmqXfqRRpyrML1dkGSY4g.QnYn6PS8gVx_8GvAPQ1WNbh9hUGrilQr6B_aSMxguOkg.PNG.goddlaek/image.png?type=w800)



## Maven Plugin

Maven에서 제공하는 모든 기능은 plugin을 기반으로 동작합니다.  Maven 자체는 기본적인 기능만 지니고 있고, 대부분의 기능은 plugin을 통해 제공하도록 되어 있습니다. 

Plugin은 몇 가지 goal을 가지고 있고, goal은 plugin에 포함되어 있는 명령입니다. 즉, plugin은 하나 이상의 goal의 집합체입니다.

Lifecycle 내에 정의되어 있는 각 Phase는 연결되어 있는 plugin을 통해 goal을 실행시키는 개념이라고 이해하면 될 것 같습니다. 아래는 Maven에서 활용할 수 있는 대부분의 plugin을 제공하는 사이트입니다.

- 아파치 메이븐 사이트 : [http://maven.apache.org/plugins/](http://maven.apache.org/plugins/)
- 코드하우스 모조 프로젝트 : [http://mojo.codehaus.org/plugins.html](http://mojo.codehaus.org/plugins.html)



 