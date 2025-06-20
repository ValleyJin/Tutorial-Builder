# Chapter 7: 기억 (Memory)


이전 [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)에서는 타이니퍼슨에게 회상, 파일 참조, 도구 사용과 같은 고차원적인 인지 능력을 부여하는 '정신 능력'에 대해 배웠습니다. 특히 회상 능력은 타이니퍼슨의 '기억'과 아주 밀접하게 연결되어 있었죠. 이번 장에서는 타이니퍼슨이 정보를 마음속에 간직하고 필요할 때 다시 꺼내 쓰는 방법, 즉 '기억(Memory)' 시스템에 대해 자세히 알아보겠습니다.

## 타이니퍼슨에게 기억은 왜 필요할까요?

여러분이 '하나'라는 이름의 타이니퍼슨을 만들었다고 상상해 보세요. 하나가 어제 친구 '두리'와 나눴던 대화 내용을 전혀 기억하지 못한다면, 오늘 두리를 만났을 때 어색한 상황이 벌어질 수 있습니다. "어제 빌려 간 내 책 언제 돌려줄 거야?"라는 두리의 질문에 하나가 "내가 네 책을 빌렸었나?"라고 대답한다면 정말 이상하겠죠?

**핵심 사용 사례:** 하나는 며칠 전 두리와 "주말에 함께 공원에서 자전거를 타자"고 약속했습니다. 주말이 되어 두리가 "하나야, 오늘 공원에서 만나기로 한 거 기억하지?"라고 물었을 때, 하나는 이 약속을 정확히 기억해내고 "응, 물론이지! 몇 시에 만날까?"라고 자연스럽게 대답해야 합니다. 또한, 하나가 학교에서 '지구 온난화'에 대해 배웠다면, 나중에 관련된 질문을 받았을 때 그 내용을 떠올려 설명할 수 있어야 합니다.

이처럼 타이니퍼슨이 과거의 경험이나 학습한 내용을 바탕으로 현재 상황을 판단하고 미래 행동을 결정하려면, 마치 사람처럼 정보를 저장하고 회상하는 '기억' 능력이 필수적입니다. `TinyTroupe`에서 기억은 타이니퍼슨이 더 똑똑하고 일관성 있는 행동을 하도록 돕는 중요한 역할을 합니다.

## 기억의 종류: 일화 기억과 의미 기억

`TinyTroupe`의 타이니퍼슨은 크게 두 가지 종류의 기억을 가집니다. 이 둘은 `TinyMemory`라는 기본적인 기억 설계도를 바탕으로 만들어졌습니다.

1.  **일화 기억 (`EpisodicMemory`)**:
    *   **개념**: 특정 사건이나 경험을 시간 순서대로 기억하는 방식입니다. 마치 우리가 개인적인 일기나 짧은 순간의 스냅샷처럼 기억하는 것과 비슷해요. "어제 오후 3시에 두리와 카페에서 커피를 마셨다" 또는 "방금 사용자가 나에게 '안녕'이라고 인사했다" 와 같은 구체적인 에피소드들이 여기에 저장됩니다.
    *   **특징**: 시간 순서가 중요하며, 주로 최근에 일어난 일들이나 대화의 흐름을 파악하는 데 사용됩니다. 사람의 '단기 기억'과 비슷한 역할을 한다고 볼 수 있습니다.

2.  **의미 기억 (`SemanticMemory`)**:
    *   **개념**: 일반적인 사실, 개념, 세상에 대한 지식 등을 저장하는 방식입니다. "대한민국의 수도는 서울이다" 또는 "나는 '하나'이고, 학생이다" 와 같이 특정 시간이나 사건과 직접적으로 연결되지 않은 일반적인 정보들이 여기에 저장됩니다.
    *   **특징**: 시간 순서보다는 정보의 '의미'가 중요하며, 에이전트가 세상을 이해하고, 학습한 내용을 바탕으로 추론하는 데 사용됩니다. 사람의 '장기 기억'이나 '지식 창고'와 유사하다고 생각할 수 있습니다.

이 두 가지 기억은 서로 협력하여 타이니퍼슨이 과거 경험(일화 기억)으로부터 일반적인 지식(의미 기억)을 배우고, 이를 바탕으로 현재 상황을 이해하며 미래를 계획하도록 돕습니다.

## 타이니퍼슨은 어떻게 기억할까요?

타이니퍼슨은 특별한 설정 없이도 기본적으로 일화 기억과 의미 기억 능력을 가지고 있습니다. 타이니퍼슨이 경험하는 모든 일(외부 자극 수신, 자신의 행동 등)은 자동으로 이 기억들에 기록됩니다.

### 1. 기억 저장하기

타이니퍼슨이 어떤 말을 듣거나(`listen`), 무언가를 보거나(`see`), 스스로 어떤 행동을 하면(`act`), 이러한 정보들은 즉시 기억 속에 저장됩니다.

*   **일화 기억 (`EpisodicMemory`)**: 타이니퍼슨이 경험한 사건들은 발생한 시간 순서대로 `EpisodicMemory`에 차곡차곡 쌓입니다. 예를 들어, 사용자와 대화하는 경우, 사용자의 말과 타이니퍼슨의 답변이 순서대로 기록됩니다.
    ```python
    from tinytroupe.agent import TinyPerson
    import tinytroupe.control as control
    
    control.begin() # 시뮬레이션 시작
    
    hana = TinyPerson(name="하나")
    
    # 하나가 사용자의 말을 듣습니다.
    hana.listen("안녕, 하나야!")
    # 이 "안녕, 하나야!" 라는 자극이 하나의 일화 기억에 저장됩니다.
    
    # 하나가 응답합니다.
    hana.act() # 예시: 하나가 "안녕하세요!" 라고 말하는 행동
    # 이 행동 역시 하나의 일화 기억에 저장됩니다.
    
    control.end() # 시뮬레이션 종료
    ```
    위 코드에서 `hana.listen(...)`과 `hana.act()`가 실행될 때마다 해당 내용이 하나의 일화 기억에 자동으로 추가됩니다.

*   **의미 기억 (`SemanticMemory`)**: 일화 기억에 저장된 내용 중 일부는 일반화되어 의미 기억에도 저장될 수 있습니다. 예를 들어, 하나가 "나는 학생이다"라는 정보를 페르소나에 가지고 있다면, 이 정보는 의미 기억에 저장되어 언제든지 참조할 수 있습니다. 또한, [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)에서 배운 `RecallFaculty`를 통해 과거의 중요한 사건이나 학습 내용이 요약되어 의미 기억에 추가될 수도 있습니다.
    ```python
    # 의미 기억은 주로 내부적으로, 또는 RecallFaculty 등을 통해 관리됩니다.
    # 사용자가 직접 의미 기억에 세세하게 저장하는 경우는 드뭅니다.
    # 예시: 하나가 페르소나에 "직업: 학생"을 정의하면,
    # hana.define("occupation", "학생")
    # 이 정보는 의미 기억에서 검색 가능한 형태로 변환될 수 있습니다.
    ```

### 2. 기억 꺼내 보기 (회상)

타이니퍼슨은 저장된 기억을 다시 꺼내 볼 수 있습니다.

*   **일화 기억에서 꺼내 보기 (`retrieve_recent_memories`)**:
    타이니퍼슨은 최근에 있었던 일들을 쉽게 떠올릴 수 있습니다. `retrieve_recent_memories()` 메서드를 사용하면 최근 대화 기록 등을 가져올 수 있습니다. 이 정보는 LLM에게 현재 대화의 맥락을 제공하는 데 매우 중요합니다.

    ```python
    # (이전 코드에 이어서, 시뮬레이션은 시작된 상태)
    # control.begin()
    # hana = TinyPerson(name="하나")
    # hana.listen("만나서 반가워.")
    # hana.act() # 하나가 "저도 반가워요." 라고 응답했다고 가정
    
    # 하나의 최근 기억(대화 내용) 가져오기
    recent_memories = hana.retrieve_recent_memories()
    
    print("\n하나의 최근 기억:")
    for memory_item in recent_memories:
        # 실제 메모리 아이템은 딕셔너리 형태입니다. 여기서는 간단히 내용만 출력합니다.
        if isinstance(memory_item.get('content'), dict) and 'stimuli' in memory_item['content']:
            print(f"- 역할: {memory_item['role']}, 내용: {memory_item['content']['stimuli'][0]['content']}")
        elif isinstance(memory_item.get('content'), dict) and 'action' in memory_item['content']:
            print(f"- 역할: {memory_item['role']}, 내용: {memory_item['content']['action']['content']}")
    
    # control.end()
    ```
    출력 예시 (실제 내용은 LLM 응답에 따라 다름):
    ```
    하나의 최근 기억:
    - 역할: user, 내용: 만나서 반가워.
    - 역할: assistant, 내용: 저도 반가워요.
    ```
    `retrieve_recent_memories()`는 기본적으로 일정한 개수의 앞부분 기억과 최근 기억들을 조합해서 보여줍니다. 만약 기억이 너무 많으면 중간 부분은 생략되었다는 표시(`MEMORY_BLOCK_OMISSION_INFO`)와 함께 보여주어, LLM에게 전달되는 정보의 양을 조절합니다.

*   **의미 기억에서 꺼내 보기 (`retrieve_relevant_memories`와 `RecallFaculty`)**:
    일반적인 지식이나 과거의 중요한 사건에 대한 정보는 의미 기억에서 검색합니다. 이것은 주로 [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)에서 배운 `RecallFaculty`가 `RECALL` 액션을 처리할 때 내부적으로 사용됩니다. `RecallFaculty`는 `agent.retrieve_relevant_memories(relevance_target="검색어")` 와 같은 함수를 호출하여 의미 기억에서 "검색어"와 관련된 정보를 찾아옵니다.

    ```python
    # (하나에게 RecallFaculty가 추가되어 있다고 가정)
    # control.begin()
    # hana = TinyPerson(name="하나")
    # recall_faculty = RecallFaculty() # RecallFaculty 임포트 필요
    # hana.add_mental_faculty(recall_faculty)
    
    # 하나가 "지구 온난화의 원인은 무엇인가요?" 라는 질문을 들었다고 가정
    # hana.listen("지구 온난화의 원인은 무엇인가요?")
    # hana.act() 
    #   -> 내부적으로 LLM이 RECALL("지구 온난화 원인") 액션 생성 가능
    #   -> RecallFaculty가 hana.retrieve_relevant_memories("지구 온난화 원인") 호출
    #   -> 의미 기억에서 관련 정보 검색 후 답변 생성에 활용
    
    # control.end()
    ```
    이처럼 의미 기억은 타이니퍼슨이 학습하고 경험한 내용을 바탕으로 지적인 답변을 생성하는 데 중요한 역할을 합니다.

## 기억 시스템의 내부 동작 살펴보기

타이니퍼슨의 기억 시스템이 내부적으로 어떻게 작동하는지 간략하게 알아보겠습니다.

### `TinyMemory` (기억의 기본 설계도)

모든 기억 유형(일화 기억, 의미 기억 등)은 `TinyMemory`라는 기본 클래스(설계도)를 따릅니다. 이 클래스에는 기억을 다루기 위한 기본적인 기능들이 정의되어 있습니다.

*   `_preprocess_value_for_storage(value)`: 값을 기억에 저장하기 전에 적절한 형태로 가공합니다. 예를 들어, 복잡한 데이터를 단순화하거나 특정 형식으로 변환할 수 있습니다.
*   `_store(value)`: 실제로 가공된 값을 기억 장소에 저장합니다. (자식 클래스에서 구체적으로 구현)
*   `store(value)`: 외부에서 값을 저장할 때 사용하는 메서드로, 내부적으로 `_preprocess_value_for_storage`와 `_store`를 호출합니다.
*   `retrieve(...)`: 저장된 기억을 꺼내 오는 여러 가지 방법을 제공합니다. (자식 클래스에서 구체적으로 구현)

### `EpisodicMemory` (일화 기억 저장소)

일화 기억은 비교적 단순하게 작동합니다.

*   **저장 (`_store`)**: `EpisodicMemory`는 `self.memory`라는 리스트(목록)에 사건들을 시간 순서대로 그냥 추가합니다.
    ```python
    # tinytroupe/agent/memory.py 의 EpisodicMemory 일부
    class EpisodicMemory(TinyMemory):
        def __init__(self, fixed_prefix_length: int = 100, lookback_length: int = 100):
            # ... 초기화 ...
            self.memory = [] # 기억을 저장할 리스트

        def _store(self, value: Any) -> None:
            self.memory.append(value) # 리스트 끝에 추가
    ```
*   **회상 (`retrieve_recent`)**: 최근 기억을 가져올 때는, 가장 오래된 기억 중 일부(`fixed_prefix_length` 만큼)와 가장 최근 기억 일부(`lookback_length` 만큼)를 조합해서 반환합니다. 만약 전체 기억이 너무 길면, 중간 부분은 `MEMORY_BLOCK_OMISSION_INFO`라는 특별한 메시지로 대체하여 보여줍니다. 이는 LLM에게 너무 많은 정보를 한꺼번에 주지 않기 위함입니다.
    ```python
    # tinytroupe/agent/memory.py 의 EpisodicMemory 일부
    def retrieve_recent(self, include_omission_info:bool=True) -> list:
        omisssion_info = [EpisodicMemory.MEMORY_BLOCK_OMISSION_INFO] if include_omission_info else []
        fixed_prefix = self.memory[: self.fixed_prefix_length] + omisssion_info
        # ... (나머지 최근 기억 계산 로직) ...
        return fixed_prefix + self.memory[-remaining_lookback:] # 조합하여 반환
    ```

### `SemanticMemory` (의미 기억 저장소)

의미 기억은 좀 더 복잡한 방식으로 정보를 저장하고 검색합니다. 내부적으로 LlamaIndex 라이브러리의 `Document` 객체와 `BaseSemanticGroundingConnector` (정보 검색 시스템)를 사용합니다.

*   **저장 전 가공 (`_preprocess_value_for_storage`)**: 일화 기억에서 넘어온 사건(행동 또는 자극) 정보를 의미 기억에 저장하기 좋은 텍스트 형태로 변환합니다. 예를 들어, 타이니퍼슨의 행동은 "# Fact (사실)\n언제 이런 행동을 했음: 내용" 과 같은 형태로, 외부 자극은 "# Stimulus (자극)\n언제 이런 자극을 받음: 내용" 과 같은 형태로 바뀝니다.
    ```python
    # tinytroupe/agent/memory.py 의 SemanticMemory 일부
    def _preprocess_value_for_storage(self, value: dict) -> Any:
        engram = None # 기억의 흔적
        if value['type'] == 'action':
            engram = f"# Fact\nI have performed the following action at date and time {value['simulation_timestamp']}:\n\n {value['content']}"
        elif value['type'] == 'stimulus':
            engram = f"# Stimulus\nI have received the following stimulus at date and time {value['simulation_timestamp']}:\n\n {value['content']}"
        return engram
    ```
*   **저장 (`_store`)**: 가공된 텍스트(`engram`)는 LlamaIndex의 `Document` 객체로 만들어져, `self.semantic_grounding_connector`를 통해 검색 가능한 형태로 저장됩니다. 이 커넥터는 마치 의미 기억 속의 작은 도서관 사서와 같아서, 나중에 관련 정보를 쉽게 찾을 수 있도록 도와줍니다.
    ```python
    # tinytroupe/agent/memory.py 의 SemanticMemory 일부
    def _store(self, value: Any) -> None:
        # 가공된 텍스트(value)로 Document 만들기
        engram_doc = self._build_document_from(self._preprocess_value_for_storage(value))
        # 커넥터를 통해 Document 저장
        self.semantic_grounding_connector.add_document(engram_doc)
    ```
*   **관련 기억 검색 (`retrieve_relevant`)**: 사용자가 특정 "검색어"로 관련 기억을 찾고 싶을 때, `semantic_grounding_connector`가 이 검색어와 가장 관련성이 높은 `Document`들을 찾아 그 내용을 반환합니다.
    ```python
    # tinytroupe/agent/memory.py 의 SemanticMemory 일부
    def retrieve_relevant(self, relevance_target:str, top_k=20) -> list:
        # 커넥터를 사용해 관련성 높은 문서 검색 (결과는 텍스트 리스트)
        return self.semantic_grounding_connector.retrieve_relevant(relevance_target, top_k)
    ```

### 기억 저장 과정 흐름도

타이니퍼슨이 외부 자극을 받거나 행동을 할 때, 정보가 두 종류의 기억에 어떻게 저장되는지 간단한 그림으로 살펴봅시다.

```mermaid
sequenceDiagram
    participant User as 사용자
    participant Agent as 타이니퍼슨 (하나)
    participant EpisodicMem as 일화 기억 (하나의 것)
    participant SemanticMem as 의미 기억 (하나의 것)

    User->>Agent: "오늘 점심 뭐 먹었어?" (자극)
    Note over Agent: 자극을 받고 기억 저장 시작
    Agent->>EpisodicMem: store({"type":"stimulus", "content":"오늘 점심 뭐 먹었어?", ...})
    EpisodicMem->>EpisodicMem: 자극 내용을 리스트에 추가 (시간 순)
    Agent->>SemanticMem: store({"type":"stimulus", "content":"오늘 점심 뭐 먹었어?", ...})
    Note over SemanticMem: 자극 내용을 "# Stimulus..." 텍스트로 가공
    SemanticMem->>SemanticMem: 가공된 텍스트를 Document로 만들어 검색 가능하게 저장
    Note over Agent: 이후 회상 시 각 기억 사용 가능
end
```

`TinyPerson` 클래스의 `store_in_memory` 메서드는 새로운 정보(행동이나 자극)가 들어올 때마다 기본적으로 `EpisodicMemory`에 저장합니다. `SemanticMemory`에도 정보가 전달되어 `_preprocess_value_for_storage`를 통해 처리된 후 저장될 수 있습니다. (현재 `TinyPerson` 코드에서는 `store_in_memory`가 주로 `EpisodicMemory`에만 저장하고, `SemanticMemory`는 `RecallFaculty` 등을 통해 간접적으로 채워지거나, 페르소나 정보를 기반으로 초기화될 수 있습니다. 하지만 개념적으로는 두 기억 모두 사건으로부터 정보를 얻습니다.)

```python
# tinytroupe/agent/tiny_person.py 의 TinyPerson 클래스 일부

# ... (다른 메서드들) ...

    ###########################################################
    # Memory management (기억 관리)
    ###########################################################
    def store_in_memory(self, value: Any) -> list:
        # TODO: 일화적 정보를 의미 기억으로 추상화하는 더 스마트한 방법 찾기
        # self.semantic_memory.store(value) # 현재는 주석 처리, 필요시 활성화 가능

        self.episodic_memory.store(value) # 주로 일화 기억에 저장

    def retrieve_recent_memories(self, max_content_length:int=None) -> list:
        # 일화 기억에서 최근 내용 가져오기
        episodes = self.episodic_memory.retrieve_recent()
        # ... (내용 길이 조절 로직) ...
        return episodes

    def retrieve_relevant_memories(self, relevance_target:str, top_k=20) -> list:
        # 의미 기억에서 관련 내용 가져오기
        relevant = self.semantic_memory.retrieve_relevant(relevance_target, top_k=top_k)
        return relevant
```
이처럼 타이니퍼슨은 일화 기억과 의미 기억을 통해 세상을 경험하고, 학습하며, 그 지식을 바탕으로 상호작용합니다.

## 정리 및 다음 단계

이번 장에서는 타이니퍼슨의 '기억 (Memory)' 시스템에 대해 알아보았습니다. 타이니퍼슨은 특정 사건을 시간 순서대로 기억하는 '일화 기억 (`EpisodicMemory`)'과 일반적인 사실이나 지식을 저장하는 '의미 기억 (`SemanticMemory`)'을 가지고 있으며, 이 두 기억은 `TinyMemory`라는 공통 기반 위에서 작동합니다. 타이니퍼슨은 경험을 통해 자동으로 기억을 저장하고, 필요에 따라 이 기억들을 꺼내 현재 상황을 판단하고 미래 행동을 결정하는 데 사용합니다. 특히 의미 기억은 [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)의 회상 능력과 밀접하게 연관되어 타이니퍼슨의 지적인 행동을 가능하게 합니다.

**핵심 요약:**
*   타이니퍼슨은 '일화 기억'과 '의미 기억' 두 종류의 기억을 가집니다.
*   **일화 기억 (`EpisodicMemory`)**: 시간 순서대로 사건을 기록하며, 최근 대화 맥락 파악 등에 사용됩니다. (단기 기억과 유사)
*   **의미 기억 (`SemanticMemory`)**: 일반적 지식과 사실을 저장하며, 학습 및 추론에 사용됩니다. (장기 기억과 유사)
*   타이니퍼슨은 경험(자극, 행동)을 자동으로 기억에 저장합니다.
*   `retrieve_recent_memories()`로 최근 일화 기억을, `retrieve_relevant_memories()` (주로 `RecallFaculty`를 통해)로 의미 기억 속 관련 정보를 가져올 수 있습니다.

이제 타이니퍼슨은 페르소나, 정신 능력, 그리고 기억까지 갖추어 점점 더 사람과 비슷하게 생각하고 행동할 수 있게 되었습니다. 하지만 때로는 타이니퍼슨이 직접 수행하기 어려운 계산을 하거나, 문서를 작성하는 등 특별한 작업이 필요할 수 있습니다. 이런 경우, 타이니퍼슨은 외부 '도구'의 도움을 받을 수 있습니다.

다음 [제8장: 도구 (Tools)](08_도구__tools__.md)에서는 타이니퍼슨이 어떻게 다양한 도구들을 활용하여 자신의 능력을 확장하고 더 복잡한 작업을 수행하는지 알아보겠습니다. 기대해 주세요!

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)