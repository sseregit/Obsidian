### [3.0 LLMs and Chat Models](https://nomadcoders.co/fullstack-gpt/lectures/4549)
- LangChain
	- LLM
	- Chat model
***
### [3.1 Predict Messages](https://nomadcoders.co/fullstack-gpt/lectures/4550)
- HumanMessage
- AIMessage
	- AI에 의해 보내지는 것
- SystemMessage
	- 우리가 LLM에 설정들을 제공하기 위한 Message
```python
from langchain.chat_models import ChatOpenAI  
  
chat = ChatOpenAI(temperature=0.1)  
#%%  
from langchain.schema import HumanMessage, AIMessage, SystemMessage  
  
messages = [  
    SystemMessage(content="You are a geography expert. And you only reply in Italian."),  
    AIMessage(content="Ciao, mi chiamo Paolo!"),  
    HumanMessage(content="What is the distance between Mexico and Thailand. Also, what is your name?")  
]  
  
chat.predict_messages(messages)
```
***
### [3.2 Prompt Templates](https://nomadcoders.co/fullstack-gpt/lectures/4551)
- prompt
	- LLM과 의사소통할 수있는 유일한 방법
- ChatPromptTemplate
	- template을 message로 부터 만든다.
- PromptTemplate
	- string을 이용해서 template를 만든다.
- template를 사용해서 변수(variable)들을 검증(validate)할 수있다.
```python
from langchain.chat_models import ChatOpenAI  
from langchain.prompts import PromptTemplate, ChatPromptTemplate  
  
chat = ChatOpenAI(temperature=0.1)  
  
template = PromptTemplate.from_template(  
    "What is the distance between {country_a} and {country_b}."  
)  
  
prompt = template.format(country_a="Mexico", country_b="Thailand")  
  
chat.predict(prompt)  
#%%  
from langchain.schema import HumanMessage, AIMessage, SystemMessage  
  
template = ChatPromptTemplate.from_messages([  
    ("system", "You are a geography expert. And you only reply in {language}."),  
    ("ai", "Ciao, mi chiamo {name}!"),  
    ("human", "What is the distance between {country_a} and {country_b}. Also, what is your name?")  
])  
  
prompt = template.format_messages(  
    language="Greek",  
    name="Socrates",  
    country_a="Mexico",  
    country_b="Thailand",  
)  
  
chat.predict_messages(prompt)
```
***
### [3.3 OutputParser and LCEL](https://nomadcoders.co/fullstack-gpt/lectures/4552)
- Output Parser가 필요한 이유
	- LLM의 응답(Response)을 변형해야 할 때가 있기 때문이다.
***
### [3.4 Chaining Chains](https://nomadcoders.co/fullstack-gpt/lectures/4553)
***
### [3.5 Recap (05:21)](https://nomadcoders.co/fullstack-gpt/lectures/4554)
***
