# Chapter 8: 도구 (Tools)


이전 [제7장: 기억 (Memory)](07_기억__memory__.md)에서는 타이니퍼슨이 과거의 경험과 지식을 어떻게 저장하고 활용하는지 살펴보았습니다. 기억 덕분에 타이니퍼슨은 더 일관성 있고 맥락에 맞는 행동을 할 수 있게 되었죠. 하지만 때로는 타이니퍼슨이 글을 쓰거나, 복잡한 계산을 하거나, 일정을 관리하는 것처럼 특별한 능력이 필요할 때가 있습니다. 마치 우리가 스마트폰 앱이나 컴퓨터 프로그램을 사용하는 것처럼 말이죠. 이번 장에서는 타이니퍼슨이 이런 특정 작업을 수행하기 위해 사용할 수 있는 가상의 '도구(Tools)'에 대해 알아보겠습니다.

## 도구는 왜 필요할까요?

여러분이 '민준'이라는 이름의 학생 타이니퍼슨을 만들었다고 상상해 보세요. 민준이는 학교 과제로 "미래 도시의 모습"이라는 보고서를 작성해야 합니다. 그리고 보고서 작성이 끝나면, 팀 프로젝트 회의 일정을 잡아야 합니다. 만약 민준이가 직접 보고서를 한 글자씩 타이핑하고, 달력에 일일이 약속을 적는다면 매우 비효율적일 것입니다.

**핵심 사용 사례:** '민준'이는 보고서 작성을 위해 '워드 프로세서' 도구를 사용하고 싶어 합니다. 이 도구를 사용하면 쉽게 글을 쓰고, 편집하고, 저장할 수 있습니다. 또한, 팀 회의 일정을 잡기 위해서는 '캘린더' 도구를 사용하여 팀원들과 가능한 시간을 조율하고 약속을 등록하고 싶어 합니다.

이처럼 도구는 타이니퍼슨이 특정 작업을 더 효율적으로 수행할 수 있도록 도와주는 가상의 도구들입니다. 이는 마치 실제 사람이 특정 목적을 위해 소프트웨어나 물리적 도구를 사용하는 것과 유사하며, 에이전트의 행동 범위를 확장시키고 시뮬레이션을 더욱 풍부하게 만듭니다. 각 도구는 에이전트가 사용할 수 있는 특별한 행동(액션)과 그 사용 규칙(제약 조건)을 정의합니다.

## 도구의 핵심 구성 요소: `TinyTool`과 친구들

TinyTroupe에서 모든 도구는 `TinyTool`이라는 기본적인 '설계도'를 바탕으로 만들어집니다. 이 설계도를 확장하여 다양한 기능을 가진 구체적인 도구들을 만들 수 있습니다.

### 1. `TinyTool`: 모든 도구의 시작점

`TinyTool` 클래스는 모든 도구가 가져야 할 기본적인 속성과 기능을 정의합니다. 예를 들어, 도구의 이름, 설명, 소유자(만약 있다면), 그리고 실제 세상에 영향을 미치는지 여부 등을 설정할 수 있습니다. 가장 중요한 것은 각 도구가 LLM에게 "나는 이런 행동을 할 수 있어!"라고 알려주는 방법을 정의한다는 점입니다.

```python
# tinytroupe/tools/tiny_tool.py 의 일부 (개념 설명용)
class TinyTool:
    def __init__(self, name, description, owner=None, ...):
        self.name = name # 도구 이름 (예: "wordprocessor")
        self.description = description # 도구 설명
        # ... 기타 속성 ...

    def _process_action(self, agent, action: dict) -> bool:
        # 각 도구는 이 메서드를 구현하여 특정 액션을 처리합니다.
        raise NotImplementedError("자식 클래스에서 구현해야 합니다.")

    def actions_definitions_prompt(self) -> str:
        # 이 도구가 제공하는 액션에 대한 설명을 LLM에게 전달합니다.
        raise NotImplementedError("자식 클래스에서 구현해야 합니다.")

    def actions_constraints_prompt(self) -> str:
        # 이 도구의 액션 사용 규칙을 LLM에게 전달합니다.
        raise NotImplementedError("자식 클래스에서 구현해야 합니다.")
```
위 코드는 `TinyTool`의 핵심 아이디어를 보여줍니다. 실제 도구를 만들 때는 이 `TinyTool`을 상속받아 `_process_action`, `actions_definitions_prompt`, `actions_constraints_prompt` 메서드를 구체적으로 구현해야 합니다.

### 2. 구체적인 도구들: 워드 프로세서와 캘린더

TinyTroupe에는 몇 가지 기본적인 도구들이 미리 준비되어 있습니다.

*   **`TinyWordProcessor` (타이니 워드 프로세서)**:
    *   설명: 문서를 작성하고 편집하는 데 사용되는 도구입니다.
    *   주요 액션: `WRITE_DOCUMENT` (문서 작성)
    *   사용 예시: 타이니퍼슨이 보고서, 이메일, 이야기 등을 작성할 때 활용합니다.

*   **`TinyCalendar` (타이니 캘린더)**:
    *   설명: 일정, 약속, 회의 등을 관리하는 데 사용되는 도구입니다.
    *   주요 액션: `CREATE_EVENT` (일정 생성)
    *   사용 예시: 타이니퍼슨이 친구와의 약속을 잡거나, 회의 일정을 등록할 때 활용합니다.

이 외에도 필요에 따라 여러분만의 맞춤형 도구를 `TinyTool`을 상속받아 만들 수 있습니다! 예를 들어, '계산기 도구', '그림판 도구' 등 상상하는 모든 것을 구현할 수 있습니다.

## 타이니퍼슨에게 도구 장착하고 사용하기

타이니퍼슨이 도구를 사용하려면, 먼저 해당 도구를 '가지고' 있어야 합니다. 이는 [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)에서 배운 `TinyToolUse`라는 특별한 정신 능력을 통해 이루어집니다.

### 1. 도구 사용 능력 부여하기

먼저, 사용할 도구 객체들을 만듭니다. 그리고 이 도구들을 리스트에 담아 `TinyToolUse` 정신 능력을 생성한 후, 타이니퍼슨에게 추가합니다.

```python
from tinytroupe.agent import TinyPerson
from tinytroupe.agent.mental_faculty import TinyToolUse # 도구 사용 정신 능력
from tinytroupe.tools import TinyWordProcessor, TinyCalendar # 실제 도구들

# '민준'이라는 타이니퍼슨 생성
minjun = TinyPerson(name="민준")

# 사용할 도구들 생성
word_processor = TinyWordProcessor(owner=minjun) # 민준이가 주인인 워드프로세서
calendar = TinyCalendar(owner=minjun)           # 민준이가 주인인 캘린더

# 도구 사용 정신 능력 생성 및 민준이에게 추가
tool_faculty = TinyToolUse(tools=[word_processor, calendar])
minjun.add_mental_faculty(tool_faculty)

print(f"{minjun.name}은(는) 이제 {len(tool_faculty.tools)}개의 도구를 사용할 수 있습니다.")
```
이제 '민준'이는 워드 프로세서와 캘린더를 사용할 수 있는 능력을 갖추게 되었습니다! `owner=minjun`은 이 도구들이 '민준'의 것이라는 의미입니다. (도구에 따라 소유자 없이 공용으로 사용할 수도 있습니다.)

### 2. 타이니퍼슨은 어떻게 도구를 사용하기로 결정할까요?

타이니퍼슨은 스스로 "아, 지금은 워드 프로세서를 써야겠다!"라고 판단하지 않습니다. 대신, 타이니퍼슨의 '뇌' 역할을 하는 LLM이 상황을 보고 어떤 도구의 어떤 기능을 사용해야 할지 결정합니다.

`TinyToolUse` 정신 능력은 자신이 가진 모든 도구(여기서는 워드 프로세서와 캘린더)에게 "너희가 할 수 있는 액션이랑 사용 규칙 좀 알려줘"라고 물어봅니다. 각 도구는 자신의 `actions_definitions_prompt()`와 `actions_constraints_prompt()` 메서드를 통해 이 정보를 제공합니다.

예를 들어, `TinyWordProcessor`는 다음과 같이 알려줄 수 있습니다:
*   정의: `WRITE_DOCUMENT: 문서를 만들 수 있습니다. 제목, 내용, 작성자 등을 JSON 형식으로 알려줘야 합니다.`
*   규칙: `WRITE_DOCUMENT를 할 때는 내용을 한번에 다 써야 하고, 자세하게 써야 합니다.`

이 모든 정보는 타이니퍼슨의 기본 지침(시스템 프롬프트)에 포함되어 LLM에게 전달됩니다. 따라서 LLM은 이제 "민준이가 보고서를 써야 하는 상황이군. `TinyWordProcessor`의 `WRITE_DOCUMENT` 액션을 사용해서 이렇게 시켜야겠다!"라고 생각할 수 있게 됩니다.

### 3. 예시: `TinyWordProcessor`로 보고서 작성하기

민준이가 "미래 도시 보고서"를 작성해야 하는 상황입니다.

```python
import tinytroupe.control as control
import json # JSON 형식의 액션 내용을 만들기 위해 import

control.begin() # 시뮬레이션 시작 (LLM 호출 캐싱 등)

# 민준이에게 보고서 작성 임무 부여 (사용자 입력)
task_prompt = "민준아, '미래 도시의 모습'이라는 제목으로 보고서를 작성해줘. 내용은 자유롭게 상상해서 써보고, 작성자는 너의 이름으로 해줘."
print(f"사용자: {task_prompt}")

# 민준이가 듣고 행동 (LLM이 WRITE_DOCUMENT 액션을 생성할 것을 기대)
minjun.listen_and_act(task_prompt)

# 예상되는 민준이의 행동 (LLM이 생성):
# 민준 acts: [THOUGHT] '미래 도시의 모습' 보고서를 작성해야겠다. 워드프로세서 도구를 사용하자.
# 민준 acts: [USE_TOOL] wordprocessor (action="WRITE_DOCUMENT", content={"title": "미래 도시의 모습", "content": "## 서론\n미래 도시는...", "author": "민준"})
# (TinyToolUse가 이 액션을 TinyWordProcessor에게 전달하여 처리)
# 민준 acts: [THOUGHT] 보고서 작성이 완료되었다.
# 민준 acts: [TALK] 네, '미래 도시의 모습' 보고서 작성을 완료했어요!

control.end()
```
위 코드에서 `minjun.listen_and_act(task_prompt)`가 실행되면, LLM은 상황을 판단하고 `TinyWordProcessor`를 사용하기로 결정할 가능성이 높습니다. 그러면 LLM은 다음과 유사한 `USE_TOOL` 액션을 생성할 수 있습니다. (실제 `USE_TOOL` 액션은 LLM의 출력 형식에 따라 조금 다를 수 있지만, 개념적으로는 도구 이름과 수행할 액션, 그리고 그 내용을 포함합니다. TinyTroupe에서는 도구 사용 액션이 조금 더 직접적으로 `WRITE_DOCUMENT`와 같은 형태로 나올 수 있습니다.)

LLM이 생성하는 구체적인 액션 형식은 다음과 같을 수 있습니다 (도구의 `actions_definitions_prompt`에 따라 달라짐):

```json
// LLM이 WRITE_DOCUMENT 액션에 대해 생성할 수 있는 내용(content)의 예시
{
  "title": "미래 도시의 모습",
  "content": "## 서론\n2077년, 미래 도시는 기술과 자연이 조화를 이루는...\n\n## 본론\n1. 스마트 교통 시스템...\n2. 친환경 에너지...\n\n## 결론\n미래 도시는...",
  "author": "민준"
}
```
이 `WRITE_DOCUMENT` 액션과 내용은 `TinyToolUse` 정신 능력을 통해 `TinyWordProcessor`의 `_process_action` 메서드로 전달됩니다. `TinyWordProcessor`는 이 정보를 받아 실제로 "문서 작성"이라는 작업을 수행합니다. 만약 `TinyWordProcessor`에 `exporter`가 설정되어 있다면, 작성된 문서는 파일(예: `.md`, `.docx`, `.json`)로 저장될 수도 있습니다.

### 4. 예시: `TinyCalendar`로 회의 일정 잡기

이번에는 민준이가 팀 프로젝트 회의를 다음 주 월요일 오전 10시에 잡아야 하는 상황입니다.

```python
# (이전 코드에 이어서, 시뮬레이션은 시작된 상태, 민준이에게 캘린더 도구가 있음)
# control.begin()

# 민준이에게 회의 일정 등록 임무 부여
schedule_prompt = "민준아, 다음 주 월요일 오전 10시에 '팀 프로젝트 회의' 일정을 너의 캘린더에 등록해줘. 참석자는 너와 '지수'야."
print(f"사용자: {schedule_prompt}")

minjun.listen_and_act(schedule_prompt)

# 예상되는 민준이의 행동 (LLM이 생성):
# 민준 acts: [THOUGHT] 팀 프로젝트 회의 일정을 캘린더에 등록해야겠다.
# 민준 acts: [USE_TOOL] calendar (action="CREATE_EVENT", content={"title": "팀 프로젝트 회의", "mandatory_attendees": ["민준", "지수"], "start_time": "다음 주 월요일 오전 10시"})
# (TinyToolUse가 이 액션을 TinyCalendar에게 전달하여 처리)
# 민준 acts: [THOUGHT] 회의 일정이 캘린더에 등록되었다.
# 민준 acts: [TALK] 네, 다음 주 월요일 오전 10시 팀 프로젝트 회의 일정을 캘린더에 등록했어요!

# control.end()
```
LLM은 이번에도 상황에 맞는 `CREATE_EVENT` 액션을 생성할 것입니다. `content` 부분은 다음과 유사한 JSON 형식이 될 수 있습니다:

```json
// LLM이 CREATE_EVENT 액션에 대해 생성할 수 있는 내용(content)의 예시
{
  "title": "팀 프로젝트 회의",
  "description": "팀 프로젝트 진행 상황 공유 및 다음 단계 논의",
  "mandatory_attendees": ["민준", "지수"],
  "start_time": "다음 주 월요일 오전 10:00",
  "end_time": "다음 주 월요일 오전 11:00" 
}
```
이 정보는 `TinyCalendar`의 `_process_action` 메서드로 전달되어, `TinyCalendar` 내부의 `self.calendar` 딕셔너리에 새로운 일정이 추가됩니다. (실제 날짜/시간 파싱은 더 복잡할 수 있으며, 여기서는 개념 설명을 위해 단순화했습니다.)

## 도구는 어떻게 작동할까요? 내부 동작 살펴보기

타이니퍼슨이 도구를 사용하는 과정은 `TinyToolUse` 정신 능력과 각 도구의 긴밀한 협력을 통해 이루어집니다.

### 1. 비-코드 흐름도 (Non-code Walkthrough)

1.  **자극 수신**: 타이니퍼슨('민준')이 사용자로부터 요청(예: "보고서 써줘")을 받습니다.
2.  **LLM 호출 (행동 결정)**: '민준'은 자신의 페르소나, 현재 상황, 그리고 `TinyToolUse`를 통해 알게 된 사용 가능한 도구 액션들(예: `WRITE_DOCUMENT`, `CREATE_EVENT`)을 종합적으로 고려하여 LLM에게 다음 행동을 요청합니다.
3.  **도구 사용 액션 생성**: LLM이 특정 도구를 사용하기로 결정하면, 해당 도구의 액션(예: `WRITE_DOCUMENT`)과 필요한 내용(예: 보고서 제목, 내용)을 포함하는 응답을 생성합니다.
4.  **`TinyToolUse`의 액션 처리**: '민준'의 `act()` 메서드 내에서, 이 액션은 `TinyToolUse` 정신 능력의 `process_action()` 메서드에 전달됩니다.
5.  **적절한 도구 찾기**: `TinyToolUse`는 자신이 가지고 있는 도구들(`self.tools` 리스트)을 하나씩 살펴보면서, 현재 액션을 처리할 수 있는 도구를 찾습니다.
    *   예를 들어, 액션 타입이 `WRITE_DOCUMENT`이면 `TinyWordProcessor`가 "이건 내 일이야!"라고 반응합니다.
6.  **도구의 작업 수행**: 해당 도구(예: `TinyWordProcessor`)의 `_process_action()` 메서드가 호출되고, 액션 내용(보고서 제목, 내용 등)이 전달됩니다. 도구는 이 정보를 바탕으로 자신의 주된 작업(예: 문서 "작성")을 수행합니다.
7.  **(선택 사항) 결과 알림**: 도구는 작업 결과를 에이전트에게 알릴 수도 있습니다. 예를 들어, `agent.think("문서 작성이 완료되었습니다.")`와 같이 에이전트의 다음 생각에 영향을 줄 수 있습니다. (이 부분은 현재 `TinyTool` 구현에서는 명시적이지 않을 수 있지만, 개념적으로 가능합니다.)
8.  **후속 행동**: 에이전트는 도구 사용 결과를 바탕으로 다음 행동(예: 사용자에게 보고)을 결정합니다.

### 2. 순서도 (Sequence Diagram)

다음은 민준이가 워드 프로세서로 보고서를 작성하는 과정을 보여주는 순서도입니다.

```mermaid
sequenceDiagram
    participant User as 사용자
    participant Minjun as 민준 (타이니퍼슨)
    participant LLM as 대규모 언어 모델
    participant ToolUseF as 도구 사용 능력 (TinyToolUse)
    participant WordP as 워드 프로세서 (TinyWordProcessor)

    User->>Minjun: "보고서 써줘" (listen_and_act)
    Minjun->>LLM: 행동 요청 (페르소나, 상황, 사용 가능 도구 액션[WRITE_DOCUMENT 등] 기반)
    LLM-->>Minjun: 행동 제안: `{"type": "WRITE_DOCUMENT", "content": {"title":"보고서 제목", ...}}`
    Minjun->>Minjun: `act()` 내부에서 정신 능력 처리 루프 실행
    Minjun->>ToolUseF: `process_action({"type": "WRITE_DOCUMENT", ...})` 호출
    ToolUseF->>WordP: `process_action({"type": "WRITE_DOCUMENT", ...})` 호출 (WordP가 이 액션을 처리 가능하다고 판단)
    WordP->>WordP: `write_document(title="보고서 제목", ...)` 내부 로직 실행 (문서 "작성")
    Note over WordP: (선택) 작성 결과를 파일로 저장 (exporter 사용 시)
    WordP-->>ToolUseF: 처리 완료 (True 반환)
    ToolUseF-->>Minjun: 처리 완료 (True 반환)
    Minjun->>LLM: 다음 행동 요청 (보고서 작성 완료 상황 기반)
    LLM-->>Minjun: 행동 제안: `{"type": "TALK", "content": "보고서 작성을 완료했습니다."}`
    Minjun-->>User: "보고서 작성을 완료했습니다." (화면 출력)
end
```

### 3. 코드 내부 살펴보기

이제 실제 코드에서 이 과정이 어떻게 구현되어 있는지 몇 가지 핵심 부분을 살펴보겠습니다.

*   **`TinyTool` (기본 도구 클래스 - `tinytroupe/tools/tiny_tool.py`)**:
    모든 도구의 기초가 됩니다.

    ```python
    # tinytroupe/tools/tiny_tool.py 일부
    class TinyTool(JsonSerializableRegistry):
        def __init__(self, name, description, owner=None, real_world_side_effects=False, exporter=None, enricher=None):
            self.name = name
            self.description = description
            self.owner = owner # 도구 소유 에이전트
            self.real_world_side_effects = real_world_side_effects # 실제 세상에 영향 여부
            self.exporter = exporter # 결과물 외부 저장용 (예: 파일)
            self.enricher = enricher # 결과물 내용 보강용 (예: LLM으로 더 길게 쓰기)

        def _process_action(self, agent, action: dict) -> bool:
            # 자식 클래스에서 반드시 구현해야 할 핵심 로직
            raise NotImplementedError("Subclasses must implement this method.")
        
        # LLM에게 액션 정의를 알려주는 프롬프트
        def actions_definitions_prompt(self) -> str:
            raise NotImplementedError("Subclasses must implement this method.")
        
        # LLM에게 액션 사용 제약 조건을 알려주는 프롬프트
        def actions_constraints_prompt(self) -> str:
            raise NotImplementedError("Subclasses must implement this method.")

        def process_action(self, agent, action: dict) -> bool:
            # 실제 _process_action 호출 전에 몇 가지 안전장치/확인사항 수행
            self._protect_real_world() # 실제 세상 영향 경고 (필요시)
            self._enforce_ownership(agent) # 소유권 확인 (필요시)
            return self._process_action(agent, action) # 실제 작업 처리 위임
    ```
    `process_action` 메서드가 외부에서 호출되면, 내부적으로 소유권 등을 확인한 후 실제 작업은 자식 클래스에 구현된 `_process_action`에게 넘기는 구조입니다.

*   **`TinyWordProcessor` (워드 프로세서 도구 - `tinytroupe/tools/tiny_word_processor.py`)**:
    `TinyTool`을 상속받아 문서 작성 기능을 구현합니다.

    ```python
    # tinytroupe/tools/tiny_word_processor.py 일부
    class TinyWordProcessor(TinyTool):
        def __init__(self, owner=None, exporter=None, enricher=None):
            super().__init__("wordprocessor", "문서 작성 도구.", owner, False, exporter, enricher)
            
        def write_document(self, title, content, author=None):
            # 실제 문서 작성 로직 (간단히 로깅만)
            logger.debug(f"문서 작성 중: 제목 '{title}', 내용: '{content[:50]}...'")
            if self.exporter: # exporter가 있다면
                # ... 문서를 파일로 저장하는 로직 (예: md, docx, json) ...
                self.exporter.export(artifact_name=title, artifact_data=content, ...)

        def _process_action(self, agent, action: dict) -> bool:
            if action['type'] == "WRITE_DOCUMENT" and action['content'] is not None:
                doc_spec = utils.extract_json(action['content']) # JSON 내용 파싱
                valid_keys = ["title", "content", "author"]
                utils.check_valid_fields(doc_spec, valid_keys) # 유효한 필드인지 확인
                self.write_document(**doc_spec) # write_document 메서드 호출
                return True # 처리 성공
            return False # 이 도구가 처리할 액션 아님

        def actions_definitions_prompt(self) -> str:
            return utils.dedent("""
            - WRITE_DOCUMENT: 새 문서를 만듭니다. 내용은 JSON 형식이어야 합니다.
                * title: 문서 제목 (필수).
                * content: 실제 문서 내용 (마크다운 사용, 필수).
                * author: 작성자 (선택 사항, 본인 이름 권장).
            """)
        
        def actions_constraints_prompt(self) -> str:
            return utils.dedent("""
            - WRITE_DOCUMENT 시, 모든 내용을 한 번에 작성해야 합니다.
            - 내용은 특별한 이유가 없는 한 길고 상세해야 합니다.
            - JSON 내용에는 유효한 이스케이프 시퀀스만 사용해야 합니다.
            """)
    ```
    `_process_action` 메서드에서 액션 타입이 `WRITE_DOCUMENT`인지 확인하고, 그렇다면 JSON으로 된 내용을 파싱하여 `write_document` 함수를 호출하는 것을 볼 수 있습니다. `actions_definitions_prompt`와 `actions_constraints_prompt`는 LLM에게 이 도구를 어떻게 사용해야 하는지 알려줍니다.

*   **`TinyCalendar` (캘린더 도구 - `tinytroupe/tools/tiny_calendar.py`)**:
    비슷한 구조로 일정 관리 기능을 제공합니다. `CREATE_EVENT` 액션을 처리합니다.

    ```python
    # tinytroupe/tools/tiny_calendar.py 일부
    class TinyCalendar(TinyTool):
        def __init__(self, owner=None):
            super().__init__("calendar", "일정 관리 도구.", owner, False)
            self.calendar = {} # {날짜: [이벤트_딕셔너리_리스트]} 형태

        def add_event(self, date_key, title, description=None, ...): # 실제 날짜 파싱 필요
            if date_key not in self.calendar:
                self.calendar[date_key] = []
            self.calendar[date_key].append({"title": title, ...})
            logger.debug(f"'{date_key}'에 '{title}' 이벤트 추가됨.")

        def _process_action(self, agent, action: dict) -> bool:
            if action['type'] == "CREATE_EVENT" and action['content'] is not None:
                event_content = json.loads(action['content']) # JSON 파싱
                # ... (유효 필드 확인 및 날짜/시간 처리) ...
                # 실제로는 event_content에서 날짜 정보를 추출하여 date_key로 사용해야 함
                self.add_event(event_content.get("start_time", "미정"), **event_content)
                return True
            return False

        def actions_definitions_prompt(self) -> str:
            return utils.dedent("""
            - CREATE_EVENT: 새 일정을 만듭니다. 내용은 JSON 형식이어야 합니다.
                * title: 일정 제목 (필수).
                * description: 설명 (선택).
                * mandatory_attendees: 필수 참석자 목록 (선택).
                * start_time: 시작 시간 (선택).
            """)
        # ... actions_constraints_prompt() ...
    ```

*   **`TinyToolUse` (도구 사용 정신 능력 - `tinytroupe/agent/mental_faculty.py`)**:
    이 정신 능력은 여러 도구들을 관리하고, 에이전트의 액션을 적절한 도구에게 전달하는 역할을 합니다.

    ```python
    # tinytroupe/agent/mental_faculty.py 의 TinyToolUse 클래스 일부
    class TinyToolUse(TinyMentalFaculty):
        def __init__(self, tools:list) -> None: # 도구 리스트를 받음
            super().__init__("Tool Use")
            self.tools = tools # [TinyWordProcessor객체, TinyCalendar객체]
        
        def process_action(self, agent, action: dict) -> bool:
            # 자신이 가진 모든 도구에게 현재 액션을 처리할 수 있는지 물어봄
            for tool in self.tools:
                if tool.process_action(agent, action): # 도구가 액션을 처리했다면
                    return True # 성공 반환
            return False # 어떤 도구도 이 액션을 처리하지 못함
        
        def actions_definitions_prompt(self) -> str:
            # 모든 도구의 액션 정의를 모아서 반환
            prompt = ""
            for tool in self.tools:
                prompt += tool.actions_definitions_prompt()
            return prompt
        
        def actions_constraints_prompt(self) -> str:
            # 모든 도구의 액션 제약 조건을 모아서 반환
            prompt = ""
            for tool in self.tools:
                prompt += tool.actions_constraints_prompt()
            return prompt
    ```
    `process_action` 메서드가 핵심입니다. 에이전트로부터 액션을 받으면, `self.tools` 리스트에 있는 각 도구의 `process_action`을 차례로 호출합니다. 만약 어떤 도구가 해당 액션을 성공적으로 처리하면 (True를 반환하면), `TinyToolUse`도 True를 반환하며 작업이 완료되었음을 알립니다. 또한, LLM에게 전달할 프롬프트도 모든 도구의 정보를 종합하여 생성합니다.

## 정리 및 다음 단계

이번 장에서는 타이니퍼슨이 특정 작업을 수행하기 위해 사용할 수 있는 '도구 (Tools)'에 대해 배웠습니다. `TinyTool`이라는 기본 설계도를 바탕으로 `TinyWordProcessor`(문서 작성), `TinyCalendar`(일정 관리)와 같은 구체적인 도구들이 어떻게 만들어지고 작동하는지 살펴보았습니다. 타이니퍼슨은 [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)에서 배운 `TinyToolUse` 정신 능력을 통해 이러한 도구들을 사용할 수 있게 되며, LLM은 각 도구가 제공하는 액션 정의와 제약 조건을 바탕으로 상황에 맞는 도구 사용을 지시합니다. 이를 통해 타이니퍼슨은 마치 실제 사람이 소프트웨어를 사용하듯 자신의 능력을 확장하고 더 복잡한 작업을 수행할 수 있게 됩니다.

**핵심 요약:**
*   도구는 타이니퍼슨이 특정 작업을 수행하도록 돕는 가상의 도구들입니다 (예: 워드 프로세서, 캘린더).
*   모든 도구는 `TinyTool`을 기반으로 하며, 각 도구는 고유한 액션과 사용 규칙을 정의합니다.
*   타이니퍼슨은 `TinyToolUse` 정신 능력을 통해 도구를 사용할 수 있습니다.
*   LLM은 도구가 제공하는 액션 정의/규칙을 보고, 상황에 맞게 `WRITE_DOCUMENT` 또는 `CREATE_EVENT` 같은 액션을 생성하여 도구 사용을 지시합니다.
*   `TinyToolUse`는 이 액션을 적절한 도구의 `_process_action` 메서드로 전달하여 실제 작업을 수행하게 합니다.

이것으로 `07_TinyTroupe` 튜토리얼 시리즈의 모든 장을 마쳤습니다! 여러분은 이제 시뮬레이션을 제어하고([제1장: 시뮬레이션 제어 (Simulation Control)](01_시뮬레이션_제어__simulation_control__.md)), 개성 있는 타이니퍼슨을 만들며([제2장: 타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md), [제5장: 타이니퍼슨 팩토리 (TinyPerson Factory)](05_타이니퍼슨_팩토리__tinyperson_factory__.md)), 그들이 살아갈 세계를 구축하고([제3장: 타이니월드 (TinyWorld)](03_타이니월드__tinyworld__.md)), LLM을 통해 지능을 부여하며([제4장: OpenAI 유틸리티 (OpenAI Utilities)](04_openai_유틸리티__openai_utilities__.md)), 정신 능력([제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)), 기억([제7장: 기억 (Memory)](07_기억__memory__.md)), 그리고 오늘 배운 도구까지 활용하여 더욱 풍부하고 현실적인 에이전트 기반 시뮬레이션을 만들 수 있는 기초를 다졌습니다.

`TinyTroupe` 프로젝트는 여러분이 상상하는 다양한 시나리오와 에이전트들을 실험해 볼 수 있는 강력한 플랫폼입니다. 지금까지 배운 내용들을 바탕으로 자신만의 독창적인 시뮬레이션을 만들어보고, 에이전트들이 만들어가는 흥미로운 이야기들을 관찰해 보세요. 이 작은 세계 속에서 무한한 가능성이 여러분을 기다리고 있습니다!

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)