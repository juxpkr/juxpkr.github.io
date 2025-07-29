---
layout: single
title: 2025-06-20-Azure-Functions
date: 2025-06-20 16:16:14 +0900
category:
  - learn
tags:
  - Azure
  - Learn
  - AzureFunctions
toc: "true"
toc_sticky: "true"
---

## 1. 서론 : 왜 서버리스 컴퓨팅(Azure Functions)인가? 

### 1.1 배치 처이 방식의 한계

* **데이터 수집 및 분석 지연**
	* 기존의 배치 처리 방식은 데이터를 모아서 한 번에 처리하기 때문에, 필연적으로 시간지연이 발생한다. 이 시간 지연은 비즈니스 의사 결정에 큰 영향을 미치며, 다양한 문제를 야기한다. 
* **의사 결정 속도 저하**
	* 배치 처리 방식은 분석 결과가 늦게 나와서 의사 결정을 신속하게 내리는 것을 어렵게 만든다. 이러한 의사 결정 지연은 기업의 경쟁력을 약화시키고, 다양한 손실을 초래할 수 있다. 
* **기회 상실과 위험 증가**
	* 실시간으로 발생하는 문제점이나 새로운 기회를 포착하지 못할 수 있다.
- **비효율적인 리소스 사용**
	- 배치 처리 방식은 데이터를 모아서 한 번에 처리하기 때문에, 필요 이상의 컴퓨팅 리소스를 소모하고, 데이터 처리 시간과 비용을 증가시키는 비효율적인 구조를 가지고 있다. 


### 1.2 Azure Functions의 등장 : 서버리스 컴퓨팅이 필요한 이유와 실시간 데이터 분석의 장점

 데이터의 양이 폭증하고, 비즈니스의 속도가 가속화 되면서 기존의 배치 처리 방식은 한계에 직면한다. 데이터를 모아서 한번에 처리하는 방식은 필연적인 시간 지연을 야기한다. 이는 신속한 의사결정을 저해하고, 실시간으로 발생하는 비즈니스 기회나 문제에 즉각 대응하기 어렵게 만든다. 또한 예측 불가능한 데이터 유입량에 대해 리소스 사용의 비효율성을 초래한다.
 
 이러한 문제점을 해결하고 **실시간 데이터 분석의 이점을 극대화하기 위해 등장한 것이 서버리스(Serverless)컴퓨팅** 이다. 그리고 Microsoft Azure 클라우드 환경에서 이 서버리스 컴퓨팅을 대표하는 서비스가 바로 Azure Functions이다.

 Azure Functions는 애플리케이션 실행에 필요한 인프라와 리소스를 주문형(On-Demand)으로 제공하며 지속적으로 업데이트한다. Azure Functions가 가진 서버리스의 핵심 특성들은 위에서 언급된 배치 처리의 한계를 극복하고 실시간 데이터 파이프라인 구축에 혁신적인 이점을 제공한다.

##### 리소스의 On-Demand제공 및 종량제 과금
Azure Functions는 코드가 실제로 실행될 때만 컴퓨팅 리소스를 할당하고, 사용한 만큼만 비용을 청구하는 모델이다. 이는 24시간 서버를 유지해야 하는 기존 방식과 달리, 데이터 유입량이 불규칙하거나 예측 불가능한 상황에서 **비용을 크게 절감하고 효율적인 리소스 사용을 가능하게 한다**. 특히 웹 크롤링이나 특정 이벤트 발생 시에만 짧게 실행되는 데이터 수집 및 변환 작업에 최적화 되어있다.

##### 자동 스케일링을 통한 즉각적인 확장성 
대규모의 데이터 스트림이 갑자기 유입되거나 트래픽이 폭증하더라도, Azure Functions는 자동으로 필요한 만큼의 인스턴스를 확장하여 모든 요청을 지연 없이 처리한다. 이러한 **빠른 확장성**은 데이터 수집 및 분석의 지연을 최소화하고, 항상 **최신 정보를 실시간으로 제공**한다. 이는 기업이 '빠른 의사결정'을 내리고, 실시간으로 '문제를 해결'하며, '기회를 포착'하는 데 필수적이다.
		
##### 서버 관리 부담 감소와 개발 생산성 향상
Azure Functions는 기반 인프라(서버, 운영체제, 런타임 등)의 관리 및 유지보수를 Microsoft Azure가 전적으로 책임진다. 데이터 엔지니어는 인프라 운영에 대한 부담 없이 **순수하게 비즈니스 로직을 구현하는 코드 개발에만 집중할 수 있다.** 이는 개발 생산성을 크게 향상시키고, 데이터 파이프라인 구축 및 변경에 소요되는 시간을 단축시켜 전반적인 운영 효율성을 극대화한다.

결론적으로, Azure Functions는 서버리스 특성 덕분에 실시간 데이터 파이프라인 구축의 핵심적인 구성요소가 된다. 배치 처리의 한계를 뛰어넘어 **신속하고, 비용 효율적이며, 확장 가능한 데이터 처리 환경을 제공한다.**



#### 1.3 Azure Functions의 핵심 개념과 데이터 엔지니어링 파이프라인에서 Azure Functions의 역할, 그리고 실제 활용 사례

##### 파트너 시스템에서 제품 카탈로그 정보를 파일 형태로 Blob Storage에 업로드 하는 시나리오
1. 파일 업로드 : 파트너 시스템에서 제품 카탈로그 정보가 담긴 파일을 Azure Blob Storage에 업로드
2. Blob Storage 트리거 : Blob Storage에 파일이 업로드 되는 즉시, Blob Storage 트리거가 Azure Functions를 활성화
3. Azure Functions 실행 및 파일 처리 : 
	-  트리거 된 Azure Functions는 업로드 된 파일을 다운로드 하여 데이터 유효성 검사를 수행
	-  유효성 검사를 통과한 데이터는 Azure Functions 내에서 데이터 변환 작업 수행
	-  변환된 데이터는 기본 시스템으로 전달하여 제품 카탈로그 정보 업데이트를 진행
4. 처리 결과 : Azure Functions는 파일 처리 결과를 로깅하거나 추가적인 후속 작업을 수행할 수 있다. 성공/ 실패 여부를 별도 저장소에 기록하거나 관리자에게 알림을 보내는 등의 기능을 구현할 수 있다.

![](/assets/images/posts/AF_diagram1.png)


##### IoT 센서로부터 생성되는 방대한 양의 데이터를 실시간으로 처리하는 시나리오
1. 데이터 수집 (Event Hubs): 다수의 IoT 센서가 온도, 습도, 조도, 움직임 등 다양한 환경 데이터를 측정하여 Event Hubs로 전송
2. Event Hubs 트리거 : 데이터가 도착하는 즉시, Azure Functions가 Event Hubs 트리거에 의해 자동으로 활성화 (데이터 스트림의 유입을 감지하고, 데이터 처리 함수를 즉시 실행시키는 '자동 감지' 시스템으로 작동됨)
3. Azure Function을 활용한 데이터 전처리 및 분석 :
	- 트리거 된 Azure Functions는 Event Hubs로 부터 센서 데이터를 받아 전처리 과정을 수행. 데이터 정규화, 오류 데이터 필터링, 필요한 정보 추출 등 분석에 용이한 형태로 데이터를 가공
	- 전처리 된 데이터는 Azure Stream Analytics와 같은 실시간 데이터 분석 서비스로 전달되어 분석. IoT센서 데이터 분석을 통해 의미 있는 정보를 실시간으로 추출. 예를들어, 특정 임계 값을 초과하는 온도 데이터를 감지하여 경고를 발생시킬 수 있음.
4. 처리 결과 활용 : 분석 결과는 대시보드를 통해 시각화 하여 실시간 모니터링에 활용하거나, 알림 시스템과 연동하여 이상 상황 발생 시 즉시 관리자에게 전송할 수 있음

![](/assets/images/posts/AF_diagram2.png)


##### 금융 서비스의 고객 데이터베이스에서 중복 항목을 제거하는 작업을 일정에 따라 자동화 하는 시나리오
1. 예약 작업 설정(Timer 트리거) : 함수를 실행 할 시간 및 주기를 정의
2. Azure Functions 자동 실행 : 설정된 시간 또는 주기가 되면 Timer 트리거가 자동으로 Azure Functions를 실행. 금융 서비스 담담자는 별도의 수동 작업 없이, 예약된 시간에 데이터 베이스 정리 작업이 시작되는 것을 확인 할 수 있다.
3. 중복 항목 제거 작업 수행 : Azure Functions는 금융 서비스 고객 데이터베이스를 조회하여 중복된 고객 정보 항목을 식별하고 제거
4. 작업 결과 로깅 : Azure Functions는 중복 제거 작업 실행 결과를 로깅. 제거된 중복 항목 수, 제거된 항목의 상세 정보, 작업 성공/실패 여부 등을 로그에 기록하여 데이터 정리 작업의 이력을 관리 
![](/assets/images/posts/AF_diagram3.png)


### 2. Azure Functions 핵심 개념
 

#### 2.1 이벤트 기반 아키텍처

Azure Functions은 이벤트 기반 아키텍처 (Event-Driven Architecture)의 핵심 구성 요소이다.
이벤트 기반 아키텍처는 시스템 내에서 발생하는 특정 '이벤트'에 반응하여 미리 정의된 코드나 프로세스가 자동으로 실행되도록 설계된 방식을 의미한다.

데이터 엔지니어링 관점에서 이벤트는 새로운 데이터 유입, 파일 생성, 메시지 큐에 데이터 도착, 특정 시간 도달 등 다양한 형태로 정의될 수 있다. Azure Functions는 이러한 다양한 이벤트를 **트리거(Trigger)** 메커니즘을 통해 감지하고, 해당이벤트에 특화된 함수 코드를 즉각적으로 실행한다.

결론적으로, 이벤트 기반 아키텍처는 현대의 고속 데이터 처리 및 복잡한 분산 시스템 구축에 필수적인 패러다임이며, Azure Functions는 이러한 아키텍처를 구현하는 데 최적화된 서버리스 컴퓨팅 서비스이다.
#### 2.2 트리거 (Triggers)

Azure Functions는 특정 '이벤트'가 발생했을 때 미리 정의된 함수 코드를 자동으로 실행시킨다. 이때 함수 실행을 시작하는 역할을 하는 것이 바로 **트리거(Trigger)이다**. 트리거는 마치 함수의 방아쇠와 같아서, 다양한 외부 시스템이나 서비스의 변화를 감지하고 함수를 깨워 작업을 수행하게 만든다.

데이터 엔지니어링 파이프라인에서 Azure Functions의 트리거는 데이터 흐름의 시작점 역할을 하며, 다양한 데이터 수집 및 처리 시나리오를 가능하게 한다.

##### HTTP 트리거
- **정의** : 웹이나 애플리케이션에서 HTTP요청(GET, POST 등)이 들어오면 Azure Functions를 실행한다.
- **활용** : 외부 시스템으로부터 데이터를 API형태로 수신하거나, 웹훅(Webhook)을 통해 실시간 알림을 받을 때 유용하다. 예를 들어, 특정 데이터가 업데이트되었을 때 외부 서비스가 Functions의 HTTP엔드포인트를 호출하여 알리거나, REST API를 구축하여 데이터를 입력받는 용도로 활용된다.

##### Timer 트리거
- **정의** : 설정해 놓은 시간 간격(CRON 표현식)에 따라 Azure Functions가 자동으로 작동을 시작한다.
- **활용** : 주기적인 데이터 수집, 배치 작업 실행, 데이터베이스 정리 등 정해진 시간에 반복적으로 수행해야 하는 작업에 최적화되어있다. 프로젝트에서 주기적으로 웹 크롤링을 수행하여 최신 데이터를 수집하는 핵심적인 역할을 담당할 수 있다.

##### Event Hub 트리거
- **정의** : Azure Event Hubs에 새로운 이벤트(데이터 스트림)가 도착하면 Azure Functions가 즉시 실행된다.
- **활용** : 대규모 실시간 데이터 스트리밍 파이프라인의 핵심 진입점이다. IoT 센서 데이터, 웹 클릭 스트림, 애플리케이션 로그 등 **연속적으로 발생하는 대량의 데이터를 Event Hubs를 통해 수집한 후, Functions가 이를 실시간으로 받아 전처리하거나 다음 단계로 전달**하는 데 활용된다.
##### Queue 트리거
- **정의** : 메시지 큐(Azure Storage Queue 등)에 새로운 메시지나 작업이 들어오면 Azure Functions가 자동으로 실행된다.
- **활용** : 비동기적인 작업 처리 및 시스템 간의 느슨한 결합을 구현할 때 사용된다. 대량의 요청을 일괄적으로 처리하거나, 웹 요청과 같이 지연될 수 있는 작업을 백그라운드 큐로 분리하여 처리할 때 효과적이다. 예를 들어, 웹에서 사용자가 대용량 파일을 업로드하면 큐에 메시지를 넣고, Functions가 이 메시지를 받아 비동기적으로 파일을 처리하는 방식이다.

##### Blob Storage 트리거
- **정의** : Azure Blob Storage에 새로운 파일이 업로드되거나 기존 파일이 수정되면 Azure Functions가 동작한다.
- **활용** : 파일 기반의 데이터 수집 파이프라인에서 매우 유용하다. 외부 시스템이 Blob Storage에 파일을 업로드하는 즉시 Functions가 이를 감지하여 파일의 유효성을 검사하고, 데이터를 추출하며, 필요한 변환을 수행하여 다른 저장소로 옮기는 등의 자동화된 워크플로우를 구축할 수 있다.

#### 2.3 바인딩 (Bindings)

바인딩(Binding)은 Azure Functions에서 함수 코드 내에서 외부 서비스의 데이터에 접근하는 과정을 간소화하는 강력한 도구이다. 바인딩을 사용하면 데이터의 입력 및 출력을 함수 코드 내에서 직접적으로 구현하지 않고도, `function.json` 파일에 선언적으로 정의하여 외부 서비스와 쉽게 연동할 수 있다. 이는 코드의 복잡성을 줄이고, 재사용성을 높이며, 개발 생산성을 크게 향상시킨다.

##### 입력 바인딩 (Input Binding)
- **정의** : 함수가 실행될 때 필요한 데이터를 외부 서비스로부터 자동으로 가져와 함수 코드 안에서 바로 사용할 수 있도록 하는 도구이다.
- **활용** : 함수가 특정 파일을 읽거나, 데이터베이스에서 정보를 조회해야 할 때 유용하다. 예를 들어, Blob Storage 입력 바인딩을 통해 특정 Blob 파일의 내용을 함수가 직접 읽어오거나, Cosmos DB 입력 바인딩을 통해 데이터베이스의 특정 문서를 함수 안에서 바로 참조할 수 있게 해준다.

##### 출력 바인딩 (Output Binding)
- **정의** : 함수가 처리한 결과물(데이터)을 자동으로 외부 서비스에 저장하거나 다른 서비스로 전송해 주는 도구이다. 함수 코드 내에서 명시적인 API 호출이나 클라이언트 라이브러리 코드를 작성할 필요 없이, 바인딩 정의만으로 데이터 전송이 이루어진다.
- **활용** : 함수에서 처리된 데이터를 다음 파이프라인 단계로 쉽게 전달할 때 사용된다. 예를 들어, **Event Hub 출력 바인딩을 통해 웹 크롤링으로 수집한 데이터를 Azure Event Hubs로 자동으로 푸시**하여 실시간 스트리밍 파이프라인의 다음 단계로 연결할 수 있다. 또한, Blob Storage 출력 바인딩을 사용하여 처리 결과를 Blob 파일로 저장하거나, Azure SQL Database 출력 바인딩을 통해 변환된 데이터를 관계형 데이터베이스에 저장할 수 있다.

바인딩은 트리거와 함께 Functions의 '이벤트 기반' 및 '서버리스' 특성을 극대화하며, 복잡한 데이터 파이프라인을 매우 간결하고 효율적으로 구축할 수 있게 돕는 핵심 기능이다.

#### 3. Azure Functions 개발 및 배포 실습

##### 3.1 개발 환경 설정 및 함수 앱 생성

Azure Functions 를 배포하기 위한 첫 단계는 함수 앱 (Function App) 리소스를 생성하는 것이다.
함수 앱은 함수 코드가 실행될 환경을 제공하며, 필요한 인프라와 리소스를 관리한다. 이 과정에서 함수 앱의 이름, 런타임 스택, 호스팅 계획 등 핵심적인 설정을 구성하게 된다.

#### 3.1.1 호스팅 계획 선택
함수 앱의 호스팅 계획은 성능, 비용, 확장성에 직접적인 영향을 미치므로 신중하게 선택해야 한다. Azure Functions는 다양한 워크로드에 맞춰 여러 가지 호스팅 옵션을 제공한다.

- **사용량**: 가장 대표적인 서버리스 호스팅 계획이다. 함수가 실행될 때만 리소스가 할당되고, 사용한 만큼만 비용을 지불한다. 자동 스케일링을 통해 트래픽 급증에 유연하게 대응한다. 콜드 스타트가 발생할 수 있지만, 비용 효율성이 가장 높다.
- **Functions 프리미엄**: Consumption 계획의 장점(탄력적 확장, 종량제 과금)을 유지하면서도 콜드 스타트를 최소화하고 가상 네트워크 연결 같은 고급 기능을 제공한다.
- **App Service 계획**: 전용 컴퓨팅 리소스를 항상 할당하는 방식이다. 다른 App Service 앱과 리소스를 공유하며, 예측 가능한 부하가 있는 경우 비용 효율적일 수 있다.
- **Container Apps 환경**: 컨테이너화된 함수를 실행할 때 사용하며, 마이크로 서비스 아키텍처에 적합하다.

데이터 엔지니어링 워크로드, 특히 이벤트 기반의 간헐적이고 예측 불가능한 데이터 처리 작업에는 **사용량**이 가장 적합하고 비용 효율적인 선택이다. 나는 실습에서 '사용량' 계획을 선택했으며, 실제 프로젝트에서도 해당 계획이 안정적으로 오류 없이 작동하는 것을 확인하여 주력으로 사용하고 있다.

![](/assets/images/posts/create_functionApp1.png)
#### 3.1.2 기본 정보 설정
- **구독** : Azure 리소스가 속할 구독을 선택한다.
- **리소스 그룹** : 관련 Azure 리소스들을 논리적으로 묶어 관리하는 컨테이너다. 함수 앱과 관련된 모든 리소스를 하나의 리소스 그룹에 두면 관리가 용이하다. 기존 리소스 그룹을 선택하거나 새로 생성할 수 있다.
- **함수 앱 이름** : 함수 앱의 이름을 지정한다. 도메인과 결합하여 함수의 기본 URL이 된다.
- **운영 체제** : 함수 앱이 실행될 운영체제를 선택한다. Python 런타임 스택은 주로 Linux를 사용한다.
- **지역** : 함수 앱이 배포될 Azure 데이터센터의 지리적 위치를 선택한다. 사용자와 가까운 지역을 선택하면 지연 시간을 줄일 수 있으며, 데이터 규정 준수 요건도 고려해야 한다.
![](/assets/images/posts/create_functionApp2.png)

#### 3.1.3 Azure에 배포 및 모니터링

로컬 환경에서 함수 코드를 성공적으로 작성했다면, 다음 단계는 이 함수를 Azure 클라우드에 배포하고 정상적으로 작동하는지 모니터링하는 것이다. VS Code의 Azure Function extension은 이러한 배포 과정을 매우 편리하게 지원한다.

##### 로컬 설정(local.settings.json) 업로드

함수 앱은 데이터베이스 연결 문자열, API 키, 웹훅 URL 등 민감하거나 환경별로 달라지는 설정 정보를 필요로 한다. 로컬 환경에서 이러한 설정은 `local.settings.json` 파일에 저장된다. Azure에 함수를 배포하기 전에, 이 로컬 설정을 Azure Function App의 '애플리케이션 설정(Application Settings)'으로 안전하게 업로드하는 과정이 필요하다. 이는 보안을 강화하고, 환경별 설정 관리를 용이하게 한다.
![](/assets/images/posts/Pasted%20image%2020250706143543.png)


##### 함수 앱 배포

`local.settings.json` 설정이 Azure에 안전하게 반영되면, 이제 함수 코드를 Azure Function App에 배포할 차례이다. VS Code 내에서 몇 번의 클릭만으로 로컬 개발 환경의 코드를 클라우드에 쉽게 올릴 수 있다. 이 과정은 함수 앱을 빌드하고, 필요한 종속성(dependencies)을 설치하며, 최종적으로 Azure 리소스에 코드를 배포하는 일련의 작업을 포함한다.
![](/assets/images/posts/Pasted%20image%2020250706143548.png)

##### 배포된 함수 모니터링

배포가 성공적으로 완료되면, Function App은 Azure 클라우드에서 정의된 트리거에 따라 대기하고, 이벤트 발생 시 자동으로 실행될 준비를 마친다.

함수가 배포된 후에는 Azure Portal을 통해 함수의 실행 상태와 성능을 지속적으로 모니터링하는 것이 중요하다. Azure Functions는 Application Insights와 같은 통합된 모니터링 도구를 제공하여, 함수의 실행 로그, 오류 발생 여부, 성능 지표 등을 실시간으로 확인할 수 있게 한다. 이를 통해 함수의 정상 작동을 확인하고, 문제가 발생했을 때 신속하게 진단하고 대응할 수 있다.

![](/assets/images/posts/Pasted%20image%2020250706150605.png)


#### 3.2 함수 코드 작성 (Python)

이 섹션에서는 Azure Functions의 기본적인 작동 방식(트리거 및 바인딩)을 보여주는 간단한 Python 함수 코드 예시를 다룬다. 이 코드는 특정 프로젝트에 종속되지 않고, Functions의 핵심 기능을 이해하는 데 초점을 맞춘다.

##### 간단한 HTTP 트리거 함수 예시
이 함수는 HTTP 요청을 받으면 응답 메시지를 반환하는 기본적인 HTTP 트리거 함수이다. 함수 매개변수로 HTTP 요청 객체(req)를 받아 처리한다.

```
import logging
import azure.functions as func

# Azure Functions 앱 인스턴스 생성
app = func.FunctionApp()

@app.http_trigger(
    methods=['GET', 'POST'], 
    auth_level=func.AuthLevel.FUNCTION # 함수 키 필요
)
def simple_http_function(req: func.HttpRequest) -> func.HttpResponse:
    logging.info('Python HTTP trigger function processed a request.')

    name = req.params.get('name')
    if not name:
        try:
            req_body = req.get_json()
        except ValueError:
            pass
        else:
            name = req_body.get('name')

    if name:
        return func.HttpResponse(f"안녕하세요, {name}님! Azure Functions에 오신 것을 환영합니다.", status_code=200)
    else:
        return func.HttpResponse(
            "이 함수는 이름 매개변수를 기대합니다. 쿼리 문자열 또는 요청 본문에 이름을 전달해주세요.",
            status_code=400
        )
```

##### 바인딩 정의(`function.json` 예시)

Python V2 앱 모델에서는 트리거와 바인딩이 Python 코드 내의 데코레이터를 통해 정의되므로, 별도의 `function.json` 파일을 직접 생성하거나 편집할 필요가 없다. 런타임이 코드를 분석하여 이 메타데이터를 동적으로 생성한다. 그럼에도 불구하고, `function.json`이 내부적으로 어떻게 구성될 수 있는지 이해를 돕기 위해 일반적인 Timer Trigger와 Blob Output 바인딩 예시를 보여준다.

```
{
  "scriptFile": "__init__.py",
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "0 */5 * * * *" // 매 5분마다 실행 예시
    },
    {
      "name": "outputBlob",
      "type": "blob",
      "direction": "out",
      "path": "outputcontainer/{name}.txt", // Blob Storage 경로 예시
      "connection": "AzureWebJobsStorage"
    }
  ]
}
```


##### 로컬 환경 변수 설정 (`local.settings.json` 예시)

로컬 개발 환경에서 사용되는 환경 변수들은 `local.settings.json` 파일에 정의된다. 이 값들은 Azure에 배포될 때 함수 앱의 '애플리케이션 설정'으로 안전하게 업로드되어 사용된다.

```
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "MyAPI_URL": "https://api.example.com/data", // 예시 API URL
    "MyBlobStorageConnection": "DefaultEndpointsProtocol=https;AccountName=yourstorage;AccountKey=...", // 예시 Blob Storage 연결 문자열
    "MyQueueConnection": "DefaultEndpointsProtocol=https;AccountName=yourqueue;AccountKey=..." // 예시 Queue Storage 연결 문자열
  }
}
```




재난문자 API 알림 시스템은 Python으로 개발된 Azure Functions를 통해 구현된다. 이 함수는 Timer 트리거로 주기적으로 실행되며, 재난문자 API 호출, Blob Storage를 통한 ID 관리, Event Hub 및 Teams 웹훅을 통한 알림을 수행한다. Functions App은 모든 함수 코드를 `function_app.py` 파일 내에 정의하고, Python V2 앱 모델의 데코레이터를 사용하여 트리거와 바인딩을 선언한다.






##### 웹훅 알림 함수 (`send_teams_webhook`)
코드를 모듈화하고 재사용성을 높이기 위해 Teams 웹훅으로 메시지를 전송하는 헬퍼 함수를 별도로 정의했다.
이 함수는 주어진 텍스트 메시지를 설정된 웹훅 URL로 POST 요청을 보낸다.

```
import logging
import os
import json
import datetime
import requests
from azure.storage.blob import BlobServiceClient
import azure.functions as func

# --- 웹훅 알림 헬퍼 함수 (재사용성 및 간결성 확보) ---
# 이 함수는 메시지를 Teams 웹훅으로 전송.
def send_teams_webhook(message_text: str) -> None:
    logging.info(f"Teams 웹훅 알림 요청: '{message_text[:50]}...'")
    try:
        webhook_url = os.environ.get("AzureWebHookUrl")
        if not webhook_url:
            logging.warning("Teams 웹훅 URL이 환경 변수에 설정되어 있지 않습니다. 알림을 건너뜀.")
            return
        response = requests.post(webhook_url, json={"text": message_text})
        response.raise_for_status()
        logging.info(f"Teams 웹훅 실행 결과: {response.status_code}")
    except Exception as e:
        logging.error(f"Teams 웹훅 전송 중 오류 발생: {e}")

# --- 재난문자 감지 스케줄러 함수 (`main` 함수) ---
# 매 5분마다 실행되며, Event Hubs로 데이터를 보내고 Teams에 알림을 보냅니다.
@app.timer_trigger(schedule="0 */5 * * * *", arg_name="timer", run_on_startup=True, use_monitor=False)
@app.event_hub_output(arg_name="event", event_hub_name=os.environ["EventHubName"], connection="EventHubConnectionString")
def disaster_message_scheduler(timer: func.TimerRequest, event: func.Out[str],
                               latest_disaster_id_input: func.InputStream, # Blob Storage에서 최신 ID 읽기
                               latest_disaster_id_output: func.Out[str],   # Blob Storage에 최신 ID 쓰기
                               webhook_output: func.Out[str]                 # 팀 웹훅으로 알림 보내기
                               ):
    logging.info('재난문자 감지 스케줄러 시작되었습니다.')

    # 1. Blob Storage에서 이전 처리 ID 로드 (latest_disaster_id_input 사용)
    # 2. 재난문자 API 호출 (requests 라이브러리 사용)
    # 3. 새로운 메시지 필터링 및 처리 (이전 ID와 비교)
    # 4. 새로운 메시지 전송 (Event Hubs 출력 바인딩 'event' 사용)
    # 5. Teams로 새로운 메시지 알림 (webhook_output 바인딩 사용, send_teams_webhook 호출)
    # 6. Blob Storage에 마지막 처리 ID 저장 (latest_disaster_id_output 사용)

    logging.info('재난문자 감지 스케줄러 종료되었습니다.')
```

##### 바인딩 정의 ()

```
```



![](/assets/images/posts/create_eventHub_ns1.png)

![](/assets/images/posts/create_eventHub1.png)


![](/assets/images/posts/create_storage1.png)


![](/assets/images/posts/create_blobStorage1.png)





![](/assets/images/posts/create_webHook1.png)

![](/assets/images/posts/create_webHook2.png)







![](/assets/images/posts/create_webHook3.png)





![](/assets/images/posts/crete_streamAnalytics1.png)



![](/assets/images/posts/crete_streamAnalytics2.png)

##### 3.2 함수 코드 작성

##### 3.3 Azure에 배포 및 모니터링
