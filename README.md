# GTRPGM Project

> Graph-based Tabletop Role-Playing Game Master

## 프로젝트 소개

**GTRPGM**은 고정된 세계관과 룰 안에서
시나리오를 그래프로 관리하며,
자연어 상호작용으로 몰입감 있는 TRPG 플레이를 가능하게 하는
AI 게임 마스터 시스템 입니다.

### 주요 기능

- **Rule Engine (RUE)**: 자연어 입력을 룰북의 요소로 변환하고, 이를 기반으로 상태 업데이트를 계산
- **Scenario Writer (SWR)**: 세계관을 기반으로 일관적인 세계관을 작성하고 시나리오 그래프(SG)로 변환
- **Graph-based Game Master (GGM)**: RUE와 SG를 기반으로 TRPG 세션을 진행

## 프로젝트 레포지토리 설명

- [**main**](./): 프로젝트 소개와 팀 협업·의사결정 과정을 함께 기록한 메인 레포지토리
- [**rule-engine**](https://github.com/GTRPGM/rule-engine): 룰 엔진 서비스
- [**scenario-writer**](./): 시나리오 라이터 서비스
- [**GM**](./): 게임 마스터 서비스
- [**FE**](./): 프론트엔드 애플리케이션
- [**BE**](./): 백엔드 API 및 세션 처리 로직 및 LLM 게이트웨이
- [**Ops**](./): 통합 테스트, 배포 설정, CI/CD 파이프라인

## 라이선스

- 미정
