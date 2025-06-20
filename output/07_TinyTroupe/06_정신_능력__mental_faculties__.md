# Chapter 6: 정신 능력 (Mental Faculties)


이전 [제5장: 타이니퍼슨 팩토리 (TinyPerson Factory)](05_타이니퍼슨_팩토리__tinyperson_factory__.md)에서는 다양한 페르소나를 가진 타이니퍼슨들을 효율적으로 생성하는 방법을 배웠습니다. 이제 우리는 개성 넘치는 캐릭터들을 만들 수 있지만, 이들이 단순히 주어진 정보에 반응하는 것을 넘어, 마치 사람처럼 더 깊이 생각하고, 기억을 활용하며, 주변 정보를 탐색하는 등 복잡한 인지 활동을 하려면 어떻게 해야 할까요? 바로 여기서 '정신 능력(Mental Faculties)'이 등장합니다.

## 정신 능력이란 무엇이고 왜 필요할까요?

여러분이 '지혜'라는 이름의 학생 타이니퍼슨을 만들었다고 상상해 보세요. 지혜가 단순히 현재 대화 내용에만 반응하는 것이 아니라, 이전에 배웠던 수업 내용을 '기억'해내서 질문에 답하거나, '참고 자료' 파일을 열어 특정 용어의 정의를 찾아보고, 심지어 '계산기' 도구를 사용해 수학 문제를 푼다면 훨씬 더 똑똑하고 현실적인 학생처럼 보일 것입니다.

**핵심 사용 사례:** '지혜'는 어제 역사 수업에서 배운 내용을 바탕으로 오늘 퀴즈에 답해야 합니다. 또한, 선생님이 나눠준 '용어 해설집.txt' 파일에서 '르네상스'의 정확한 의미를 찾아보고 싶어 합니다. 복잡한 계산 문제는 직접 풀기보다 '계산기' 도구를 사용하고 싶어 합니다. 이런 상황에서 '정신 능력'은 지혜가 과거를 회상하고, 파일을 참조하며, 도구를 사용하는 등의 고등 인지 기능을 수행할 수 있도록 돕는 핵심 요소입니다.

정신 능력은 타이니퍼슨이 가진 다양한 인지적 능력을 나타냅니다. 이는 `TinyMentalFaculty`라는 기반 클래스를 바탕으로 하며, 다음과 같은 구체적인 능력들이 포함될 수 있습니다:

*   **회상 능력 (`RecallFaculty`):** 과거의 기억(예: 이전 대화, 학습 내용)을 떠올리는 능력입니다. "어제 무엇을 배웠지?" 하고 스스로에게 묻는 것과 같습니다.
*   **파일 및 웹 참조 능력 (`FilesAndWebGroundingFaculty`):** 로컬 파일이나 웹 페이지에서 정보를 찾아보는 능력입니다. 마치 책이나 인터넷에서 자료를 검색하는 것과 같습니다.
*   **도구 사용 능력 (`TinyToolUse`):** 특정 도구(예: 계산기, 워드 프로세서)를 사용하는 능력입니다. 이 능력 덕분에 타이니퍼슨은 직접 수행하기 어려운 작업을 도구의 힘을 빌려 해결할 수 있습니다. ([제8장: 도구 (Tools)](08_도구__tools__.md)에서 더 자세히 다룹니다.)

각 정신 능력은 타이니퍼슨 에이전트가 더 복잡하고 현실적인 행동을 할 수 있도록 돕는 전문 기술과 같습니다. 이 장에서는 이러한 정신 능력을 타이니퍼슨에게 어떻게 부여하고 사용하는지 알아보겠습니다.

## 타이니퍼슨에게 정신 능력 부여하기

정신 능력은 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md) 객체를 만들 때 직접 추가하거나, 객체를 만든 후에 `add_mental_faculty()` 메서드를 사용하여 추가할 수 있습니다.

먼저, 필요한 정신 능력 클래스들을 가져옵니다.

```python
from tinytroupe.agent import TinyPerson, RecallFaculty, FilesAndWebGroundingFaculty, TinyToolUse
# TinyToolUse를 위해서는 실제 도구 클래스도 필요하지만, 여기서는 개념만 설명합니다.
# from tinytroupe.tools import CalculatorTool # 예시 도구 (제8장에서 자세히 다룸)
```

이제 '지혜'라는 타이니퍼슨을 만들고, 회상 능력과 파일 참조 능력을 추가해 보겠습니다.

```python
# 지혜라는 이름의 타이니퍼슨 생성
jihye = TinyPerson(name="지혜")

# 회상 능력 추가
recall_faculty = RecallFaculty()
jihye.add_mental_faculty(recall_faculty)

# 파일 참조 능력 추가 (예: 'study_materials' 폴더를 참조하도록 설정)
# 실제 사용 시에는 해당 폴더에 파일이 있어야 합니다.
grounding_faculty = FilesAndWebGroundingFaculty(folders_paths=["./study_materials"])
jihye.add_mental_faculty(grounding_faculty)

# 도구 사용 능력 추가 (개념적 예시)
# calculator = CalculatorTool() # 실제로는 도구 객체 생성
# tool_use_faculty = TinyToolUse(tools=[calculator])
# jihye.add_mental_faculty(tool_use_faculty)

print(f"{jihye.name}에게 {len(jihye._mental_faculties)}개의 정신 능력이 추가되었습니다.")
```
이제 '지혜'는 기억을 회상하고, 지정된 폴더의 파일을 참조할 수 있는 능력을 갖추게 되었습니다!

## 정신 능력 활용하기: 더 똑똑해진 타이니퍼슨

정신 능력을 갖춘 타이니퍼슨은 이제 대규모 언어 모델(LLM)에게 단순히 '말하기'나 '생각하기' 외에 더 다양한 행동을 지시받을 수 있습니다. LLM은 각 정신 능력이 제공하는 특별한 행동(예: `RECALL`, `CONSULT`)을 페르소나와 상황에 맞게 사용하도록 학습됩니다.

### 1. 회상 능력 (`RecallFaculty`) 사용하기

'지혜'가 어제 배운 내용을 기억해내야 하는 상황을 가정해 봅시다.

```python
import tinytroupe.control as control

# 시뮬레이션 시작 (LLM 호출 캐싱 등)
control.begin()

# 지혜에게 질문하기
user_question = "지혜야, 어제 역사 수업에서 배운 중요한 사건이 뭐였니?"
print(f"사용자: {user_question}")

# 지혜가 질문을 듣고 행동 (내부적으로 RECALL 액션을 사용할 수 있음)
jihye.listen_and_act(user_question)
# 예상되는 지혜의 행동 (LLM 생성):
# 지혜 acts: [THOUGHT] 어제 역사 수업 내용을 떠올려 봐야겠다.
# 지혜 acts: [RECALL] 어제 역사 수업 중요 사건
# (RecallFaculty가 작동하여 관련 기억을 찾고, 그 내용으로 THINK 액션을 유도)
# 지혜 acts: [THOUGHT] 아, 어제는 프랑스 혁명에 대해 배웠지! 중요한 사건은 바스티유 감옥 습격이었어.
# 지혜 acts: [TALK] 어제 역사 수업에서는 프랑스 혁명에 대해 배웠어요. 가장 중요한 사건은 바스티유 감옥 습격이었던 것 같아요!

control.end()
```
위 예시에서 `jihye.listen_and_act(user_question)`가 호출되면, '지혜'의 LLM은 질문에 답하기 위해 과거 기억을 참조해야 한다고 판단할 수 있습니다. 그러면 LLM은 `RECALL` 액션을 생성하고, `RecallFaculty`의 `process_action` 메서드가 실행됩니다. 이 메서드는 '지혜'의 [기억 (Memory)](07_기억__memory__.md) (특히 의미 기억)에서 "어제 역사 수업 중요 사건"과 관련된 정보를 검색합니다. 검색된 정보는 '지혜'의 다음 `THINK` 액션의 내용으로 활용되어, 최종적으로 질문에 대한 답변을 생성하는 데 사용됩니다.

### 2. 파일 및 웹 참조 능력 (`FilesAndWebGroundingFaculty`) 사용하기

이번에는 '지혜'가 '용어 해설집.txt' 파일에서 '르네상스'의 정의를 찾아보는 상황입니다. `study_materials` 폴더에 다음과 같은 내용의 `glossary.txt` 파일이 있다고 가정합니다.

```
# glossary.txt 내용 예시
르네상스: 14세기부터 16세기에 걸쳐 이탈리아를 중심으로 유럽에서 일어난 문예 부흥 운동.
바로크: 17세기 유럽에서 유행한 예술 양식.
```

```python
# (이전 코드에 이어서, 시뮬레이션은 시작된 상태, jihye에게 grounding_faculty가 추가된 상태)

# 파일 참조 능력을 사용하도록 유도하는 상황
user_request = "지혜야, '르네상스'가 정확히 무슨 뜻인지 'glossary.txt' 파일에서 찾아줄 수 있니?"
print(f"사용자: {user_request}")

jihye.listen_and_act(user_request)
# 예상되는 지혜의 행동 (LLM 생성):
# 지혜 acts: [THOUGHT] 'glossary.txt' 파일에서 '르네상스'를 찾아봐야겠다.
# 지혜 acts: [LIST_DOCUMENTS] # 사용 가능한 문서 목록 확인 (선택적)
# 지혜 acts: [THOUGHT] 사용 가능한 문서 중에 'glossary.txt'가 있네.
# 지혜 acts: [CONSULT] glossary.txt
# (FilesAndWebGroundingFaculty가 glossary.txt 파일 내용을 읽어 THINK 액션 유도)
# 지혜 acts: [THOUGHT] 파일 내용: "르네상스: 14세기부터 16세기에 걸쳐 이탈리아를 중심으로 유럽에서 일어난 문예 부흥 운동."
# 지혜 acts: [TALK] 네, 'glossary.txt' 파일을 찾아봤어요. '르네상스'는 14세기부터 16세기에 걸쳐 이탈리아를 중심으로 유럽에서 일어난 문예 부흥 운동을 의미한대요.

# control.end() # 실제로는 이전 예제에서 이미 호출됨
```
사용자가 특정 파일(`glossary.txt`)을 언급하며 정보를 요청하면, LLM은 `CONSULT` 액션을 생성할 가능성이 높습니다. `FilesAndWebGroundingFaculty`의 `process_action`은 지정된 파일을 읽어 그 내용을 '지혜'의 다음 생각으로 전달하고, 이를 바탕으로 '지혜'는 답변을 생성합니다. `LIST_DOCUMENTS` 액션은 사용 가능한 문서 목록을 먼저 확인하는 데 사용될 수 있습니다.

### 3. 도구 사용 능력 (`TinyToolUse`)

'지혜'가 복잡한 수학 문제를 '계산기' 도구를 사용해 푸는 상황을 생각해 봅시다. ([제8장: 도구 (Tools)](08_도구__tools__.md)에서 도구 생성 및 사용법을 자세히 다룹니다.)

```python
# (개념 설명용 코드 - 실제 도구 연동은 제8장 참조)
# calculator_tool = CalculatorTool() # 가상의 계산기 도구
# tool_use_faculty = TinyToolUse(tools=[calculator_tool])
# jihye.add_mental_faculty(tool_use_faculty) # 지혜에게 도구 사용 능력 추가

# control.begin() # 시뮬레이션 시작

user_problem = "지혜야, 123 곱하기 456은 얼마인지 계산기로 계산해 줄래?"
print(f"사용자: {user_problem}")

jihye.listen_and_act(user_problem)
# 예상되는 지혜의 행동 (LLM 생성):
# 지혜 acts: [THOUGHT] 계산기를 사용해서 123 * 456을 계산해야겠다.
# 지혜 acts: [USE_TOOL] CalculatorTool (action="calculate", expression="123 * 456")
# (TinyToolUse 및 CalculatorTool이 계산을 수행하고 결과를 THINK 액션으로 유도)
# 지혜 acts: [THOUGHT] 계산 결과는 56088 이야.
# 지혜 acts: [TALK] 계산기로 계산해 보니 123 곱하기 456은 56088이에요!

# control.end()
```
LLM이 `USE_TOOL`과 같이 특정 도구를 사용하는 액션을 생성하면, `TinyToolUse` 능력은 해당 도구의 기능을 실행하고 그 결과를 에이전트에게 알려줍니다.

## 정신 능력은 LLM 프롬프트에 어떻게 영향을 줄까요?

타이니퍼슨의 LLM은 어떻게 이 새로운 능력들(RECALL, CONSULT 등)을 알고 사용하는 걸까요? 비밀은 각 정신 능력이 제공하는 '정의(definitions)'와 '제약 조건(constraints)' 프롬프트에 있습니다.

*   `actions_definitions_prompt()`: 각 정신 능력은 자신이 제공하는 새로운 액션의 이름과 설명을 반환합니다. 예를 들어, `RecallFaculty`는 "RECALL: 기억에서 정보를 회상합니다. 'mental query'를 지정해야 합니다." 와 같은 설명을 제공합니다.
*   `actions_constraints_prompt()`: 각 정신 능력은 해당 액션을 언제, 어떻게 사용해야 하는지에 대한 규칙이나 팁을 제공합니다. 예를 들어, "모르는 것을 단정하기 전에 반드시 RECALL을 시도해야 합니다." 와 같은 내용입니다.

이 정보들은 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md)이 자신의 시스템 프롬프트(LLM에게 전달되는 기본 지침)를 생성할 때 (`generate_agent_system_prompt()` 메서드 내에서) 포함됩니다.

```python
# TinyPerson.generate_agent_system_prompt() 내부의 일부 (개념적)

# ... 기본 페르소나 정보 ...

# 추가 액션 정의 및 제약 조건 준비
actions_definitions_prompt = ""
actions_constraints_prompt = ""
for faculty in self._mental_faculties: # 에이전트가 가진 모든 정신 능력에 대해
    actions_definitions_prompt += f"{faculty.actions_definitions_prompt()}\n"
    actions_constraints_prompt += f"{faculty.actions_constraints_prompt()}\n"

# 이 정보들이 전체 시스템 프롬프트에 포함되어 LLM에게 전달됨
# template_variables['actions_definitions_prompt'] = actions_definitions_prompt
# template_variables['actions_constraints_prompt'] = actions_constraints_prompt
```
이렇게 함으로써, LLM은 이제 `RECALL "키워드"`나 `CONSULT "파일명"`과 같은 새로운 형식의 액션을 이해하고, 상황에 맞게 생성할 수 있게 됩니다. 즉, 정신 능력은 타이니퍼슨의 행동 범위를 확장시켜 주는 것입니다.

## 정신 능력의 내부 동작 살펴보기

정신 능력은 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md)의 행동 결정 과정과 긴밀하게 연동됩니다.

### 비-코드 흐름도

1.  **자극 수신**: 타이니퍼슨이 외부로부터 자극(예: 사용자 질문)을 받습니다.
2.  **LLM 호출 (행동 결정)**: 타이니퍼슨은 현재 상태, 페르소나, 기억, 그리고 정신 능력이 제공하는 액션 정의/제약 조건 등을 바탕으로 LLM에게 다음 행동을 요청합니다.
3.  **정신 능력 관련 액션 생성**: LLM이 `RECALL "회의록"`이나 `CONSULT "문서A"`와 같이 정신 능력과 관련된 특별한 액션을 생성할 수 있습니다.
4.  **액션 처리 루프**: 타이니퍼슨의 `act()` 메서드 내부에서, 생성된 액션은 에이전트가 가진 각 정신 능력의 `process_action()` 메서드에 전달됩니다.
5.  **해당 능력의 처리**:
    *   만약 액션이 `RECALL`이고 `RecallFaculty`가 있다면, `RecallFaculty.process_action()`이 실행됩니다. 이 메서드는 에이전트의 [기억 (Memory)](07_기억__memory__.md)에서 정보를 검색하고, 그 결과를 바탕으로 새로운 `THINK` 액션을 생성하여 에이전트의 다음 생각에 영향을 줍니다.
    *   만약 액션이 `CONSULT`이고 `FilesAndWebGroundingFaculty`가 있다면, 해당 파일/웹 내용을 읽어와 유사하게 `THINK` 액션으로 변환합니다.
6.  **후속 행동**: 정신 능력에 의해 생성된 새로운 `THINK` 액션(예: 회상된 내용, 읽어온 문서 내용)은 다시 LLM에게 전달될 프롬프트의 일부가 되어, 최종적인 사용자 응답이나 다음 행동에 영향을 미칩니다.

### 순서도 (Sequence Diagram)

다음은 사용자가 질문했을 때 `RecallFaculty`가 작동하는 과정을 보여주는 순서도입니다.

```mermaid
sequenceDiagram
    participant User as 사용자
    participant Jihye as 지혜 (타이니퍼슨)
    participant LLM as 대규모 언어 모델
    participant RecallF as 회상 능력 (RecallFaculty)
    participant Memory as 기억 장치 (SemanticMemory)

    User->>Jihye: "어제 배운 내용 기억나?" (listen_and_act)
    Jihye->>LLM: 행동 요청 (페르소나, 기억, 사용 가능 액션[RECALL 등] 기반)
    LLM-->>Jihye: 행동 제안: `{"type": "RECALL", "content": "어제 배운 내용"}`
    Jihye->>Jihye: `act()` 내부에서 정신 능력 처리 루프 실행
    Jihye->>RecallF: `process_action({"type": "RECALL", "content": "어제 배운 내용"})` 호출
    RecallF->>Memory: `retrieve_relevant_memories("어제 배운 내용")` 호출
    Memory-->>RecallF: 관련 기억 반환 ("프랑스 혁명...")
    RecallF->>Jihye: 내부적으로 `jihye.think("기억 내용: 프랑스 혁명...")` 유도
    Note over Jihye: 새로운 생각(기억 내용)이 현재 메시지에 추가됨
    Jihye->>LLM: 다음 행동 요청 (회상된 내용 포함)
    LLM-->>Jihye: 행동 제안: `{"type": "TALK", "content": "네, 어제 프랑스 혁명에 대해 배웠어요."}`
    Jihye-->>User: "네, 어제 프랑스 혁명에 대해 배웠어요." (화면 출력)
end
```

### 코드 내부 (`tinytroupe/agent/mental_faculty.py` 및 `tinytroupe/agent/tiny_person.py`)

*   **`TinyMentalFaculty` (기반 클래스)**:
    모든 정신 능력의 부모 클래스입니다. 핵심 메서드들을 정의합니다.

    ```python
    # tinytroupe/agent/mental_faculty.py 일부
    class TinyMentalFaculty(JsonSerializableRegistry):
        def __init__(self, name: str, requires_faculties: list=None) -> None:
            self.name = name # 능력의 이름
            # ...
        
        def process_action(self, agent, action: dict) -> bool:
            # 자식 클래스에서 이 메서드를 구현하여 특정 액션을 처리해야 함
            raise NotImplementedError("Subclasses must implement this method.")
        
        def actions_definitions_prompt(self) -> str:
            # 자식 클래스에서 이 능력이 제공하는 액션 설명을 반환해야 함
            raise NotImplementedError("Subclasses must implement this method.")

        def actions_constraints_prompt(self) -> str:
            # 자식 클래스에서 액션 사용 규칙/팁을 반환해야 함
            raise NotImplementedError("Subclasses must implement this method.")
    ```

*   **`RecallFaculty` (회상 능력)**:
    `RECALL` 액션을 처리하고, 관련 프롬프트를 제공합니다.

    ```python
    # tinytroupe/agent/mental_faculty.py 일부
    class RecallFaculty(TinyMentalFaculty):
        def __init__(self):
            super().__init__("Memory Recall") # 능력 이름 설정
            
        def process_action(self, agent, action: dict) -> bool:
            if action['type'] == "RECALL" and action['content'] is not None:
                content = action['content'] # LLM이 제공한 검색어
                # 에이전트의 의미 기억에서 관련 정보 검색
                semantic_memories = agent.retrieve_relevant_memories(relevance_target=content)
                if len(semantic_memories) > 0:
                    # 검색된 내용을 바탕으로 THINK 액션 유도
                    agent.think("다음 정보를 기억해냈습니다: \n" + \
                                "\n".join([f"  - {item}" for item in semantic_memories]))
                else:
                    agent.think(f"'{content}'에 대해 아무것도 기억나지 않습니다.")
                return True # RECALL 액션 처리 완료
            return False # 이 능력과 관련 없는 액션임

        def actions_definitions_prompt(self) -> str:
            return textwrap.dedent("""
              - RECALL: 기억에서 정보를 회상할 수 있습니다. 원하는 기억을 찾기 위해 "mental query"를 지정해야 합니다.
            """)
        
        def actions_constraints_prompt(self) -> str:
            return textwrap.dedent("""
            - 무언가를 모르거나 정보에 접근할 수 없다고 결론 내리기 전에, 반드시 기억에서 RECALL을 시도해야 합니다.
            - "mental query"는 질문이 아니라 찾고 있는 내용을 설명하는 키워드 기반 검색어여야 합니다. (예: "코로나19 증상")
            """)
    ```
    `process_action` 메서드가 `agent.retrieve_relevant_memories()`를 호출하여 실제 기억 검색을 수행하고, `agent.think()`를 통해 검색 결과를 에이전트의 다음 생각으로 전달하는 것을 볼 수 있습니다.

*   **`FilesAndWebGroundingFaculty` (파일 및 웹 참조 능력)**:
    `CONSULT`, `LIST_DOCUMENTS` 액션을 처리합니다.

    ```python
    # tinytroupe/agent/mental_faculty.py 일부
    class FilesAndWebGroundingFaculty(TinyMentalFaculty):
        def __init__(self, folders_paths: list=None, web_urls: list=None):
            super().__init__("Local Files and Web Grounding")
            # 파일 및 웹 페이지 접근을 위한 커넥터 초기화
            self.local_files_grounding_connector = LocalFilesGroundingConnector(folders_paths)
            # ... web_grounding_connector ...

        def process_action(self, agent, action: dict) -> bool:
            if action['type'] == "CONSULT" and action['content'] is not None:
                target_name = action['content'] # LLM이 제공한 파일/웹페이지 이름
                # 커넥터를 사용해 실제 파일/웹 내용 가져오기
                results = self.local_files_grounding_connector.retrieve_by_name(target_name)
                # ... 웹 결과도 유사하게 처리 ...
                if results:
                    agent.think(f"다음 문서를 읽었습니다: \n{results}")
                else:
                    agent.think(f"'{target_name}' 이름의 문서를 찾을 수 없습니다.")
                return True
            # ... LIST_DOCUMENTS 액션 처리 로직 ...
            return False

        def actions_definitions_prompt(self) -> str:
            return textwrap.dedent("""
            - LIST_DOCUMENTS: 접근 가능한 문서 목록을 보여줍니다.
            - CONSULT: 특정 문서의 내용을 가져와 참조합니다. 문서 이름을 지정해야 합니다.
            """)
        # ... actions_constraints_prompt() ...
    ```

*   **`TinyPerson`의 액션 처리 부분**:
    `act()` 메서드 내에서 각 정신 능력의 `process_action()`을 호출합니다.

    ```python
    # tinytroupe/agent/tiny_person.py 의 act() 메서드 일부
    # ... (LLM으로부터 action_detail, cognitive_state_update 등을 받음) ...
    # action = content['action'] # LLM이 생성한 액션 (예: {"type": "RECALL", "content": "..."})

    # ... (생성된 액션을 기억에 저장하고, 인지 상태 업데이트) ...
            
    # 일부 액션은 즉각적인 자극이나 다른 부작용을 유발합니다.
    # 정신 능력을 통해 여기서 처리해야 합니다.
    for faculty in self._mental_faculties: # 에이전트가 가진 모든 정신 능력에 대해
        faculty.process_action(self, action) # 현재 액션을 처리하도록 시도
    
    # ... (루프 계속 또는 종료) ...
    ```
    이 루프를 통해 LLM이 생성한 액션이 해당 정신 능력에 의해 특별하게 처리될 기회를 갖게 됩니다.

## 정리 및 다음 단계

이번 장에서는 타이니퍼슨에게 고차원적인 인지 기능을 부여하는 '정신 능력 (Mental Faculties)'에 대해 배웠습니다. `TinyMentalFaculty`를 기반으로 하는 `RecallFaculty`(회상 능력), `FilesAndWebGroundingFaculty`(파일/웹 참조 능력), `TinyToolUse`(도구 사용 능력) 등이 어떻게 타이니퍼슨을 더 똑똑하게 만드는지 살펴보았습니다. 이러한 능력들을 타이니퍼슨에게 추가하고, 각 능력이 제공하는 특별한 액션(예: `RECALL`, `CONSULT`)을 통해 타이니퍼슨이 어떻게 더 복잡한 작업을 수행할 수 있는지 예시와 함께 알아보았습니다. 또한, 정신 능력이 LLM 프롬프트에 어떻게 영향을 미치고 내부적으로 어떻게 작동하는지에 대해서도 간략하게 탐구했습니다.

**핵심 요약:**
*   정신 능력은 타이니퍼슨에게 기억 회상, 정보 검색, 도구 사용과 같은 전문 기술을 제공합니다.
*   `RecallFaculty`는 `RECALL` 액션을 통해 과거 기억을 떠올리게 합니다.
*   `FilesAndWebGroundingFaculty`는 `LIST_DOCUMENTS`와 `CONSULT` 액션을 통해 파일이나 웹 페이지 내용을 참조하게 합니다.
*   `TinyToolUse`는 특정 도구를 사용하는 액션을 처리합니다. (자세한 내용은 [제8장: 도구 (Tools)](08_도구__tools__.md)에서)
*   각 정신 능력은 LLM에게 새로운 액션의 정의와 사용 규칙을 알려주어, 타이니퍼슨의 행동 범위를 넓힙니다.
*   타이니퍼슨의 `act()` 메서드는 LLM이 생성한 액션을 각 정신 능력의 `process_action()` 메서드에 전달하여 처리합니다.

정신 능력, 특히 회상 능력은 타이니퍼슨의 '기억'이라는 또 다른 중요한 요소와 깊은 관련이 있습니다. 타이니퍼슨은 과연 무엇을, 어떻게 기억하고, 그 기억을 어떻게 활용할까요?

다음 [제7장: 기억 (Memory)](07_기억__memory__.md)에서는 타이니퍼슨의 기억 시스템에 대해 더 자세히 파헤쳐 보겠습니다. 타이니퍼슨의 마음 속 여행을 계속해 주세요!

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)