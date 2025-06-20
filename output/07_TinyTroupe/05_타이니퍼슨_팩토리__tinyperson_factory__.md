# Chapter 5: 타이니퍼슨 팩토리 (TinyPerson Factory)


이전 [제4장: OpenAI 유틸리티 (OpenAI Utilities)](04_openai_유틸리티__openai_utilities__.md)에서는 타이니퍼슨에게 생각하고 말하는 능력을 부여하는 핵심 엔진, 즉 LLM과의 소통 방법을 배웠습니다. 이제 우리는 타이니퍼슨이 어떻게 지능적으로 행동하는지 이해했지만, 만약 시뮬레이션에 각기 다른 개성을 가진 수많은 타이니퍼슨이 필요하다면 어떨까요? 예를 들어, 새로운 게임을 개발하고 다양한 유형의 플레이어 반응을 테스트하고 싶다고 상상해 보세요. "호기심 많은 초등학생", "과학을 좋아하는 꼼꼼한 중학생", "예술에 관심 있는 창의적인 고등학생" 등 다양한 페르소나를 가진 타이니퍼슨들을 일일이 수동으로 만드는 것은 꽤 번거로운 작업일 수 있습니다.

바로 이런 문제를 해결하기 위해 '타이니퍼슨 팩토리(TinyPersonFactory)'가 등장합니다!

## 타이니퍼슨 팩토리는 무엇이고 왜 필요할까요?

타이니퍼슨 팩토리는 마치 주문 제작 로봇 공장과 같습니다. 여러분이 원하는 캐릭터의 대략적인 특징(예: "브라질 출신 의사, 반려동물과 자연을 사랑하며 헤비메탈 음악을 즐겨 들음")과 약간의 주변 상황(컨텍스트)을 알려주면, 이 팩토리는 LLM의 창의력을 활용하여 해당 설명에 맞는 상세한 프로필을 가진 새로운 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md) 객체를 '뚝딱' 만들어냅니다.

**핵심 사용 사례:** 여러분이 다양한 연령과 관심사를 가진 학생들을 대상으로 하는 새로운 교육용 소프트웨어를 개발했다고 가정해 봅시다. 각기 다른 학생 페르소나를 가진 타이니퍼슨 수십 명을 만들어 소프트웨어와 상호작용하게 함으로써, 어떤 유형의 학생이 어떤 부분에서 흥미를 느끼고 어려움을 겪는지 빠르게 파악하고 싶습니다. 이때 타이니퍼슨 팩토리를 사용하면, "코딩을 좋아하는 10대 소녀", "역사에 관심 많은 대학생", "새로운 기술 배우기를 즐기는 은퇴한 교사" 등 다양한 페르소나를 설명만으로 손쉽게 생성하여 시뮬레이션에 바로 투입할 수 있습니다. 이를 통해 프로토타이핑 과정과 다양한 사용자 페르소나를 탐색하는 시간을 크게 단축할 수 있습니다.

타이니퍼슨 팩토리는 다음과 같은 멋진 일을 해냅니다:
*   **간단한 설명으로 상세한 페르소나 생성**: 몇 마디 특징만으로도 LLM이 살을 붙여 풍부한 배경 이야기를 가진 캐릭터를 만듭니다.
*   **다양한 에이전트 손쉽게 확보**: 여러 종류의 에이전트를 빠르게 만들어 실험에 활용할 수 있습니다.
*   **페르소나 탐색 가속화**: 다양한 아이디어를 빠르게 캐릭터로 구현해 볼 수 있습니다.

이 장을 통해 여러분은 타이니퍼슨 팩토리를 사용하여 원하는 페르소나의 타이니퍼슨을 자동으로 생성하는 방법을 배우게 될 것입니다.

## 타이니퍼슨 팩토리 사용하기: 나만의 캐릭터 주문하기

타이니퍼슨 팩토리를 사용하는 것은 매우 간단합니다. 먼저 `TinyPersonFactory` 객체를 만들어야 합니다. 이때 이 팩토리가 캐릭터를 생성할 때 참고할 전반적인 '상황' 또는 '배경(context)'을 알려줍니다.

### 1. 팩토리 만들기

예를 들어, "상파울루의 한 병원"이라는 배경에서 일어날 법한 캐릭터들을 만들고 싶다고 해봅시다.

```python
from tinytroupe.factory import TinyPersonFactory

# "상파울루의 한 병원"이라는 배경을 가진 팩토리 생성
hospital_factory = TinyPersonFactory(context_text="상파울루의 한 병원입니다.")

print(f"'{hospital_factory.context_text}' 배경의 팩토리가 준비되었습니다!")
```
이제 `hospital_factory`는 "상파울루의 한 병원"이라는 컨텍스트를 기억하고, 이와 관련된 캐릭터를 생성할 준비가 되었습니다.

### 2. 특정 페르소나 생성하기: `generate_person()`

이제 이 팩토리에 구체적인 캐릭터 특징을 주문해 봅시다. `generate_person()` 메서드를 사용하고, 원하는 캐릭터의 특징을 문자열로 전달합니다.

```python
# (이전 코드에 이어서)
# 시뮬레이션 제어를 위해 import (제1장에서 배운 내용)
import tinytroupe.control as control

# LLM 호출 결과 등을 캐싱할 수 있도록 시뮬레이션 시작
control.begin()

# 원하는 캐릭터 특징을 설명합니다.
description = "브라질 사람이고 의사입니다. 애완동물과 자연을 좋아하고 헤비메탈 음악을 사랑합니다."
new_doctor = hospital_factory.generate_person(agent_particularities=description)

if new_doctor:
    print(f"\n새로운 타이니퍼슨 생성 완료: {new_doctor.name}")
    print(f"간단 소개: {new_doctor.minibio()}") # minibio()는 페르소나의 요약 정보를 보여줍니다.
    # 예시 출력:
    # 새로운 타이니퍼슨 생성 완료: Dr. Isabella Oliveira
    # 간단 소개: Dr. Isabella Oliveira, 34세, 상파울루 종합병원 심장내과 의사. ... 헤비메탈 팬.
else:
    print("타이니퍼슨 생성에 실패했습니다.")

# 시뮬레이션 종료
control.end()
```
위 코드를 실행하면, `hospital_factory`는 LLM에게 "상파울루의 한 병원"이라는 배경과 "브라질 의사, 애완동물과 자연을 좋아하고 헤비메탈을 사랑함"이라는 특징을 전달하여, 이에 맞는 상세한 페르소나를 가진 `TinyPerson` 객체를 생성합니다. `new_doctor.name`이나 `new_doctor.minibio()`를 통해 LLM이 만들어낸 캐릭터의 이름과 간단한 소개를 확인할 수 있습니다. LLM이 창의적으로 만들기 때문에 실행할 때마다 이름이나 세부 설정은 조금씩 달라질 수 있습니다!

여기서 `control.begin()`과 `control.end()`는 [제1장: 시뮬레이션 제어 (Simulation Control)](01_시뮬레이션_제어__simulation_control__.md)에서 배운 내용으로, 팩토리가 LLM을 호출하여 페르소나를 생성하는 과정과 그 결과를 캐싱할 수 있게 해줍니다.

### 3. 여러 명의 페르소나 한 번에 생성하기: `generate_people()`

만약 비슷한 특징을 가진 여러 명의 캐릭터가 필요하다면 `generate_people()` 메서드를 사용할 수 있습니다.

```python
# (이전 코드에 이어서, 시뮬레이션은 시작된 상태라고 가정)

# 같은 설명으로 2명의 간호사 캐릭터 생성 요청
nurse_description = "경험이 풍부한 간호사이며, 환자들에게 친절하고 동정심이 많습니다."
number_to_generate = 2

nurses = hospital_factory.generate_people(
    number_of_people=number_to_generate,
    agent_particularities=nurse_description,
    verbose=True # 생성 과정을 간단히 출력
)

print(f"\n총 {len(nurses)}명의 간호사 페르소나가 생성되었습니다.")
for nurse in nurses:
    print(f"- {nurse.name} ({nurse.get('age')}세)") # get()으로 특정 정보 가져오기
```
`generate_people()`은 지정된 수만큼의 타이니퍼슨 객체 리스트를 반환합니다. `verbose=True`로 설정하면 생성될 때마다 간단한 정보가 출력됩니다. 각 캐릭터는 `nurse_description`을 바탕으로 하지만, LLM에 의해 고유한 이름, 나이, 세부 배경 등을 갖게 됩니다.

## 타이니퍼슨 팩토리는 어떻게 작동할까요? (내부 모습 살짝 보기)

타이니퍼슨 팩토리가 어떻게 마법처럼 설명만으로 캐릭터를 만들어낼까요? 그 비밀은 바로 LLM에게 전달하는 '요청서(프롬프트)'에 있습니다.

### 1. 특별한 요청서 준비 (프롬프트 엔지니어링)

`TinyPersonFactory` 내부에는 캐릭터 생성을 위한 특별한 '요청서 템플릿'이 준비되어 있습니다. (실제로는 `generate_person.mustache`라는 템플릿 파일을 사용합니다.) 이 템플릿에는 다음과 같은 정보들이 채워져 LLM에게 전달됩니다:

*   **배경 컨텍스트 (`context_text`)**: "상파울루의 한 병원입니다." 와 같이 팩토리를 만들 때 제공한 정보입니다.
*   **요청된 캐릭터 특징 (`agent_particularities`)**: "브라질 의사, 애완동물과 자연을 좋아하고 헤비메탈을 사랑함" 과 같이 사용자가 `generate_person`에 전달한 설명입니다.
*   **생성 예시**: LLM에게 어떤 형식으로 캐릭터 정보를 만들어야 하는지 알려주기 위해, 이미 잘 만들어진 캐릭터 페르소나의 예시(JSON 형식) 몇 개가 포함됩니다. (예: `Friedrich_Wolf.agent.json`, `Sophie_Lefevre.agent.json` 파일의 내용)
*   **이미 사용된 이름 목록**: 시뮬레이션 내에서 캐릭터 이름이 중복되지 않도록, 지금까지 생성된 모든 타이니퍼슨의 이름 목록 (`TinyPerson.all_agents_names()`)과 현재 팩토리가 생성한 캐릭터들의 간단한 소개 목록 (`self.generated_minibios`)을 전달하여, LLM이 새로운 이름을 짓도록 유도합니다.

### 2. LLM 셰프에게 요리 주문 (`_aux_model_call`)

이렇게 잘 준비된 요청서(프롬프트)는 `_aux_model_call`이라는 내부 함수를 통해 [제4장: OpenAI 유틸리티 (OpenAI Utilities)](04_openai_유틸리티__openai_utilities__.md)를 거쳐 LLM에게 전달됩니다. 이때 LLM에게 "답변은 반드시 JSON 형식으로 줘!"라고 특별히 요청합니다. LLM은 이 요청서를 보고 창의력을 발휘하여 캐릭터의 이름, 나이, 직업, 성격, 배경 이야기 등을 포함하는 상세한 프로필을 JSON 형태로 '요리'해냅니다.

`_aux_model_call` 함수는 `@transactional` 데코레이터로 장식되어 있어, [제1장: 시뮬레이션 제어 (Simulation Control)](01_시뮬레이션_제어__simulation_control__.md)의 캐싱 기능 덕분에 동일한 요청에 대해서는 LLM을 다시 호출하지 않고 저장된 결과를 재사용할 수 있습니다.

### 3. 캐릭터 조립 및 완성 (`_setup_agent`)

LLM이 캐릭터 프로필(JSON)을 반환하면, `TinyPersonFactory`는 먼저 이 프로필에 있는 이름이 이미 사용된 이름은 아닌지 확인합니다. 만약 중복되거나 다른 문제가 있다면, 몇 번 더 (최대 `attepmpts` 횟수만큼) LLM에게 새로운 프로필을 요청할 수 있습니다.

성공적으로 고유한 프로필을 받으면, 다음 단계가 진행됩니다:
1.  새로운 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md) 객체가 생성됩니다 (예: `person = TinyPerson(name="Dr. Isabella Oliveira")`).
2.  `_setup_agent`라는 내부 함수가 호출되어, LLM이 생성한 JSON 프로필의 모든 세부 정보를 이 새로운 타이니퍼슨 객체에 설정합니다. 이 과정은 마치 [제2장: 타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md)에서 `define()` 메서드를 여러 번 호출하는 것과 비슷하지만, 자동으로 한 번에 처리됩니다.
    (`agent.include_persona_definitions(configuration)` 코드가 이 역할을 합니다.)
3.  `_setup_agent` 함수 역시 `@transactional`로 장식되어 있어, 이 설정 과정도 캐싱될 수 있습니다.
4.  마지막으로, 새로 생성된 타이니퍼슨 객체가 사용자에게 반환됩니다.

이 과정을 간단한 순서도로 나타내면 다음과 같습니다:

```mermaid
sequenceDiagram
    participant UserCode as 사용자 코드
    participant Factory as 타이니퍼슨 팩토리
    participant LLM as OpenAI LLM
    participant NewPerson as 새 타이니퍼슨 객체

    UserCode->>Factory: generate_person("의사, 헤비메탈 좋아함") 호출
    Factory->>Factory: 프롬프트 템플릿 + 컨텍스트 + 특징 + 예시 + 사용된 이름으로 프롬프트 구성
    Factory->>LLM: (_aux_model_call 통해) 완성된 프롬프트로 페르소나 JSON 요청
    LLM-->>Factory: 페르소나 JSON 응답 ("Isabella Oliveira", 34세, ...)
    Factory->>Factory: 이름 중복 검사 (필요시 재시도)
    Factory->>NewPerson: TinyPerson("Isabella Oliveira") 객체 생성
    Factory->>NewPerson: (_setup_agent 통해) LLM 응답(JSON)으로 페르소나 상세 설정
    NewPerson-->>Factory: 설정 완료된 타이니퍼슨 객체
    Factory-->>UserCode: 완성된 타이니퍼슨 객체 반환
end
```

### 코드 살짝 엿보기 (`tinytroupe/factory/tiny_person_factory.py`)

실제 코드에서 이 마법이 어떻게 일어나는지 몇 가지 핵심 부분을 살펴보겠습니다. (코드는 이해를 돕기 위해 실제보다 간략화될 수 있습니다.)

*   **팩토리 초기화 (`__init__`)**:
    팩토리가 처음 만들어질 때, 컨텍스트 정보와 프롬프트 템플릿 경로 등을 설정합니다.

    ```python
    # tinytroupe/factory/tiny_person_factory.py 일부
    class TinyPersonFactory(TinyFactory):
        def __init__(self, context_text, simulation_id:str=None):
            super().__init__(simulation_id)
            # 페르소나 생성 프롬프트 템플릿 파일 경로
            self.person_prompt_template_path = os.path.join(
                os.path.dirname(__file__), 'prompts/generate_person.mustache'
            )
            self.context_text = context_text # 배경 컨텍스트
            self.generated_minibios = [] # 이 팩토리가 생성한 페르소나 요약본 목록
            self.generated_names = []    # 이 팩토리가 생성한 이름 목록
    ```

*   **페르소나 생성 요청 (`generate_person`)**:
    이 메서드는 프롬프트를 만들고, LLM을 호출하며, 결과를 처리하는 전체 과정을 지휘합니다.

    ```python
    # tinytroupe/factory/tiny_person_factory.py 일부
    def generate_person(self, 
                        agent_particularities:str=None, 
                        temperature:float=1.5, # LLM 창의성 조절
                        # ... 기타 파라미터 ...
                        attepmpts:int=10): # 이름 중복 시 재시도 횟수
        
        # 예시 페르소나 JSON 파일 로드 (LLM에게 출력 형식 안내용)
        example_1 = json.load(open(os.path.join(os.path.dirname(__file__), '../examples/agents/Friedrich_Wolf.agent.json')))
        example_2 = json.load(open(os.path.join(os.path.dirname(__file__), '../examples/agents/Sophie_Lefevre.agent.json')))

        # 프롬프트 템플릿에 정보 채우기 (chevron 라이브러리 사용)
        prompt_data = {
            "context": self.context_text,
            "agent_particularities": agent_particularities,
            "example_1": json.dumps(example_1["persona"], indent=4), # JSON 문자열로 변환
            "example_2": json.dumps(example_2["persona"], indent=4),
            "already_generated_minibios": self.generated_minibios,
            "already_generated_names": TinyPerson.all_agents_names() # 전체 시뮬레이션의 이름들
        }
        rendered_prompt = chevron.render(open(self.person_prompt_template_path).read(), prompt_data)
        
        # ... (aux_generate 함수를 통해 LLM 호출 및 이름 중복 검사 로직) ...
        # agent_spec = self._try_to_generate_unique_spec(rendered_prompt, temperature, attepmpts)

        # 실제로는 aux_generate 내부에서 _aux_model_call을 호출합니다.
        # 여기서는 개념을 단순화하여 LLM 호출 부분을 나타냅니다.
        messages = [{"role": "system", "content": "당신은 사람 시뮬레이션 명세 생성 시스템입니다..."},
                    {"role": "user", "content": rendered_prompt}]
        
        # _aux_model_call 이 LLM 호출을 담당 (캐싱 가능)
        llm_output_message = self._aux_model_call(messages=messages, temperature=temperature, ...)
        
        if llm_output_message:
            agent_spec = utils.extract_json(llm_output_message["content"]) # JSON 파싱
            
            # 이름 중복 및 유효성 검사 후 (실제 코드에서는 더 복잡)
            if agent_spec and agent_spec["name"].lower() not in self.generated_names:
                person = TinyPerson(agent_spec["name"]) # 타이니퍼슨 객체 생성
                self._setup_agent(person, agent_spec)    # 페르소나 설정 (캐싱 가능)
                self.generated_minibios.append(person.minibio())
                self.generated_names.append(person.get("name").lower())
                return person
        
        return None # 생성 실패
    ```
    위 코드는 실제 `generate_person` 내부 로직을 단순화하여 보여줍니다. 중요한 점은 `chevron.render`로 프롬프트를 만들고, `_aux_model_call`로 LLM에게 JSON 응답을 요청한 뒤, 그 결과를 바탕으로 `TinyPerson` 객체를 만들고 `_setup_agent`로 상세 정보를 채운다는 것입니다.

*   **LLM 호출 담당 (`_aux_model_call`)**:
    이 함수는 실제 LLM API를 호출하는 역할을 합니다. `@transactional` 덕분에 캐싱이 가능합니다.

    ```python
    # tinytroupe/factory/tiny_person_factory.py 일부
    @transactional # 시뮬레이션 제어에 의해 캐싱될 수 있음
    def _aux_model_call(self, messages, temperature, frequency_penalty, presence_penalty):
        # openai_utils를 통해 LLM API 호출, 응답 형식은 JSON 객체로 요청
        return openai_utils.client().send_message(
            messages, 
            temperature=temperature, 
            frequency_penalty=frequency_penalty, 
            presence_penalty=presence_penalty,
            response_format={"type": "json_object"} # LLM에게 JSON 형식으로 응답하도록 요청
        )
    ```

*   **페르소나 설정 (`_setup_agent`)**:
    LLM이 생성한 JSON 데이터를 바탕으로 `TinyPerson` 객체의 페르소나를 실제로 설정합니다. 이 함수도 `@transactional`로 캐싱될 수 있습니다.

    ```python
    # tinytroupe/factory/tiny_person_factory.py 일부
    @transactional # 시뮬레이션 제어에 의해 캐싱될 수 있음
    def _setup_agent(self, agent, configuration):
        # JSON 설정(configuration)을 에이전트의 페르소나에 적용
        agent.include_persona_definitions(configuration)
        
        # 반환값이 없음에 유의 (에이전트 객체 자체를 캐싱하지 않기 위함)
    ```
    `agent.include_persona_definitions(configuration)`는 `configuration` (LLM이 생성한 JSON)에 있는 모든 키와 값을 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md) 객체의 페르소나에 한 번에 설정해주는 편리한 메서드입니다.

이처럼 타이니퍼슨 팩토리는 잘 만들어진 프롬프트와 LLM의 능력을 활용하여, 복잡한 페르소나 생성 과정을 자동화하고 사용자가 더 창의적인 작업에 집중할 수 있도록 도와줍니다.

## 정리 및 다음 단계

이번 장에서는 `타이니퍼슨 팩토리 (TinyPerson Factory)`라는 강력한 도구에 대해 배웠습니다. 간단한 설명과 배경 컨텍스트만으로 LLM을 활용하여 상세하고 독특한 페르소나를 가진 [타이니퍼슨 (TinyPerson)](02_타이니퍼슨__tinyperson__.md)을 자동으로 생성하는 방법을 익혔습니다. `TinyPersonFactory` 객체를 만들고, `generate_person()` 또는 `generate_people()` 메서드를 사용하여 원하는 캐릭터를 손쉽게 만들어낼 수 있다는 것을 알게 되었습니다. 또한, 팩토리 내부에서 프롬프트 엔지니어링, LLM 호출, 결과 처리 및 캐싱이 어떻게 이루어지는지도 간략하게 살펴보았습니다.

**핵심 요약:**
*   `TinyPersonFactory`는 LLM을 사용하여 설명 기반으로 새로운 타이니퍼슨을 자동으로 생성합니다.
*   `TinyPersonFactory(context_text="배경")`로 팩토리를 생성합니다.
*   `factory.generate_person(agent_particularities="특징")`으로 단일 페르소나를, `factory.generate_people()`로 여러 페르소나를 생성할 수 있습니다.
*   내부적으로는 프롬프트 템플릿, 예시 페르소나, 이름 중복 방지 로직 등을 사용하여 LLM으로부터 JSON 형식의 페르소나 정의를 얻어냅니다.
*   LLM 호출 및 페르소나 설정 과정은 [제1장: 시뮬레이션 제어 (Simulation Control)](01_시뮬레이션_제어__simulation_control__.md)의 캐싱 기능에 의해 최적화될 수 있습니다.

이제 우리는 다양한 개성을 가진 타이니퍼슨들을 빠르고 효율적으로 준비할 수 있게 되었습니다. 하지만 타이니퍼슨이 단순히 페르소나만 가지고 상호작용하는 것을 넘어, 마치 사람처럼 기억을 활용하고, 주변 환경을 인지하며, 더 복잡한 목표를 추구하려면 어떻게 해야 할까요?

다음 [제6장: 정신 능력 (Mental Faculties)](06_정신_능력__mental_faculties__.md)에서는 타이니퍼슨에게 이러한 고차원적인 인지 능력을 부여하는 '정신 능력'에 대해 자세히 알아보겠습니다. 타이니퍼슨이 더욱 똑똑해지는 여정에 함께해주세요!

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)