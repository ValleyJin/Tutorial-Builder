# Chapter 3: 타이니월드 (TinyWorld)


이전 [제2장: 타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md)에서는 시뮬레이션의 개별 배우인 '타이니퍼슨'을 만들고 각자의 개성을 부여하는 방법을 배웠습니다. 하지만 배우들만 있어서는 이야기가 완성되지 않겠죠? 그들이 함께 호흡하고, 서로 영향을 주고받으며 이야기를 펼쳐나갈 '무대'가 필요합니다. 이번 장에서는 바로 그 무대, '타이니월드(TinyWorld)'에 대해 알아보겠습니다.

## 타이니월드는 무엇일까요? 왜 필요할까요?

타이니월드는 타이니퍼슨들이 살아가는 무대 또는 환경입니다. 마치 연극의 배경처럼, 이곳에서 에이전트(타이니퍼슨)들은 서로 대화하고, 정보를 교환하며, 공동의 목표를 향해 나아가거나 갈등을 겪기도 합니다. 타이니월드는 에이전트들의 상호작용 방식과 규칙을 정의하며, 시뮬레이션의 시간 흐름도 관리합니다.

**핵심 사용 사례:** 여러분이 작은 스타트업의 팀장이라고 상상해 보세요. 다음 분기 제품 개발 방향에 대해 팀원들과 브레인스토밍을 하고 싶습니다. 팀원 A는 매우 창의적이지만 현실 감각이 부족하고, 팀원 B는 신중하지만 새로운 아이디어에 소극적입니다. 이 두 팀원이 가상의 회의실에서 아이디어를 주고받는 모습을 시뮬레이션해 보면 어떨까요? 타이니월드는 바로 이 "가상의 회의실"과 같은 역할을 합니다. 각기 다른 성격의 타이니퍼슨들이 이 월드 안에서 서로 대화하고 반응하며, 우리는 그 과정을 통해 실제 팀 논의에서 어떤 결과가 나올지 미리 가늠해 볼 수 있습니다.

타이니월드가 없다면, 타이니퍼슨들은 각자 고립되어 아무런 상호작용도 할 수 없을 것입니다. 타이니월드는 다음과 같은 중요한 역할을 합니다:

*   **타이니퍼슨들의 활동 공간:** 타이니퍼슨들이 존재하고 움직일 수 있는 공간을 제공합니다.
*   **상호작용의 매개체:** 타이니퍼슨들 간의 대화나 행동이 서로에게 전달될 수 있도록 합니다.
*   **시간 관리자:** 시뮬레이션 내의 시간이 어떻게 흘러가는지를 관리합니다.
*   **환경 규칙 정의:** 특정 환경(예: 소셜 네트워크, 사무실)에 맞는 상호작용 규칙을 설정할 수 있습니다.

이 장을 통해 여러분은 타이니월드를 만들고, 타이니퍼슨들을 그 안에 배치하며, 그들이 서로 상호작용하는 기본적인 시뮬레이션을 실행하는 방법을 배우게 될 것입니다.

## 타이니월드 만들기: 첫걸음

가장 먼저, 타이니퍼슨들이 살아갈 세상을 만들어야 합니다. `TinyWorld` 클래스를 사용하여 간단한 월드를 생성할 수 있습니다. 월드에는 이름을 붙여줄 수 있습니다.

```python
from tinytroupe.environment import TinyWorld

# "우리 동네"라는 이름의 타이니월드 생성
my_town = TinyWorld(name="우리 동네")

print(f"새로운 월드가 생성되었습니다: {my_town.name}")
```

위 코드를 실행하면 `"새로운 월드가 생성되었습니다: 우리 동네"`와 같이 출력됩니다. 이제 '우리 동네'라는 이름의 빈 무대가 준비되었습니다. 아직은 텅 비어 있지만, 곧 타이니퍼슨들로 채워질 것입니다.

## 타이니월드에 배우들 초대하기: 타이니퍼슨 추가

만들어진 타이니월드에 우리가 [제2장: 타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md)에서 만들었던 타이니퍼슨들을 초대해 봅시다. 타이니월드를 생성할 때 `agents` 파라미터에 타이니퍼슨 객체들의 리스트를 전달하거나, 생성 후에 `add_agent()` 메서드를 사용하여 한 명씩 추가할 수 있습니다.

예를 들어, '김철수'와 '이영희'라는 두 타이니퍼슨이 있다고 가정하고, 이들을 '우리 동네' 월드에 추가해 보겠습니다.

```python
from tinytroupe.agent import TinyPerson # 타이니퍼슨을 만들기 위해 import
from tinytroupe.environment import TinyWorld

# 타이니퍼슨 생성 (이전 장에서 배운 내용)
cheolsu = TinyPerson(name="김철수")
cheolsu.define("age", 30)
cheolsu.define("occupation", {"title": "회사원"})

younghee = TinyPerson(name="이영희")
younghee.define("age", 28)
younghee.define("occupation", {"title": "프리랜서 디자이너"})

# 타이니퍼슨들을 포함하여 "우리 동네" 월드 생성
my_town = TinyWorld(name="우리 동네", agents=[cheolsu, younghee])

print(f"{my_town.name}에는 현재 {len(my_town.agents)}명의 주민이 있습니다.")
for agent in my_town.agents:
    print(f"- {agent.name} ({agent.get('occupation')['title']})")
```

이 코드를 실행하면 다음과 유사한 결과가 출력될 것입니다:

```
우리 동네에는 현재 2명의 주민이 있습니다.
- 김철수 (회사원)
- 이영희 (프리랜서 디자이너)
```

이제 '우리 동네'에는 김철수 씨와 이영희 씨가 살게 되었습니다! 그들은 이제 같은 공간에 존재하며 서로 상호작용할 준비가 되었습니다.

## 타이니월드에서 상호작용 시작하기

타이니퍼슨들이 월드에 모였으니, 이제 그들이 서로 소통하고 행동하는 모습을 지켜볼 차례입니다. 타이니월드는 이러한 상호작용을 중재하고 시뮬레이션의 흐름을 관리합니다.

### 1. 월드를 통해 메시지 전달하기: `broadcast()`

월드는 모든 에이전트에게 한 번에 메시지를 전달하는 `broadcast()` 기능을 제공합니다. 예를 들어, 동네에 새로운 공지가 생겼다고 가정해 봅시다.

```python
# (이전 코드에 이어서)
announcement = "오늘 저녁 7시에 동네 공원에서 작은 음악회가 열립니다!"
print(f"\n[안내방송] {announcement}")
my_town.broadcast(announcement) # "우리 동네"의 모든 주민에게 안내방송 전달
```

`my_town.broadcast(announcement)`가 실행되면, '김철수'와 '이영희'는 모두 "오늘 저녁 7시에 동네 공원에서 작은 음악회가 열립니다!"라는 메시지를 듣게 됩니다. (정확히는 그들의 `listen` 메서드가 내부적으로 호출됩니다.)

### 2. 시뮬레이션 실행하기: `run()`

타이니퍼슨들이 스스로 생각하고 행동하게 하려면 시뮬레이션을 실행해야 합니다. `world.run()` 메서드는 시뮬레이션을 특정 '스텝(step)'만큼 진행시킵니다. 한 스텝 동안 월드 안의 각 에이전트는 한 번씩 행동할 기회를 얻습니다.

예를 들어, 김철수 씨가 이영희 씨에게 말을 거는 상황을 시뮬레이션해 봅시다.

```python
# 시뮬레이션 제어를 위해 import (제1장에서 배운 내용)
import tinytroupe.control as control

# 시뮬레이션 시작 (LLM 호출 결과 등을 캐싱)
control.begin()

# 김철수가 이영희에게 말을 걸도록 외부 자극을 줌
print(f"\n{cheolsu.name}: 이영희 씨, 안녕하세요! 혹시 오늘 저녁 음악회 가시나요?")
cheolsu.listen(f"이영희 씨에게 '안녕하세요! 혹시 오늘 저녁 음악회 가시나요?' 라고 물어보세요.")

# "우리 동네" 시뮬레이션을 1 스텝 실행
# 이 스텝에서 김철수는 위에서 들은 내용을 바탕으로 행동(말하기)할 것입니다.
print("\n--- 우리 동네 시뮬레이션 1 스텝 시작 ---")
my_town.run(steps=1)
print("--- 우리 동네 시뮬레이션 1 스텝 종료 ---\n")

# 이제 이영희가 김철수의 말을 들었으므로, 다음 스텝에서 반응할 수 있습니다.
# 이영희가 반응하도록 시뮬레이션을 1 스텝 더 실행
print("--- 우리 동네 시뮬레이션 2 스텝 시작 ---")
my_town.run(steps=1)
print("--- 우리 동네 시뮬레이션 2 스텝 종료 ---\n")


# 시뮬레이션 종료
control.end()
```

위 코드에서 `my_town.run(steps=1)`이 처음 호출되면, '김철수'는 "이영희 씨에게 '안녕하세요! 혹시 오늘 저녁 음악회 가시나요?' 라고 물어보세요."라는 최근 기억을 바탕으로 이영희에게 말을 거는 행동을 할 것입니다. (실제 대화 내용은 LLM을 통해 생성됩니다.)

그러면 이영희는 김철수의 말을 듣게 됩니다.
그 후 `my_town.run(steps=1)`이 다시 호출되면, 이번에는 이영희가 김철수의 말에 대한 반응을 행동으로 옮길 것입니다.

콘솔에는 각 에이전트의 생각과 행동이 출력되어 시뮬레이션 과정을 관찰할 수 있습니다. 예를 들면 다음과 같은 내용이 나올 수 있습니다 (실제 LLM 응답은 달라질 수 있습니다):

```
김철수: 이영희 씨, 안녕하세요! 혹시 오늘 저녁 음악회 가시나요?

--- 우리 동네 시뮬레이션 1 스텝 시작 ---
USER --> 김철수: [CONVERSATION]
          > 이영희 씨에게 '안녕하세요! 혹시 오늘 저녁 음악회 가시나요?' 라고 물어보세요.
───────────────────────────────────────── 우리 동네 step 1 of 1 (2023-10-27 10:00:00) ──────────────────────────────────────────
김철수 --> 김철수: [THOUGHT]
          > 이영희에게 인사를 하고 음악회에 가는지 물어봐야겠다.
김철수 acts: [TALK]
          > 안녕하세요, 이영희 씨! 오늘 저녁에 동네 공원에서 음악회가 열린다고 하던데, 혹시 가실 생각이세요?
김철수 --> 김철수: [THOUGHT]
          > 이제 내 할 말은 다 했으니, 이영희 씨의 대답을 기다려야겠다.
김철수 acts: [DONE]

김철수 --> 이영희: [CONVERSATION]
          > 안녕하세요, 이영희 씨! 오늘 저녁에 동네 공원에서 음악회가 열린다고 하던데, 혹시 가실 생각이세요?
--- 우리 동네 시뮬레이션 1 스텝 종료 ---

--- 우리 동네 시뮬레이션 2 스텝 시작 ---
───────────────────────────────────────── 우리 동네 step 1 of 1 (2023-10-27 10:00:01) ──────────────────────────────────────────
이영희 --> 이영희: [THOUGHT]
          > 김철수 씨가 음악회에 대해 물어봤네. 좋은 정보 고마워요. 같이 가면 좋을 것 같다.
이영희 acts: [TALK]
          > 어머, 철수 씨 안녕하세요! 네, 저도 그 소식 들었어요. 같이 가실래요?
이영희 --> 이영희: [THOUGHT]
          > 대답도 했고, 같이 가자고 제안도 했으니 이제 철수 씨 반응을 봐야지.
이영희 acts: [DONE]

이영희 --> 김철수: [CONVERSATION]
          > 어머, 철수 씨 안녕하세요! 네, 저도 그 소식 들었어요. 같이 가실래요?
--- 우리 동네 시뮬레이션 2 스텝 종료 ---
```
여기서 `control.begin()`과 `control.end()`는 [제1장: 시뮬레이션 제어 (Simulation Control)](01_시뮬레이션_제어__simulation_control__.md)에서 배운 내용으로, LLM 호출 결과를 캐싱하여 반복 실행 시 시간과 비용을 절약해줍니다. `@transactional` 데코레이터가 붙은 `world.run()`과 같은 함수들은 이러한 제어의 영향을 받습니다.

## 타이니월드 살펴보기: 시간의 흐름과 환경 규칙

타이니월드는 단순히 타이니퍼슨들을 담는 그릇 이상의 역할을 합니다.

*   **시간 관리:** `world.run(steps, timedelta_per_step)` 메서드를 통해 시뮬레이션 내의 시간이 얼마나 흘러갈지 지정할 수 있습니다. 예를 들어, `timedelta_per_step=timedelta(minutes=10)`으로 설정하면, `run(steps=6)`은 총 1시간(10분 * 6 스텝) 동안의 시뮬레이션을 진행합니다. 기본 `TinyWorld`는 스텝마다 시간을 자동으로 약간씩 증가시킵니다. (위 예시 출력에서 시간이 조금씩 바뀌는 것을 볼 수 있습니다.)
*   **환경 규칙:** `TinyWorld`를 상속받아 특별한 규칙을 가진 월드를 만들 수도 있습니다. 예를 들어, `TinySocialNetwork` 클래스는 에이전트 간의 '관계'를 설정하고, 이 관계에 따라서만 소통이 가능하도록 제한하는 소셜 네트워크 환경을 시뮬레이션합니다. (이 클래스는 `tinytroupe.environment` 모듈에서 찾을 수 있습니다.)

```python
from datetime import timedelta

# 10분 간격으로 3 스텝 (총 30분) 시뮬레이션 실행
# my_town.run(steps=3, timedelta_per_step=timedelta(minutes=10))
```

## 타이니월드는 어떻게 작동할까요? 내부 동작 살짝 엿보기

타이니월드가 여러 타이니퍼슨들의 상호작용을 어떻게 조율하는지 궁금하실 겁니다. 그 내부 과정을 간단히 살펴보겠습니다.

### 개념적 흐름

사용자가 `world.run()`을 호출하면, 타이니월드 내부에서는 대략 다음과 같은 일들이 순차적으로 일어납니다:

1.  **시작 신호:** 사용자가 `world.run(steps=N)`을 호출하여 시뮬레이션을 N 스텝만큼 진행하라고 명령합니다.
2.  **스텝 반복:** 월드는 N번의 스텝을 하나씩 처리합니다. 각 스텝마다 다음 과정이 반복됩니다.
    *   **(선택 사항) 시간 업데이트:** `timedelta_per_step`이 주어졌다면, 월드의 현재 시간을 그만큼 증가시킵니다.
    *   **(선택 사항) 환경 이벤트 처리:** 월드 자체에 설정된 특별한 이벤트(예: '매 시간 정각에 종이 울린다')가 있다면 처리합니다. (이는 `Intervention`이라는 고급 기능을 통해 구현됩니다.)
    *   **에이전트 행동 유도:** 월드는 자신이 품고 있는 모든 에이전트(타이니퍼슨)들에게 차례대로 행동할 기회를 줍니다.
        *   각 에이전트는 `agent.act()` 메서드를 호출하여 현재 상황과 자신의 생각에 따라 어떤 행동을 할지 결정합니다. (예: "이영희에게 '음악회 같이 갈까요?'라고 말하기")
    *   **행동 처리:** 에이전트가 행동을 결정하면, 월드는 그 행동을 실제로 실행합니다.
        *   만약 행동이 "말하기(`TALK`)"라면, 월드는 `_handle_talk()`와 같은 내부 함수를 통해 해당 메시지를 지정된 수신자 에이전트에게 전달합니다. 이 메시지를 받은 에이전트는 `listen()` 메서드를 통해 그 내용을 듣게 됩니다.
        *   다른 종류의 행동(예: "이동하기", "물건 사용하기" 등 - 아직 자세히 다루지 않음)도 각자의 방식대로 월드에 의해 처리됩니다.
3.  **종료:** N번의 스텝이 모두 완료되면 `run()` 메서드가 종료됩니다.

이 과정을 간단한 그림으로 표현하면 다음과 같습니다:

```mermaid
sequenceDiagram
    participant UserCode as 사용자 코드
    participant MyTown as 우리 동네 (타이니월드)
    participant Cheolsu as 김철수 (에이전트 A)
    participant Younghee as 이영희 (에이전트 B)

    UserCode->>MyTown: my_town.run(1) 호출
    MyTown->>Cheolsu: Cheolsu.act() 호출 (행동 결정)
    Cheolsu-->>MyTown: "이영희에게 '음악회 같이 갈래요?' 라고 말하기" 행동 반환
    MyTown->>MyTown: 김철수의 행동 처리 (예: _handle_talk)
    MyTown->>Younghee: Younghee.listen("음악회 같이 갈래요?", source=Cheolsu) 호출
    Younghee->>Younghee: 메시지 듣고 기억하기
    Note over MyTown: (다음 에이전트가 있다면 반복)
    MyTown-->>UserCode: run(1) 완료
end
```

### 코드 내부 살펴보기 (`tinytroupe/environment/tiny_world.py`)

실제 코드는 좀 더 복잡하지만, 핵심적인 부분들을 통해 어떻게 타이니월드가 작동하는지 감을 잡아봅시다.

*   **월드 생성 (`__init__`)**:
    타이니월드가 처음 만들어질 때, 월드의 이름이나 초기 에이전트 같은 정보들이 설정됩니다.

    ```python
    # tinytroupe/environment/tiny_world.py 일부
    class TinyWorld:
        def __init__(self, name: str="A TinyWorld", agents=[], 
                     initial_datetime=datetime.now(), # 월드의 시작 시간
                     # ... 기타 파라미터들 ...
                     ):
            self.name = name
            self.current_datetime = initial_datetime # 현재 월드 시간
            
            self.agents = [] # 이 월드에 속한 에이전트들을 담을 리스트
            self.name_to_agent = {} # 이름으로 에이전트를 빠르게 찾기 위한 딕셔너리

            # ... 기타 여러 내부 변수 초기화 ...

            self.add_agents(agents) # 생성 시 전달된 에이전트들을 월드에 추가
    ```
    `__init__` 메서드는 월드의 기본 상태를 설정합니다. 특히 `self.agents` 리스트가 이 월드에 참여하는 모든 타이니퍼슨들을 관리하게 됩니다.

*   **에이전트 추가 (`add_agent`)**:
    타이니퍼슨을 월드에 추가하는 메서드입니다.

    ```python
    # tinytroupe/environment/tiny_world.py 일부
    def add_agent(self, agent: TinyPerson):
        # 이미 월드에 있는 에이전트인지 확인
        if agent not in self.agents:
            # 에이전트에게 자신이 어떤 월드에 속해있는지 알려줌
            agent.environment = self 
            self.agents.append(agent)
            self.name_to_agent[agent.name] = agent
        else:
            # 이미 있다면 경고 메시지 (혹은 에러 처리)
            logger.warn(f"에이전트 {agent.name}은(는) 이미 이 월드에 있습니다.")
        return self # 다른 메서드를 연이어 호출할 수 있도록 self 반환
    ```
    중요한 점은 에이전트를 월드에 추가할 때, 에이전트 객체(`agent`)의 `environment` 속성에 현재 월드 객체(`self`)를 할당한다는 것입니다. 이를 통해 에이전트도 자신이 어떤 환경에 속해 있는지 알 수 있게 됩니다.

*   **시뮬레이션 실행 (`run` 및 `_step`)**:
    `run` 메서드는 시뮬레이션의 전체 루프를 담당하고, 내부적으로 `_step` 메서드를 반복 호출합니다. `_step` 메서드가 한 번의 시간 단위를 처리합니다.

    ```python
    # tinytroupe/environment/tiny_world.py 일부
    @transactional # 이 표시는 시뮬레이션 제어와 관련됨 (캐싱 등)
    def run(self, steps: int, timedelta_per_step=None, return_actions=False):
        # ...
        for i in range(steps): # 지정된 스텝 수만큼 반복
            # ... 현재 스텝 정보 등을 화면에 표시하는 로직 ...
            
            # 실제 한 스텝의 로직은 _step 메서드에 위임
            agents_actions = self._step(timedelta_per_step=timedelta_per_step)
            # ... (선택 사항) 에이전트 행동 결과 수집 ...
        # ...
        if return_actions:
            return agents_actions_over_time # 모든 스텝의 행동 결과 반환
    
    @transactional
    def _step(self, timedelta_per_step=None):
        # 월드의 현재 시간 진행
        self._advance_datetime(timedelta_per_step)

        # (만약 있다면) 이 스텝에서 적용될 환경적인 변화/개입(Intervention) 처리
        for intervention in self._interventions:
            if intervention.check_precondition(): # 개입 조건 확인
                # ... 개입 적용 및 로그 기록 ...
                intervention.apply_effect() # 실제 효과 적용

        # 월드 내 모든 에이전트들이 행동할 차례
        agents_actions_this_step = {}
        for agent in self.agents:
            # 에이전트에게 행동을 요청하고, 그 결과를 받음
            actions = agent.act(return_actions=True) 
            agents_actions_this_step[agent.name] = actions

            # 에이전트가 방금 한 행동들을 월드가 처리 (예: 메시지 전달)
            self._handle_actions(agent, agent.pop_latest_actions())
        
        return agents_actions_this_step
    ```
    `run` 메서드와 `_step` 메서드 모두 `@transactional`로 표시되어 있습니다. 이는 [제1장: 시뮬레이션 제어 (Simulation Control)](01_시뮬레이션_제어__simulation_control__.md)에서 설명한 것처럼, 이들의 실행 과정과 결과가 캐시될 수 있음을 의미합니다. `_step` 내부에서는 각 에이전트의 `act()`를 호출하여 행동을 얻어내고, `_handle_actions()`를 통해 그 행동을 처리합니다.

*   **말하기 행동 처리 (`_handle_actions` 및 `_handle_talk`)**:
    에이전트가 "말하기(`TALK`)" 행동을 결정했을 때, 월드가 이를 어떻게 처리하는지 보여주는 부분입니다.

    ```python
    # tinytroupe/environment/tiny_world.py 일부
    @transactional
    def _handle_actions(self, source: TinyPerson, actions: list):
        for action in actions: # 에이전트가 한 번에 여러 행동을 할 수도 있음
            action_type = action["type"] # 행동의 종류 (예: "TALK", "MOVE")
            content = action.get("content") # 행동의 내용 (예: 메시지)
            target = action.get("target") # 행동의 대상 (예: 메시지 수신자)

            # ... 행동 종류에 따라 다른 처리 로직 ...
            if action_type == "TALK":
                self._handle_talk(source, content, target)
            # elif action_type == "REACH_OUT": # 다른 에이전트에게 처음 말 걸기 시도
            #     self._handle_reach_out(source, content, target)
            # ... 기타 다른 행동들 처리 ...

    @transactional
    def _handle_talk(self, source_agent: TinyPerson, content: str, target: str):
        # 이름으로 대상 에이전트를 월드에서 찾음
        target_agent = self.get_agent_by_name(target)

        if target_agent is not None:
            # 대상 에이전트가 존재하면, 그 에이전트에게 메시지를 '듣게' 함
            target_agent.listen(content, source=source_agent)
        elif self.broadcast_if_no_target: 
            # 대상이 지정되지 않았거나 찾을 수 없고, 모두에게 방송 옵션이 켜져 있다면
            self.broadcast(content, source=source_agent) # 월드 전체에 방송
    ```
    `_handle_actions`는 에이전트가 반환한 행동 목록을 살펴보고, 각 행동의 `type`에 따라 적절한 `_handle_...` 함수를 호출합니다. `_handle_talk`의 경우, `target`으로 지정된 에이전트를 찾아 `listen()` 메서드를 호출하여 메시지를 전달합니다. 만약 `target`이 없거나 `broadcast_if_no_target` 옵션이 켜져 있다면, 월드 내 모든 에이전트에게 메시지를 `broadcast` 합니다.

이처럼 타이니월드는 내부적으로 에이전트들의 목록을 관리하고, 시간의 흐름에 따라 각 에이전트에게 행동 기회를 부여하며, 그 행동들이 다른 에이전트나 환경에 영향을 미치도록 중재하는 복잡한 오케스트라 지휘자와 같은 역할을 수행합니다.

## 정리 및 다음 단계

이번 장에서는 타이니퍼슨들이 살아가는 무대인 `타이니월드 (TinyWorld)`에 대해 배웠습니다. 타이니월드를 만들고, 그 안에 타이니퍼슨들을 추가하며, `run()` 메서드를 통해 시뮬레이션을 진행시키는 기본적인 방법을 익혔습니다. 또한, 타이니월드가 내부적으로 어떻게 에이전트들의 상호작용을 관리하고 시간의 흐름을 제어하는지에 대해서도 간략하게 살펴보았습니다.

**핵심 요약:**

*   `TinyWorld`는 타이니퍼슨들이 상호작용하는 환경 또는 무대입니다.
*   `TinyWorld(name="월드이름", agents=[퍼슨1, 퍼슨2])`와 같이 생성하고 타이니퍼슨을 배치할 수 있습니다.
*   `world.run(steps=N)`을 호출하여 N 스텝만큼 시뮬레이션을 진행시킬 수 있으며, 각 스텝마다 에이전트들은 행동할 기회를 얻습니다.
*   월드는 에이전트 간의 메시지 전달(`TALK` 행동 처리)과 같은 상호작용을 중재합니다.
*   월드는 시뮬레이션의 시간 흐름(`current_datetime`)을 관리합니다.

이제 우리는 개성 있는 배우들([타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md))과 그들이 뛰어놀 수 있는 무대(`타이니월드`)를 모두 갖추었습니다. 그런데 이 똑똑한 배우들은 과연 어떻게 그렇게 상황에 맞는 대사를 생각해내고 행동을 결정하는 걸까요? 그 비밀은 바로 대규모 언어 모델(LLM)에 있습니다.

다음 [제4장: OpenAI 유틸리티 (OpenAI Utilities)](04_openai_유틸리티__openai_utilities__.md)에서는 타이니퍼슨들이 이렇게 지능적인 판단을 내리는 데 필요한 핵심 도구, 즉 OpenAI의 언어 모델과 소통하는 방법에 대해 자세히 알아보겠습니다. 기대해 주세요!

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)