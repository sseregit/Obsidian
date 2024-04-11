### [4.0 Introduction](https://nomadcoders.co/fullstack-gpt/lectures/4555)
- Model I/O
	- 입력(input)과 출력(output)이 있다.
	- input == prompt
- Retrieval
	- 외부 데이터로 접근하여 이를 모델에 어떻게 제공하는 것에 관한것
- Chains
- Agents
	- 독립적으로 AI가 작동하도록 만들 수 있게 해준다.
- Memory
	- 챗봇에 memory(기억)할 수 있도록 하는 것
- Callbacks
	- 기본적으로 model이 무엇을 하고 있는지 중간에 알 수 있도록 하는것
	- 모델이 답변을 제공하기 전에 실제로 모델이 어떤 일을 하고 있는 지 확인할 수 있다.
***
### [4.1 FewShotPromptTemplate](https://nomadcoders.co/fullstack-gpt/lectures/4556)
- FewShotPromptTemplate
	- prompt를 제공하는것보다 어떻게 대답해야 하는지에 대한 예제를 제공해주는 것이 더 나은 방법이다.
	- 대답해야 하는 예제를 제공하는 일을 해준다.
***
### [4.2 FewShotChatMessagePromptTemplate](https://nomadcoders.co/fullstack-gpt/lectures/4557)
***
### [4.3 LengthBasedExampleSelector](https://nomadcoders.co/fullstack-gpt/lectures/4558)
- 예제를 무제한으로 넘겨줄수도 없고 비용도 늘어나는데 그걸 통제하는 역할을 할수 있다.
***
### [4.4 Serialization](https://nomadcoders.co/fullstack-gpt/lectures/4559)
- PipelinePromptTemplate
	- 많은 prompt들을 하나로 합칠 수 있도록 해준다.
***
### [4.5 Caching](https://nomadcoders.co/fullstack-gpt/lectures/4560)
- Caching
	- LM(언어 모델)의 응답을 저장할 수가 있다.
***
### [4.6 Serialization](https://nomadcoders.co/fullstack-gpt/lectures/4561)
- openAI의 모델을 사용할 때 지출하는 비용을 아는 방법\
```python
from langchain.chat_models import ChatOpenAI  
from langchain.callbacks import get_openai_callback  
  
chat = ChatOpenAI(  
    temperature=0.1,  
)  
  
with get_openai_callback() as usage:  
    a = chat.predict("What is the recipe for soju")  
    b = chat.predict("What is the recipe for bread")  
    print(a,b,"\n")  
    print(usage)
```
- 모델을 어떻게 저장하고 불러오는지에 대해서
```python
from langchain.chat_models import ChatOpenAI  
from langchain.llms.openai import OpenAI  
  
chat = ChatOpenAI(  
    temperature=0.1,  
    max_tokens=450,  
    model="gpt-3.5-turbo-16k"  
)  
  
chat.save("model.json")
```
- json으로 모델의 정보를 저장한다.
```python
from langchain.chat_models import ChatOpenAI  
from langchain.llms.openai import OpenAI  
from langchain.llms.loading import load_llm  
  
chat = load_llm("model.json")  
  
chat
```
- 저장한 모델의 정보를 불러온다.
***
