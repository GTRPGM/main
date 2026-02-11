# GTRPGM Project

> Graph-based Tabletop Role-Playing Game Master

## 프로젝트 소개

> [시연 링크](http://35.216.98.244:8080/login)

**GTRPGM**은 고정된 세계관과 룰 안에서
시나리오를 그래프로 관리하고 상태를 추적하며,
자연어 상호작용으로 일관성 있는 TRPG 플레이를 가능하게 하는
AI 게임 마스터 시스템 입니다.

### 주요 기능

- **Rule Engine**: 자연어 입력을 룰북의 요소로 변환하고, 이를 기반으로 상태 업데이트를 계산
- **Scenario Service**: 일관적인 세계관을 작성하고, 변화에 따른 시나리오 단계 변화 계산
- **State Manager**: 플레이 세션별로 세계관의 변화 추적
- **Game Master**: 위 서비스를 기반으로 일관성 있는 TRPG 세션을 진행

### 🧩 서비스 구성 (Microservices)

|       서비스명       | 역할 (Responsibility)                                              |
| :------------------: | :----------------------------------------------------------------- |
|    **GM Service**    | 게임의 메인 루프 실행, 턴 관리, 서사 생성, 에이전트 오케스트레이션 |
| **Scenario Service** | 사용자 컨셉 기반 시나리오(Act/Sequence) 자동 생성 및 검증          |
|   **Rule Engine**    | 게임 내 행동 판정(성공/실패), 주사위 굴림, 상태 변화 계산          |
|  **State Manager**   | 게임 월드 상태(State) 저장 및 관리, 스냅샷 제공                    |
|   **LLM Gateway**    | 모든 LLM 요청의 중앙 프록시, 모델 추상화 및 로깅                   |
|    **BE-Router**     | 클라이언트와 내부 서비스 간의 API 게이트웨이 및 라우팅             |
|       **Web**        | 사용자 인터페이스 (프론트엔드)                                     |

### Technical Stack

| 기술                 |          구분           | 사용 목적 및 상세                                                                  |
| :------------------- | :---------------------: | :--------------------------------------------------------------------------------- |
| **Python 3.11+**     |        Language         | 비동기 처리 및 풍부한 LLM 생태계(LangChain 등) 활용을 위한 주력 언어               |
| **FastAPI**          |        Framework        | 고성능 비동기 API 서버 구축. Pydantic을 통한 자동 데이터 검증 및 Swagger 문서 제공 |
| **Lang-chain**       |      LLM Framework      | llm 프롬프팅 및 에이전트 구성                                                      |
| **Langgraph**        | Orchestration Framework | 상태기반 에이전트 오케스트레이션                                                   |
| **Docker / Compose** |     Infrastructure      | 서비스 컨테이너화 및 로컬/운영 환경의 동일한 실행 환경(Environment) 보장           |
| **Github Action**    |     Infrastructure      | CI/CD 자동화 워크플로우                                                            |
| **PostgreSQL**       |        Database         | 관계형 데이터 저장. 서비스별 논리적 DB 분리를 통해 데이터 독립성 및 확장성 확보    |
| **Redis**            |      Cache/Broker       | 세션 관리, API 게이트웨이의 라우팅 정보 저장 및 빈번한 데이터의 캐싱               |

## 3. 설계 중점 사항 (Design Principles)

1. **Decoupling**: 서비스 간 통신은 표준화된 REST API를 사용하며, 각 서비스의 내부 구현은 외부에서 알 수 없도록 캡슐화.
2. **LLM Reliability**: LLM의 환각(Hallucination)이나 오류를 시스템적으로 보완하기 위해 검증용 에이전트(Reviewer)와 후처리 로직(Guardrails)을 기술적으로 배치.

## 프로젝트 레포지토리 설명

- [**main**](./): 프로젝트 소개와 팀 협업·의사결정 과정을 함께 기록한 메인 레포지토리
- [**rule-engine**](https://github.com/GTRPGM/rule-engine): 룰 엔진 서비스
- [**GM**](https://github.com/GTRPGM/gm): 게임 마스터 서비스
- [**state-manager**](https://github.com/GTRPGM/state-manager): 상태관리자 서비스
- [**scenario-service**](https://github.com/GTRPGM/scenario-service): 시나리오 서비스
- [**WEB**](https://github.com/GTRPGM/WEB): 프론트엔드 애플리케이션
- [**BE**](https://github.com/GTRPGM/BE-router): 백엔드 API 및 세션 처리 로직 및 LLM 게이트웨이
- [**infra**](https://github.com/GTRPGM/infra): 통합 테스트, DB 설정 및 배포
