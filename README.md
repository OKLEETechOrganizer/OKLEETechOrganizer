# TECH INFO

## 목차
0. [CS](#CS)
1. [FRONT](#FRONT)
2. [BACK](#BACK)
3. [DEVOPS](#DEVOPS)
4. [Architecture](#Architecture)
   1. [Multi Module](#Multi-Module)

## CS
- [CS](cs/README.md)<br>

## FRONT
- [FRONT](front/README.md)<br>

## BACK
- [BACK](back/README.md)<br>

## DEVOPS
- [DEVOPS](devops/README.md)<br>

## Architecture
### Multi Module
- 모듈이란 패키지의 한 단계 위의 집합체이며, 독립적으로 배포될 수 있는 코드의 단위
- 멀티 모듈이란 상호 연결된 여러개의 모듈로 구성된 프로젝트이다.
- 장점
  - 각 계층(Presentation layer, Busiss layer, Persistence layer 등)을 물리적으로 구분
  - 패키지가 담당하는 역할이 명확해짐
  - 패키지와 코드 구조 컨트롤
    - 패키지, 코드 간의 의존성을 얇게 
    - 의존성이 추가되지 않으면 import 불가능
  - 코드 중복을 최소화