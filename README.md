# 일루와 서비스 계획

![intro](https://user-images.githubusercontent.com/12987271/110209548-8b484a00-7ed0-11eb-8141-f5a341d009cf.png)

일루와
-----

#### 계획 내용

- 사업계획서
- 서비스흐름
- 서비스모델
- 기술스택
- 개발비용
- 진행사항

# 사업계획서

첨부된 ppt 및 계획서파일 확인

# 서비스흐름

#### 주문

![orderflow](https://user-images.githubusercontent.com/12987271/110209496-40c6cd80-7ed0-11eb-8581-f8ad660a132e.png)

# 서비스모델

![illuwa](https://user-images.githubusercontent.com/12987271/110208685-fcd1c980-7ecb-11eb-86c6-a7075f8264ea.png)

#### 인증서버 : 회원들의 ID, PW, 닉네임, 이메일, 권한 등의 정보를 저장 및 확인하는 서비스이다

- 도메인모델 - 회원(회원ID, ID, PW, 닉네임, 이메일, 전화번호, 분류, 인증여부)
- 요구기능 - 회원가입 및 정보 확인, 인가기능
- 추 후 발전 - Google, Facebook, Kakao의 OAuth2사용한 간편한 회원가입

#### 이미지서버 : 포차 게시글, 리뷰 등의 사용될 이미지를 저장하는 서비스이다

- 도메인모델 - 이미지(이미지ID, 이미지이름, 경로)
- 요구기능 - 이미지 조회 및 등록
- 특이사항 - 이미지 이름은 겹쳐선 안되기 때문에 UUID를 이용

#### 결제서버 : 결제정보를 저장 및 외부결제API와 통신하는 서비스이다

- 도메인모델 - 결제(결제ID, 결제종류 - 그에맞는 방식들~)
- 요구기능  결제정보(카드번호 등) 등록 및 수정 및 확인, 외부결제API와 통신해 결제여부 리턴

#### 주문서버 : 어떤 고객이 어떤 포차에서 어떤음식을 총 몇개 주문했는지에대한 정보를 저장하는 서비스이다

- 도메인모델 - 주문(주문ID, 고객ID, 포차ID, 상품리스트, 주문상태), 상품(상품ID, 상품제목, 상품가격, 상품개수)
- 요구기능 - 주문정보 생성 및 조회, 모든 주문 목록 확인, 주문 취소
- 연관도메인 - 주문확인전 결제서버를 통해 결제정보를 받아온다

#### 포차서버 : 포장마차의 기본적인 정보, 음식정보들을 등록할 수 있으며, 리뷰 확인 및 답변, 월말정산과 결제내역을 볼 수 있으며 포차의 전반적인 부분을 담당한다

- 도메인모델 - 포차(포차ID, 포차이름, 포차설명, 포차대표이미지, 포차공지, 음식리스트, 영업시간), 음식(음식ID, 음식이름, 음식설명, 가격), 주문내역리스트(주문ID, 포차ID, 주문정보)
- 요구기능 - 포차등록 및 조회, 리뷰확인 및 답글, 판매내역 및 월말정산, 주문목록
- 연관도메인 - 리뷰서버를 통해 리뷰정보를 받아옴, 주문서버에서 주문생성시 포차서버로 해당주문내역이 넘어온다, 주문완료시 해당 주문내역상태 변경

#### 리뷰서버 : 고객들이 음식을 먹고 난 뒤 해당 포차에대해 리뷰를 남길 수 있으며 이에 포차업주분께서 답글을 달 수 있는 서비스이다

- 도메인모델 - 리뷰(리뷰ID, 포차ID, 작성자, 별점[1~5], 내용, 공개여부, 등록시간)
- 요구기능 - 리뷰작성 및 삭제, 업주의 답글 및 삭제, 리뷰 페이징 처리, 통계부분(최근 리뷰개수, 총 별점개수)

#### 알림서버 : 고객들에게 알림(푸쉬메시지, 이메일 등)을 전달해 주는 서비스이다

- 도메인모델 - 알림(알림ID, 알림제목, 알림내용, 수신자, 송신자)
- 요구기능 - 알림 전달 및 확인 및 삭제

#### 위치서버 : 포장마차들의 실시간 위치를 알려주는 서비스이다

- 도메인모델 - 위치(위치ID, 포차ID, 포차이름, 경도, 위도)
- 요구기능 - 포차들의 실시간 위치 확인 및 변동사항 적용

# 기술스택

기술 | 설명
--- | ---
**Arduino** | 카드리더기, 포스기 등의 역할을 위해 아두이노를 이용할 예정이다
**ReactNative** | Android와 IOS를 지원하기 위해 크로스플랫폼을 이용할 예정이다
**Node.js** | GraphQL을 이용해 API게이트웨이 서버 구축 예정이다
**SpringBoot** | 서비스들은 부트를 이용해 서버 구축 예정이다
**Apache Kafka** | IPC통신용을 위해 사용할 예정이다
**MariaDB** | RDB로 사용할 예정이다
**Aamzon WebService** | 클라우딩서비스를 이용해 서버를 운영할 예정이다
**Docker** | 서버를 구동하기위해 사용할 예정이다 ( AWS과 호환성 확인 필요 )
**DynamoDB** | NoSQL로써 사용할 예정이다 ( 확정 x )
**Redis** | 캐싱서버로써 이용할 예정이다 ( 확정 x )

# 개발비용

**현재 책정된 비용은 단순 개발 비용으로써 약 2달정도의 시간을 먼저 예측해봤습니다**

* 도메인 등록(Route53, .com) 12(1년) x 2(S3버켓, ELB용) = 24달러
* S3버켓(30GB) 0.023 x 30(용량) = 0.69달러
* RDS db.t3.micro(CPI1코어, 메모리1기가) 0.026 x 24(시간) x 60(일) = 37.44달러
* DB저장공간(SSD20GB) 20(용량) x 0.131 x 2(달) = 5.24달러
* t2.small(메모리2GB) 0.0288 x 24(시간) x 60(일) = 41.472달러 (EC2 1대기준으로 추후 추가될 수 있다)

* 총 금액 : 약 122,798(원)

# 
