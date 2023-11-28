# TECH INFO

## 목차
1. [Mobile Applications](#Mobile-Applications)
2. [Cloud Providers](#Cloud-Providers)
3. [SERVERLESS](#SERVERLESS)

## Mobile Applications
### React Native
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

## Cloud Providers
### AWS

## SERVERLESS
### AWS LAMBDA
- Lambda는 빠르게 스케일 업해야 하고 수요가 없을 때는 0으로 스케일 다운해야 하는 애플리케이션 시나리오에 이상적인 컴퓨팅 서비스이다.
- 함수
  - 함수는 Lambda에서 코드를 실행하기 위해 호출할 수 있는 리소스이다.
- 트리거
  - 트리거는 Lambda에서 함수를 호출하는 리소스 또는 구성이다.
- 이벤트
  - 이벤트는 처리할 Lambda 함수에 대한 데이터가 포함된 JSON 형식 문서이다.
- 실행환경
  - <img alt="Execution_environment" src="img/serverless/Execution_environment.png">
  - 함수의 런타임은 런타임 API를 사용하여 Lambda와 통신한다. 익스텐션은 익스텐션 API를 사용하여
    Lambda와 통신한다. 또한 확장은 텔레메트리 API를 사용하여 함수의 로그 메시지와 기타 텔레메트리
    데이터를 수신할 수 있다.


test2