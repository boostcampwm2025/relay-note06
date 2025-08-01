## ✅ 퀴즈 1. (OX 퀴즈)

**Q. 스레드 풀은 작업마다 새로운 스레드를 생성하여 병렬 처리를 가능하게 해주는 시스템이다.**

<details>
<summary>정답과 해설 보기</summary>

**정답:** ❌  
**해설:**  
스레드 풀은 미리 생성된 스레드들을 재사용하여 작업을 처리한다.  
매 작업마다 새로운 스레드를 생성하면 오히려 오버헤드가 크기 때문에, 이를 줄이기 위해 스레드 풀이 사용된다.

</details>

---

## ✅ 퀴즈 2. (객관식)

**Q. 다음 중 객체 지향 프로그래밍의 네 가지 주요 원칙에 해당하지 않는 것은?**

A. 추상화 (Abstraction)  
B. 캡슐화 (Encapsulation)  
C. 반복 (Iteration)  
D. 다형성 (Polymorphism)

<details>
<summary>정답과 해설 보기</summary>

**정답:** C. 반복 (Iteration)  
**해설:**  
반복은 객체 지향의 핵심 원칙이 아니라 절차적 프로그래밍이나 일반적인 제어 흐름에서 사용되는 개념이다.

</details>

---

## ✅ 퀴즈 3. (단답형)

**Q. Git에서 특정 디렉토리의 파일 목록과 구조를 저장하는 객체는 무엇인가요?**

<details>
<summary>정답과 해설 보기</summary>

**정답:** tree  
**해설:**  
`tree` 객체는 Git에서 디렉토리 구조를 저장하며, 각 파일 및 서브 디렉토리의 이름, 모드, 해시 정보를 포함하고 있다.

</details>

---

## ✅ 퀴즈 4. (주관식)

**Q. 스레드 풀의 주요 구성 요소 중, 작업을 대기시키는 자료구조로 Producer-Consumer 패턴을 따르며, 스레드가 작업을 꺼내가는 곳은 무엇인가요?**

<details>
<summary>정답과 해설 보기</summary>

**정답 예시:**  
작업 큐, Task Queue, 또는 Work Queue

**해설:**  
작업 큐는 스레드 풀이 처리할 작업을 저장해두는 대기열이다.  
생산자(Producer)가 큐에 작업을 넣고, 소비자(Consumer)인 스레드들이 큐에서 작업을 가져가 처리한다.  
이 구조는 Producer-Consumer 패턴을 따른다.

</details>

---

## week2 - J240 퀘스트 추가

### Day 11-12 Quiz

## 퀴즈 1: 이벤트 루프 실행 순서 예측하기

### 문제

다음 JavaScript 코드의 출력 순서를 예측하고, 각각이 어떤 큐에서 처리되는지 설명하세요.

```javascript
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => {
  console.log("C");
  setTimeout(() => console.log("D"), 0);
});

Promise.resolve().then(() => console.log("E"));

console.log("F");
```

### 정답

출력 순서: A → F → C → E → B → D

### 처리 과정

1. `A`, `F` - 동기 코드 (Call Stack)
2. `C`, `E` - Job Queue (Microtask) 처리
3. `B`, `D` - Task Queue (Macrotask) 처리

### 핵심

Job Queue는 Task Queue보다 우선순위가 높음

---

## 퀴즈 2: Promise vs EventEmitter 차이점 이해하기

### 문제

다음 두 코드의 차이점을 설명하고, 각각 언제 사용하는 것이 적합한지 판단하세요.

### 코드 A

```javascript
const promise = new Promise((resolve) => {
  resolve("데이터 전송 완료");
  resolve("추가 데이터"); // 이 부분은?
});
```

### 코드 B

```javascript
const EventEmitter = require("events");
const emitter = new EventEmitter();
emitter.emit("data", "첫 번째 데이터");
emitter.emit("data", "두 번째 데이터");
```

### 정답

#### Promise (코드 A)

- 일회성 비동기 작업, 한 번 resolve되면 고정
- '추가 데이터'는 무시됨
- **사용 시기:** API 호출, 파일 읽기 등 한 번의 결과가 필요한 작업

#### EventEmitter (코드 B)

- 지속적인 이벤트 스트림 처리
- 같은 이벤트를 여러 번 발생 가능
- **사용 시기:** 실시간 데이터 스트림, 사용자 인터랙션 등 반복적 이벤트

---

## 퀴즈 3: 멀티스레드 vs 이벤트 기반 비동기 구분하기

### 문제

다음 상황들을 멀티스레드 방식과 이벤트 기반 비동기 방식 중 어느 것이 더 적합한지 판단하고, 그 이유를 설명하세요.

- **상황 A:** 대용량 이미지 파일 100개를 동시에 리사이징 처리
- **상황 B:** 실시간 채팅 서버에서 1000명의 사용자 메시지 처리
- **상황 C:** 복잡한 수학 계산을 수행하는 과학 계산 프로그램

### 정답

- **상황 A: 멀티스레드** - CPU 집약적 작업이므로 진정한 병렬처리가 필요
- **상황 B: 이벤트 기반 비동기** - I/O 집약적이고 높은 동시성 처리가 필요
- **상황 C: 멀티스레드** - CPU 집약적 계산 작업으로 병렬처리 효과적

---

### Day 13-14 Quiz

## 퀴즈 1: Git 객체 구조와 관계 이해하기

### 문제

다음 상황에서 Git이 생성하는 객체들과 그 관계를 설명하세요.

```
프로젝트 구조:
my-project/
├── README.md (내용: "Hello World")
├── src/
│   └── main.js (내용: "console.log('start');")
└── package.json (내용: "{\"name\": \"test\"}")
```

위 파일들을 모두 add하고 commit했을 때:

1. 생성되는 객체의 종류와 개수는?
2. 각 객체들이 어떻게 연결되는지 설명하세요.
3. `git cat-file -p <commit_hash>` 명령어로 확인할 수 있는 정보는?

### 정답

#### 1. 생성되는 객체

- **Blob 객체 3개**: README.md, main.js, package.json 각각의 내용
- **Tree 객체 2개**: 루트 디렉토리용 1개, src/ 디렉토리용 1개
- **Commit 객체 1개**: 전체 스냅샷을 가리키는 커밋

#### 2. 객체 연결 구조

```
Commit → Root Tree → README.md (blob)
                  → package.json (blob)
                  → src/ (tree) → main.js (blob)
```

#### 3. commit 객체에서 확인 가능한 정보

- tree 해시 (루트 디렉토리 tree 객체)
- parent 해시 (이전 커밋, 첫 커밋이면 없음)
- author 정보 (이름, 이메일, 시간)
- committer 정보
- 커밋 메시지

---

## 퀴즈 2: Git 파일 상태 변화 시나리오

### 문제

다음 Git 명령어 시퀀스에서 `test.txt` 파일의 상태 변화를 추적하세요.

```bash
# 초기 상태: test.txt 파일이 존재하지 않음
echo "Hello" > test.txt     # 1단계
git add test.txt            # 2단계
echo "World" >> test.txt    # 3단계
git add test.txt            # 4단계
git commit -m "Add test"    # 5단계
echo "!" >> test.txt        # 6단계
```

각 단계에서 `test.txt` 파일의 상태는?

### 정답

1. **Untracked** - 새로 생성된 파일, Git이 추적하지 않음
2. **Staged** - Staging Area에 추가됨 (내용: "Hello")
3. **Modified + Staged** - Working Directory에서 수정됨, 하지만 Staging Area에는 이전 버전
4. **Staged** - 최신 내용이 Staging Area에 추가됨 (내용: "Hello\nWorld")
5. **Unmodified** - 커밋 완료, 깨끗한 상태
6. **Modified** - Working Directory에서 수정됨 (내용: "Hello\nWorld\n!")

### 핵심 포인트

- 3단계에서는 **같은 파일이 동시에 Staged + Modified 상태**가 될 수 있음
- Git은 파일의 여러 버전을 동시에 추적 가능

---

## 퀴즈 3: git fetch vs git pull 상황별 선택

### 문제

다음 상황에서 `git fetch`와 `git pull` 중 어느 것을 사용하는 것이 더 적절한지 판단하고 이유를 설명하세요.

**상황 A**: 팀 프로젝트에서 다른 팀원이 작업한 내용을 확인하고 싶지만, 현재 작업 중인 코드와 충돌할 가능성이 있어 신중하게 병합하고 싶은 경우

**상황 B**: 개인 프로젝트에서 다른 컴퓨터에서 작업한 내용을 현재 컴퓨터로 동기화하려는 경우 (충돌 가능성 거의 없음)

**상황 C**: 원격 저장소에 새로운 브랜치가 생성되었는지 확인하고 싶지만, 현재 브랜치는 그대로 유지하고 싶은 경우

### 정답

#### 상황 A: git fetch 추천

- **이유**: 원격 변경사항을 먼저 확인하고, 충돌 검토 후 수동으로 병합 결정 가능
- **과정**: `git fetch` → `git log origin/main` → `git merge origin/main` 또는 `git rebase`

#### 상황 B: git pull 사용 가능

- **이유**: 충돌 가능성이 낮고 빠른 동기화가 목적
- **주의**: 그래도 `git fetch` 후 확인하는 습관이 더 안전

#### 상황 C: git fetch 필수

- **이유**: 브랜치 정보만 업데이트하고 현재 작업 브랜치는 변경하지 않음
- **확인**: `git branch -r` 명령어로 원격 브랜치 목록 확인

### 핵심 원칙

- **안전성이 중요한 경우**: `git fetch` 사용
- **빠른 동기화가 필요한 경우**: `git pull` 사용
- **git pull = git fetch + git merge**

---
