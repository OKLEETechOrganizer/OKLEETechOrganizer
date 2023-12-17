# TECH INFO

## 목차
1. [FRONT](#FRONT)
   1. [JavaScript](#JavaScript)
   2. [Package Manager](#Package-Manager)
   3. [Framework](#Framework)
   4. [Type Checkers](#Type-Checkers)
   5. [Server Side Rendering](#Server-Side-Rendering)
   6. [Mobile Applications](#Mobile-Applications)
2. [BACK](#BACK)
   1. [Language](#Language)
   2. [Framework BackEnd](#Framework-BackEnd)
   3. [NoSQL](#NoSQL)
3. [DEVOPS](#DEVOPS)
   1. [Cloud Providers](#Cloud-Providers)
   2. [SERVERLESS](#SERVERLESS)

## FRONT
### JavaScript
- 일반 함수과 화살표 함수에서 this의 차이
  - 일반 함수는 자신이 종속된 객체를 this로 가리키며, 화살표 함수는 종속된 인스턴스를 가리킨다.
    ```
    function BlackDog() {
      this.name = '흰둥이';
      return {
        name: '검둥이',
        bark: function() {
          console.log(this.name + ': 멍멍!');
        }
      }
    }
    
    const blackDog = new BlackDog();
    blackDog.bark(); // 검둥이: 멍멍!
    
    function WhiteDog() {
      this.name = '흰둥이';
      return {
        name: '검둥이',
        bark: () => {
          console.log(this.name + ': 멍멍!');
        }
      }
    }
    
    const whiteDog = new WhiteDog();
    whiteDog.bark(); // 흰둥이: 멍멍!
    ```
- 화살표 함수는 따로 {}를 열어 주지 않으면 연산한 값을 그대로 반환한다는 의미이다.
  ```
  const triple = (value) => value * 3;
  ```
- 자바스크립트에서 함수는 일급 객체다. 즉, 객체를 다루듯이 함수를 변수에 할당하거나, 함수를 다른 함수로
  전달하거나, 함수에서 함수를 반환하거나, 객체와 프로토타입에 할당하거나, 함수에 프로퍼티를 기록하거나,
  함수에 기록된 프로퍼티를 읽는 등의 작업을 할 수 있다.

- 비동기 처리
  - 자바스크립트는 런타임에서 싱글 스레드로 동작하기 때문에 비동기 처리를 위해서는 콜백(callback), 프로미스(promise), 어싱크 어웨이트(async await) 방식을 사용한다.
  - 콜백
    - 함수의 파라미터로 함수를 전달
    - 가독성이 좋지 못하여 유지보수 및 디버깅이 힘들다.
  - 프로미스
    - 비동기 작업이 완료되면 결과를 반환하는 객체
    - then(), catch() 메서드를 사용하여 성공과 실패에 대한 처리가 가능하다.
  - 어싱크 어웨이트
    - 프로미스를 사용하는 비동기 작업을 동기적으로 처리하는 것처럼 코드를 작성할 수 있다.
    - async가 붙어 있는 함수를 실행할 때 await 키워드를 사용하여 비동기 작업이 완료될 때까지 기다릴 수 있다.
    - ```
      async function myName() {
        return "Andy";
      }
      
      async function showName() {
        const name = await myName(); // await는 promise 객체인 myName() 함수의 실행이 끝나길 기다린다.
        console.log(name);
      }
      
      console.log(showName());
      ```
<hr />

### Package-Manager
- 패키지 매니저는 프로젝트에 필요한 의존성 패키지를 관리하는 프로그램을 의미한다.
  - 의존성 패키지는 해당 프로젝트를 실행하는 데 꼭 필요한 라이브러리와 모듈들이다.
#### npm
- npm은 자바스크립트용 패키지 매니저이다. 유저가 만든 패키지를 등록하는 저장소를 의미하기도 하고
  CLI를 의미 하기도 한다. Node.js를 설치할 때 함께 설치된다.

#### yarn


<hr />

### Framework
#### React
- JSX 코드는 브라우저에서는 직접 해석할 수 없으므로, 웹팩에 의해 자바스크립트 코드로 변환된다.
  이때, JSX로 구현된 컴포넌트는 자바스크립트의 객체로 표현된다. 변환된 자바스크립트 코드를
  브라우저가 읽어서 실행하고 화면을 그리기 시작한다.
- 리액트에서 DOM 요소에 스타일을 적용할 떄는 문자열 형태로 넣는 것이 아니라 객체 형태로
  넣어 주어야 한다. 스타일 이름 중에서 background-color처럼 - 문자가 포함되는 이름이 있으면,
  하이픈(-) 문자를 없애고 카멜 표기법으로 작성해야 한다.
- component
  - 라이프사이클 메서드 흐름
    <img alt="Component_lifecycle_method_flow" src="front/framework/react/Component_lifecycle_method_flow.png">
- Hooks
  - 상태 훅
    - useState
    - useEffect
    - useReducer
      - userReducer()의 반환값 배열의 첫 번째는 현재 상태, 두 번째는 dispatch 함수이다.
        dispatch 함수에 action을 전달함으로써 상태를 업데이트할 수 있다.
      - reducer가 현재 상태와 action을 기반으로 다음 상태를 결정한다.
      ```
      impport {useReducer} from 'react';
      
      function reducer(state, action) {
        // action.type에 따라 다른 작업 수행
        switch (action.type) {
          case 'INCREMENT':
            return { value: state.value + 1 };
          case 'DECREMENT':
            return { value: state.value - 1 };
          default:
            // 아무것도 해당되지 않을 떄 기존 상태 반환
            return state;
        }
      }
      
      const Counter = () => {
        const [state, dispatch] = useReducer(reducer, { value: 0 });
      
        return (
          <div>
            <p>
              현재 카운터 값은 <b>{state.value}</b>입니다.
            </p>
            <button onClick={() => dispatch({ type: 'INCREMENT' })}>+1</button>
            <button onClick={() => dispatch({ type: 'DECREMENT' })}>-1</button>
          </div>
        );
      };
      ```
      - useReducer를 사용했을 때의 가장 큰 장점은 컴포넌트 업데이트 로직을 컴포넌트 바깥으로
        빼낼 수 있다는 점이다.
  - 메모이제이션 훅
    - useCallback
    - useMemo

<hr />

### Type Checkers
#### TypeScript
- arrow function의 경우 다음과 같이 타입을 지정한다.
  ```
  (인수명: 인수_타입): 반환값_타입 => 자바스크립트_식
  let sayHello = (name: string): string => `Hello ${name}`
  ```

<hr />

### Server Side Rendering
#### Next.js
- Next.js에서는 애플리케이션 안의 다른 페이지로의 이동하기 위한 Link 컴포넌트가 있다.

<hr />

### Mobile Applications
#### React Native
- Component
  - 유저 인터페이스를 구성하는 요소
  - 컴포넌트 생성
    - ```
      const App = () => { 
        return (
          <SafeAreaView>
          </SafeAreaView>
      )} 
      ```
    - Props(Properties)를 설정하여 컴포넌트에 전달할 수 있다.
    - JSX 문법
      - 태그를 열면 반드시 닫아주기 `<Text></Text>`
      - 스스로 닫는 태그 사용하기   `<Text />`
      - 반환할 때 반드시 하나의 태그로 감싸기
      - JSX 안에서 자바스크립트 표현식을 보여줄 땐 중괄호 사용
    
- Hooks
  - useState
    - 상태 값을 관리하는 함수
    - `const [visible, setVisible] = useState(true)`
- Context API
  - 컴포넌트 사이에 공유되는 데이터를 위해 매번 공통 부모 컴포넌트를 수정하고 모든 컴포넌트에 
    Props를 전달하여 데이터를 사용하는 과정은 비효율적이다. 이처럼 비효율적인 문제를 해결하기 위해 
    리액트에서는 Flux라는 개념을 도입하였고, 그에 걸맞은 Context API를 제공하기 시작했다.
  - Context는 부모 컴포넌트로부터 자식 컴포넌트로 전달되는 데이터의 흐름과는 상관없이, 전역적으로
    사용되는 데이터를 다룬다.
  - Context를 사용하기 위해서는 Context Api를 사용하여 Context의 프로바이더(Provider)와
    컨슈머(Consumer)를 생성한다.
  - Context에 저장된 데이터를 사용하기 위해서는 공통 부모 컴포넌트에 Context의 프로바이더를 사용하여
    데이터를 제공하다. 그리고 데이터를 사용하려는 컴포넌트에서 Context의 컨슈머를 사용하여 실제
    데이터를 사용(소비)한다.
- AsyncStorage
  - 리액트에서 데이터를 다루는 Props와 State, Context는 휘발성이다. 이 데이터는 메모리에서만 존재하며, 
    물리적으로 데이터를 저장하지 않는다. 따라서 데이터들은 API를 통해 서버에 저장하여 사용하거나, 앱 내에 
    저장하여 사용하는 경우가 많다.
  - AsyncStorage는 앱 내에서 간단하게 데이터를 저장할 수 있는 저장소이다.
  - 웹에서 사용하는 windows.localStorage와 매우 유사하다.
  - AsyncStorage는 키 값 저장소로서 간단하게 앱 내에 데이터를 저장하기 위해 사용할 수 있다.

<hr />

## BACK
### Language
#### Node.js
- Node.js는 자바스크립트 코드 실행에 필요한 런타임으로 V8 엔진을 사용하고, 자바스크립트 런타임에
  필요한 이벤트 루프 및 운영체제 시스템 API를 사용하는 데는 libuv 라이브러리를 사용한다.
- Node.js의 장단점
  <img src="back/language/nodejs/node_pros_and_cons.png">
- node에서 mongoose를 사용할 시, 쿼리에 필터를 빈 객체인 {}로 넣으면 모든 값을 불러오게 되어서
  문제가 되는 경우가 있다. 이 경우 에러를 내도록 하는 설정이 strictQuery 설정이다. Mongoose6에서는
  기본값이 true이며 7에서는 false이다. 명시적으로 설정해주지 않으면 서버 기동 시 경고가 발생한다.
  ```
  const mongoose = require("mongoose");
  
  mongoose.set("strictQuery", false);
  ```

#### Java
- 자료구조
  - 배열과 리스트
    - 배열
      - 배열은 메모리의 연속 공간에 값이 채워져 있는 형태의 자료구조
      - 인덱스를 사용하여 값에 바로 접근 가능
      - 새로운 값을 삽입하거나 특정 인덱스에 있는 값을 삭제하기 어려움
      - 배열의 크기는 선언할 때 지정하며, 한 번 선언하면 크기를 늘리거나 줄일 수 없음
    - 리스트
      - 값과 포인터를 묶은 노드를 포인터로 연결한 자료구조
      - 인덱스가 없음
      - 포인터로 연결되어 있어 데이터를 삽입하거나 삭제하는 연산 속도가 쁘름
      - 크기가 가변적
  - 스택과 큐
    - 스택
      - 삽입과 삭제 연산이 후입선출(Last-in First-out)
      - push : top 위치에 새로운 데이터 삽입
      - pop : top 위치에 현재 있는 데이터를 삭제하고 확인
      - peek : top 위치에 현재 있는 데이터를 단순 확인
    - 큐
      - 삽입과 삭제 연산이 선입선출(First-in First-out)
      - add : rear 위치에 새로운 데이터 삽입
      - poll : front 위치에 있는 데이터를 삭제하고 확인
      - peek : front 위치에 있는 데이터를 단순 확인
      - 우선순위 큐 (Priority Queue) : 값이 들어간 순서와 상관 없이 우선순위가 높은 데이터가 먼저 나오는 자료구조

<hr />

### Framework BackEnd
#### EXPRESS
- HTTP에서 Body를 파싱하려면 bodyParser.json() 미들웨어를 추가해야 한다.
  ```
  const express = require("express");
  const bodyParser = require("body-parser");
  
  const app = express();
  app.use(bodyParser.json());
  ```
- EXPRESS에서의 3계층 아키텍처
  <img alt="Component_lifecycle_method_flow" src="back/frameworkbackend/express/three_layer_architecture.png">
- 미들웨어
  - 익스프레스에서 미들웨어란 HTTP 요청과 응답 사이에 함수를 추가하여 새로운 기능을 추가하는 것을
    뜻한다.
<hr />

#### NestJS
- 익스프레스와 NestJS 비교
  <img alt="Component_lifecycle_method_flow" src="back/frameworkbackend/nestjs/express_vs_nestjs.png">
- NestJS의 핵심 기능으로 의존성 주입을 들 수 있다. 의존성 주입은 모듈 간의 결합도를 낮춰서 코드의
  재사용을 용이하게 한다. 즉, 모듈 내에서의 코드의 응집도는 높여서 모듈의 재사용을 꾀하고 모듈
  간에는 결합도를 낮춰서 다양한 아키텍처에서 활용할 수 있게 해준다. 이를 위한 장치들로 모듈, 가드,
  파이프, 미들웨어, 인터셉터 같은 모듈과 코드의 의존 관계를 구성하는 프로그래밍적 장치들이 있다.
- NestJS에서는 HTTP 요청을 보통 가드 -> 인터셉터 -> 파이프 -> 컨트롤러 -> 서비스 -> 리포지토리
  순서로 처리한다.

<hr />

### NoSQL
#### MongoDB


<hr />

## DEVOPS
### Cloud Providers
#### AWS
- AWS ECR
  - 도커 이미지 파일을 pull, push 할 수 있는 컨테이너 이미지 저장소이다.
- AWS ECS
  - 컨테이너화된 애플리케이션을 쉽게 배포, 관리, 스케일링할 수 있도록 도와주는 완전 관리형 컨테이너 오케스트레이션 서비스이다.
  - 구성요소
    - 용량
      - 컨테이너가 실행되는 인프라
      - 옵션
        1. AWS EC2 인스턴스
        2. AWS Fargate
        3. 온프레미스 가상머신(VM) 또는 서버
    - 컨트롤러
      - 컨테이너에서 실행되는 애플리케이션을 배포하고 관리
    - 프로비저닝
      - 스케줄러와 함께 애플리케이션 및 컨테이너를 배포 및 관리하는 데 사용할 수 있는 도구
      - 옵션
        1. AWS Management Console
        2. AWS Command Line Interface
        3. AWS SDK
        4. Copilot
        5. AWS CDK

<hr />

### SERVERLESS
#### AWS LAMBDA
- Lambda기본
  - Lambda는 빠르게 스케일 업해야 하고 수요가 없을 때는 0으로 스케일 다운해야 하는 애플리케이션 시나리오에 이상적인 컴퓨팅 서비스이다.
  - 개념
    - 함수
      - 함수는 Lambda에서 코드를 실행하기 위해 호출할 수 있는 리소스이다.
    - 트리거
      - 트리거는 Lambda에서 함수를 호출하는 리소스 또는 구성이다.
    - 이벤트
      - 이벤트는 처리할 Lambda 함수에 대한 데이터가 포함된 JSON 형식 문서이다.
    - 실행환경
      <img alt="Execution_environment" src="devops/serverless/aws_lambda/Execution_environment.png">
      - 함수의 런타임은 런타임 API를 사용하여 Lambda와 통신한다. 익스텐션은 익스텐션 API를 사용하여
        Lambda와 통신한다. 또한 확장은 텔레메트리 API를 사용하여 함수의 로그 메시지와 기타 텔레메트리
        데이터를 수신할 수 있다.
  - Lambda 배포 패키지
    - .zip 파일 아카이브
      - Lambda 콘솔 사용
        1. Lambda 콘솔에서 함수 페이지를 연다
        2. 함수를 선택
        3. 코드 소스 창에서 업로드 원본을 선택한 다음 .zip 파일을 선택
        4. [업로드]를 선택하여 로컬 .zip 파일을 선택
        5. 저장을 선택
      - AWS CLI 사용
      - Amazon S3 사용
- 함수 배포
  - zip 파일 아카이브
    - Lambda 콘솔이나 도구 키트를 사용하여 함수를 작성하면 Lambda가 코드의.zip 파일 아카이브를 자동으로 생성
    - Lambda API, 명령줄 도구 또는 AWS SDK를 사용하여 함수를 생성하는 경우 배포 패키지를 생성해야 함.
    - 함수가 컴파일된 언어를 사용하거나 함수에 종속 항목을 추가하는 경우에도 배포 패키지를 생성해야 함.
  - 컨테이너 이미지
    - Docker 명령줄 인터페이스(CLI)와 같은 도구를 사용하여 코드 및 종속 항목을 컨테이너 이미지로 패키지화할 
      수 있다. 그런 다음 Amazon Elastic Container Registry(Amazon ECR)에서 호스팅되는 컨테이너 
      레지스트리에 이미지를 업로드할 수 있다.
- 함수 호출
  - 함수 URL 생성 및 관리
    - 함수 URL은 Lambda 함수를 위한 전용 HTTP(S) 엔드포인트이다.
    - 함수 URL 엔드포인트는 다음 형식을 취한다.
      - ```https://<url-id>.lambda-url.<region>.on.aws```
    - 함수 URL 생성(콘솔)
      - 함수 URL을 사용하여 새 함수를 생성하려면(콘솔)
        1. Lambda 콘솔의 함수 페이지를 연다.
        2. 함수 생성(Create function)을 선택
        3. 기본 정보에서 다음과 같이 한다.
           1) 함수 이름(Function name)에 my-function과 같은 함수 이름을 입력
           2) 런타임(Runtime)에서 원하는 언어 런타임을 선택합니다(예: Node.js 18.x).
           3) 아키텍처(Architecture)에서 x86_64 또는 arm64를 선택
           4) 권한(Permissions)을 확장한 다음, 새 실행 역할을 생성할지 아니면 기존 역할을 사용할지 여부를 선택
        4. 고급 설정(Advanced settings)을 확장한 다음 함수 URL(Function URL)을 선택
        5. 인증 유형(Auth type)에서 AWS_IAM 또는 NONE을 선택
        6. 함수 생성(Create function)을 선택
    - 함수 URL 생성(AWS CLI)
      - AWS Command Line Interface(AWS CLI)를 사용하여 기존 Lambda 함수에 대한 함수 URL을 생성하려면 
        다음 명령을 실행
        ``` 
           aws lambda create-function-url-config \
             --function-name my-function \
             --qualifier prod \ // optional
             --auth-type AWS_IAM
             --cors-config {AllowOrigins="https://example.com"} // optional
        ```
        이렇게 하면 함수 my-function에 대한 prod 한정자에 함수 URL이 추가됨

test 1