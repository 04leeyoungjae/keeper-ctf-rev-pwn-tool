#  Git Workflow

##  목적

이 레포는 문제 풀이 기록이 아니라
**CTF 해결을 위한 템플릿(플레이북)과 자동화 구조를 개발하는 것을 목표로 한다.**

*  문제별 writeup 중심 repo 아님 X
*  재사용 가능한 exploit / 분석 템플릿 중심

---

##  Repository Structure

```text
repo/
 ├── templates/
 │    ├── pwn/
 │    │    ├── bof/
 │    │    ├── ret2libc/
 │    │    ├── format_string/
 │    │
 │    ├── reverse/
 │    │    ├── static_analysis/
 │    │    ├── dynamic_analysis/
 │    │
 │    ├── misc/
 │         ├── multi_input/
 │
 ├── core/
 │    ├── runner.py
 │    ├── utils.py
 │
 ├── experiments/
 │
 ├── docs/
 │
 └── README.md
```

---

##  Commit Convention

### 기본 규칙

* 1 Commit = 1 변경 (템플릿 / 구조 / 로직 단위)
* Commit은 “결과”가 아니라 **재사용 가능한 로직 변화**를 기록
* 문제 이름보다 **기법 중심으로 작성**

---

### Commit Type

| Tag      | Description                 |
| -------- | --------------------------- |
| Template | 새로운 템플릿 추가                  |
| Improve  | 기존 템플릿 개선                   |
| Refactor | 구조 개선 / 코드 정리               |
| AddCase  | 특정 문제 케이스 추가 (template 보강용) |
| Debug    | 템플릿 디버깅                     |
| Research | 새로운 기법 연구                   |
| Init     | 초기 구조 생성                    |
| Docs     | 템플릿 설명 문서                   |

---

###  Commit 예시

```bash
[Template] ret2libc 기본 템플릿 추가
[Template] multi-input orchestration 구조 추가
[Improve] BOF offset 자동 계산 로직 개선
[Refactor] exploit template 구조 분리
[AddCase] input2 케이스 추가 (multi-input template 보강)
[Debug] socket 연결 타이밍 문제 수정
[Research] heap exploitation 전략 정리
```

---

##  Branch Strategy

### 기본 구조

```text
main        → 안정화된 템플릿
dev         → 개발 중 통합 브랜치
template/*  → 템플릿 개발
experiment/* → 실험 / 테스트
research/*  → 새로운 기법 연구
```

---

### 브랜치 규칙

* 브랜치는 **기법/템플릿 단위로 생성**
* 하나의 브랜치 = 하나의 템플릿 또는 실험

---

###  Branch 예시

```bash
template/ret2libc
template/heap-uaf
template/multi-input
experiment/socket-orchestration
research/mcp-agent-detection
```

---

##  PR (Pull Request) 규칙

### 기본 원칙

* 1 PR = 1 템플릿 / 1 구조 개선
* PR은 “문제 풀이”가 아니라 **템플릿 단위**

---

### PR 예시

```text
PR1: ret2libc 템플릿 추가
PR2: multi-input orchestration 템플릿 추가
PR3: leak abstraction 추가
PR4: exploit runner 구조 개선
```

---

### PR 작성 규칙

* 어떤 템플릿인지 명확히 설명
* 어떤 문제 유형을 커버하는지
* 재사용 가능 포인트 설명
* 적용 가능한 예시 (선택)

---

##  Code Review 기준

* 템플릿이 일반화 가능한가
* 특정 문제에 과하게 종속되지 않았는가
* 재사용성 (reusability)이 높은가
* 확장 가능한 구조인가
* 불필요한 가정이 없는가

---

##  Workflow

```text
[1] research/*
 → 새로운 기법 탐색

[2] template/*
 → 템플릿 구현

[3] experiment/*
 → 실제 문제에 적용 및 검증

[4] dev
 → 통합 및 테스트

[5] main
 → 안정화된 템플릿 유지
```

---

## 핵심 철학

* exploit은 코드가 아니라 **패턴이다**
* 문제는 한 번 풀지만, 템플릿은 계속 재사용된다
* Commit은 결과가 아니라 **추상화 과정 기록이다**
* 브랜치는 기능이 아니라 **기법 단위**로 나눈다
