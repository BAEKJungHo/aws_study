# AWS

- [AWS API Gateway](https://aws.amazon.com/ko/api-gateway/)
- [Serverless API Gateway](https://www.serverless.com/framework/docs/providers/aws/events/apigateway)
- [AWS Lambda](https://aws.amazon.com/ko/getting-started/hands-on/run-serverless-code/)

# IaaS, PaaS, FaaS

- IaaS(EC2, VM Instance 등)를 사용하여 Tomcat, JBoss 등의 WAS 배포를 통한 운영
- PaaS(ElastickBeansTalk 등)를 사용하여 war 혹은 jar 파일의 배포를 통한 운영
- FaaS(Lambda, Functions 등)를 사용하여 코드 배포를 통한 운여
  - API Gateway 를 사용하여 REST API URI 를 잡아줘야 한다.
  - 비지니스 로직이 담겨져 있는 코드들만 들어있다. 즉, 함수의 이름과 로직만 담겨져있다.
  - 따라서, 해당 코드가 어느 URI 를 타야하는지에 대한 정보가 없기 때문에 이에 대한 URI 주소를 매겨줘야 한다.
  - API Gateway 는 이런 URI 를 하나로 통합하는 역할을 맡게 된다.

# IAM(Identity and Access Management)

IAM(Identity and Access Management)은 유저를 관리하고 접근 레벨 및 권한에 대한 관리할 수 있는 웹 서비스.

> AWS 리소스에 대한 액세스를 안전하게 제어할 수 있는 웹 서비스입니다.

## Root User

- AWS 계정을 처음 생성할 때는 해당 계정의 모든 AWS 서비스 및 리소스에 대한 완전한 액세스 권한을 지닌 통합 인증(SSO) 자격 증명으로 시작할 수 있다. 
- 이 자격 증명은 AWS 계정 루트 사용자라고 한다.
- 계정을 생성할 때 사용한 이메일 주소와 암호로 로그인하여 액세스한다. 
- 일상적인 작업, 심지어 관리 작업의 경우에도 루트 사용자를 사용하지 않는 것을 강력히 권장한다. 

## 특징

- 접근키(Access Key), 비밀키(Secret Access Key)
- 매우 세밀한 접근 권한 부여 기능 (Granular Permission)
- 비밀번호를 수시로 변경 가능케 해줌
- Multi-Factor Authentication(다중 인증) 기능

```
- 그룹 (Group)
- 유저 (User)
- 역할 (Role)
- 정책 (Policy) 

- (`*`) 정책은 그룹, 역할에 추가시킬 수 있다.
- (`*`) 하나의 그룹 안에 다수의 유저가 존재 가능하다.
```

# EC2(Elastic Compute Cloud) 

- Amazon Web Services(AWS) 클라우드에서 `확장 가능 컴퓨팅 용량`을 제공한다. 
- Amazon EC2 를 사용하면 하드웨어에 선투자할 필요가 없어 더 빠르게 애플리케이션을 개발하고 배포할 수 있다.
- Amazon EC2 를 사용하여 원하는 수의 가상 서버를 구축하고 보안 및 네트워킹을 구성하며 스토리지를 관리할 수 있다.
- Amazon EC2 에서는 확장 또는 축소를 통해 요구 사항 변경 또는 사용량 스파이크를 처리할 수 있으므로 트래픽을 예측할 필요성이 줄어든다.

## 특징

- 인스턴스를 켜고 끌 수 있으며, 켜진 상태에서만 돈을 지불하면 된다.

## 다양한 지불 방법

- On-demand: 시간 단위로 가격이 고정되어 있음
  - 오랜시간동안 선불을 내지 않고 최소한의 비용을 지불하여 EC2 인스턴스를 사용하고 싶을때, 특히 앱/프로그램 개발시 최초로 EC2 인스턴스에 deploy 할때 매우 유용  
- Reserved: 한정된 EC2 용량 사용 가능, 1-3년동안 시간별로 할인 적용 받을 수 있음
  - 안정된, 예상 가능한 workload 시 Reserved 사용 권장, 선불로 인한 컴퓨팅 비용 대폭 감소 
- Spot: 입찰 가격 적용. 가장 큰 할인률을 적용받으며 특히 인스턴스의 시작과 끝기간이 전혀 중요하지 않을때 매우 유용
  - 단순히 비용 절감 시 유용함. 인스턴스의 시작/끝시점에 구애받지 않을 경우 권장 

## EBS(Elastic Block Storage)

- EC2 를 사용하기 위해 EBS 라는 디스크 볼륨을 요구한다.
-  저장 공간이 생성되어지며 EC2 인스턴스에 부착된다.
- 디스크 볼륨 위에 File System 이 생성된다
- EBS 는 특정 Availability Zone(AZ) 에 생성된다
  - 한쪽 서버가 다운된 경우, AZ Backup 을 통해 서비스 제공을 가능하게 해주는 `Disaster Recovery` 라고 한다.
  - ![aws ebs](https://user-images.githubusercontent.com/47518272/160271048-2383829b-c109-4a38-a336-577536b97c62.png)
   
### EBS 볼륨 타입

- __SSD 군__
  - General Purpose SSD (GP2): 최대 10K IOPS를 지원하며 1GB당 3IOPS 속도가 나옴
  - Provisioned IOPS SSD (IO1) : 극도의 I/O률을 요구하는(예시 : 매우 큰 DB관리) 환경에서 주로 사용됨. 10K 이상의 IOPS를 지원함
- __Magnetic/HDD 군__
  - Throughput Optimized HDD (ST1) : 빅데이터 Datawarehouse, Log 프로세싱시 주로 사용 (boot volume으로 사용 가능 X)
  - CDD HDD (SC1) : 파일 서버와 같이 드문 volume 접근시 주로 사용, 역시 boot volume으로 사용 불가능하나 비용은 매우 저렴함
  - Magnetic (Sandard) : 디스크 1GB당 가장 싼 비용을 자랑함. Boot volume 으로 유일하게 가능함

## ELB(Elastic Load Balancers)

- 수많은 서버의 흐름을 균형있게 흘려보내는데 중추적인 역할을 함
- 하나의 서버로 traffic 이 몰리는 병목현상(bottleneck) 방지
- Traffic 의 흐름을 `Unhealthy instance -> healthy instance` 로

### 특징

- __Application Load Balancer : OSI Layer7 에서 작동됨__
  - HTTP, HTTPS 와 같은 traffic 의 load balancing 에 가장 적합함
  - 고급 request 라우팅 설정을 통하여 특정 서버로 request 를 보낼 수 있음
- __Network Load Balancer : OSI Layer4 에서 작동됨, 매우 빠른 속도를 자랑하며 Production 환경에서 종종 쓰임__
  - 극도의 performance 가 요구되는 TCP traffic에서 적합함
  - 초당 수백만개의 request를 아주 미세한 delay 로 처리 가능
- __Classic Load Balancer : 현재 Legacy 로 간주됨, 따라서 거의 쓰이지 않음__
  - Layer7의 HTTP/HTTPS 라우팅 기능 지원
  - Layer4의 TCP traffic 라우팅 기능도 지원

### Load Balancer Error : 504 ERROR

504 Gateway Time-out

### X-Forwarded-For 헤더

![elb](https://user-images.githubusercontent.com/47518272/160271238-e486ecec-65ec-4432-9cac-c52e2cdde63c.png)

- EC2 는 Priavte IP Address 밖에 볼 수 없음
- 이때, X-Forwarded-For Header 를 통해 Public IP Address 를 얻을 수 있음

# Lambda

- Serverless 의 주축을 담당
- Events 를 통하여 Lambda 를 실행시킴
- NodeJS, Python, Java, GO 등 다양한 언어 지원
- Lambda Function

## 비용

- Lambda Function이 실행될때만 돈 지불
- 매달 1.000.000 함수 호출 시 무료 (그 후로는 유료)

## 기타

- 최대 300초(5분) 런타임 시간 허용
- 512MB의 일시적인 디스크 공간 제공 (/tmp/)
- 최대 50MB Deployment Package 허용

## 사용 예

- `S3 -> Lambda -> DB`
- `IoT -> Lambda -> SNS`

# S3(Simple Storage Service)

- 안전하고 가변적인 Object 저장공간을 제공 (ex: Google Cloud)
- 편리한 UI 인터페이스를 통해 어디서나 쉽게 데이터를 저장하고 불러올 수 있음
- 파일 크기는 0KB 부터 5TB 까지 지원
- 저장공간 무제한
- Bucket 이라는 이름을 사용함 (디렉토리와 유사함)
- Bucket 은 보편적인 namespace 를 사용함

## 구성 요소

- Key
- Value
- Version ID
- Metadata
- CORS (Cross Origin Resource Sharing)

## S3 Data Consistency Model

- Read after Write Consistency(PUT)
- Eventual Consistency(UPDATE, DELETE)

## S3 스토리지

- __일반 S3__
  - 가장 보편적으로 사용되는 스토리지 타입
  - 높은 내구성, 가용성 (Durability, Availability)   
- __S3 - IA (Infrequent Access)__
  - 자주 접근되지는 않으나 접근시 빠른 접근이 요구되는 파일이 많을 시 유용
  - 일반 S3 에 비해 비용은 저렴하나 접근시 추가 비용 발생
  - 멀티 AZ 를 통한 데이터 저장 
- __S3 - One Zone IA__
  - 단일 AZ를 통한 데이터 저장
  - 단일 AZ에 의한 데이터 접근 제한 (조금 낮은 가용성)
  - 데이터 접근시 S3 - IA보다 20% 비용 저렴
- __Glacier__
  - 거의 접근하지 않을 데이터 저장 시 유용
  - 매우 저렴한 비용
  - 데이터 접근시 대략 4-5시간 소요
- __Intelligent Tiering__
  - 데이터 접근 주기가 불규칙할때 매우 유용
  - 2가지 티어 존재
    - Frequent Tier
    - Infrequent Tier
  -  데이터 접근주기에 따라 두가지 티어중 하나로 선택됨
  - Frequent Tier가 비용이 약간 더 비쌈
  - 최고의 비용 절감 효율을 누릴 수 있음 

## S3 요금

- GB 당
- PUT, GET, COPY 요청 횟수당
- 데이터 다운로드시 / 다른 리소스로 전송시
- Metadata (object tag)

## References

- Inflearn. AWS 입문자를 위한 강의
- https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/introduction.html
