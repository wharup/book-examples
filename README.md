# 예제 코드
다음은 [마이크로서비스 아키텍처 구축 가이드]에 수록된 예제 코드에 대한 안내입니다.

#### 1. 관련 프로젝트
*	[microservices-example-sql-vs-api](https://github.com/wharup/microservices-example-sql-vs-api/tree/main)
    - 3챕터의 모놀리식 시스템과 마이크로서비스 시스템의 구현 코드
    - 테스트에 사용된 DB 스키마와 샘플 데이터를 생성하는 기능
*	[microservices-example-api-composition](https://github.com/wharup/microservices-example-api-composition/tree/main)
    - 7챕터의 API Composition 구현 코드
*	[microservices-example-common-service](https://github.com/wharup/microservices-example-common-service/tree/main)
    - 위 2개 프로젝트에서 연계하는 공통 서비스
*	[microservices-example-transactions](https://github.com/wharup/microservices-example-transactions)
    - 7챕터의 보상 트랜잭션 관련 코드

![프로젝트 관계도](https://github.com/wharup/book-examples/blob/main/%EA%B4%80%EA%B3%84%EB%8F%84.png "title") 


#### 2. 챕터별 코드 위치

#### Chapter 3 : 데이터베이스를 분리한다고?
##### 질문2 : REST API 참조로 속도가 나오겠어?
모놀리식과 마이크로서비스 아키텍처의 데이터 조회 속도 비교
*   코드 3-4 모놀리식 서비스의 데이터 조합 : MonolithServiceRequestService
    - [MonolithServiceRequestService.findAllBySQL()](https://github.com/wharup/microservices-example-sql-vs-api/blob/557390dcca7514f65a110007a94e94f064982e77/src/main/java/microservices/examples/service/MonolithServiceRequestService.java#L23)
*   코드 3-7 일괄 요청 시의 데이터 조합 : ServiceRequestService
    - [ServiceRequestService.findAllWithBatchRESTApi()](https://github.com/wharup/microservices-example-sql-vs-api/blob/557390dcca7514f65a110007a94e94f064982e77/src/main/java/microservices/examples/service/ServiceRequestService.java#L88)
*   코드 3-8 일괄 요청 & 로컬 캐시를 사용한 데이터 조합 :
    - [ServiceRequestCachedService.findAllWithBatchRESTApi()](https://github.com/wharup/microservices-example-sql-vs-api/blob/557390dcca7514f65a110007a94e94f064982e77/src/main/java/microservices/examples/service/ServiceRequestCachedService.java#L121)

#### Chapter 7 : 서비스 개발하기	
##### 7.2 서비스 간 데이터 참조 가이드
*   코드 7-3 코드 서비스의 공통 코드 조회:
*   코드 7-4 ServiceRequestService의 상담 이력 조회 메서드
*   코드 7-5 부가 정보의 조회
*   코드 7-6 CustomerGateway 클래스의 고객 이름 조회 메서드
*   코드 7-9 CodeGateway의 코드 이름 조회 메서드
*   코드 7-11 CodeGateway의 캐시 갱신 메서드
*   코드 7-12 CodeGateway의 공통 코드 조회 코드
*   코드 7-13 공통 서비스 CodeContoller의 코드 조회 요청 처리 코드

##### 7.3 트랜잭션 관리 : 원자성과 독립성

*   코드 7-14 교육 과정 생성 코드(비관적 잠금)
    - [CourseService.createCourse()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L52)
*   코드 7-15 낙관적 잠금을 활용한 교육 과정 생성 코드
    - [CourseService.createCourseOptimisticLocking_manyTryCatchBlocks()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L203)
*   코드 7-16 낙관적 잠금을 활용한 교육 과정 생성 코드 – 리팩터링
    - [CourseService.createCourseOptimisticLocking_oneTryCatchBlock()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L80)
*   코드 7-17 추출된 보상 트랜잭션 메서드
    - [CourseService.compensateSaveCourse()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L178)
    - [CourseService.compensateAddManager()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L186)
    - [CourseService.rollbackTransaction()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L170)
*   코드 7-23 커밋 순서 변경 예시
    - [CourseService.createCourseOptimisticLocking_shortTransactionSpan()](https://github.com/wharup/microservices-example-transactions/blob/0cf070bfb7736265e336cec79fb7355a80378475/src/main/java/microservices/examples/tx/course/CourseService.java#L125)


#### 3. 기타
자바 모듈화 규칙으로 실행 시 다음 JVM 옵션이 필요합니다.(Lombok, EhCache 관련)

--illegal-access=warn --add-opens java.base/java.lang=ALL-UNNAMED

 
