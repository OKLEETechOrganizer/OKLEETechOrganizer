# TECH INFO

## 목차
1. [Mobile Applications](#Mobile-Applications)
2. [Cloud Providers](#Cloud-Providers)

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
#### SERVERLESS
##### LAMBDA
