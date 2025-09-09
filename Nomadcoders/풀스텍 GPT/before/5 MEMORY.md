### [5.0 ConversationBufferMemory](https://nomadcoders.co/fullstack-gpt/lectures/4562) 
- ConversationBufferMemory
	- 단순히 이전 대화 내용 전체를 저장하는 메모리
	- text completion 할때 유용하다. 예측할 때 텍스트를 자동 완성하고 싶을때
	- 단점
		- 대화 내용이 길어질수록 메모리도 계속 커지므로 비효율적임
***
### [5.1 ConversationBufferWindowMemory](https://nomadcoders.co/fullstack-gpt/lectures/4563) 
- ConversationBufferWindowMemory
	- 대화의 특정 부분만을 저장하는 메모리
		- 가장 최근 5개 메시지만 저장된다면 6개부터는 오래된 메시지가 버려지는 방식
	- 메모리를 특정 크기로 유지할 수 있다는게 이 메모리의 큰장점
***
### [5.2 ConversationSummaryMemory](https://nomadcoders.co/fullstack-gpt/lectures/4564) 
- ConversationSummaryMemory
	- message 그대로 저장하는것이 아니라 conversation의 요약을 자체적으로 해준다.
	- 처음엔 비효율적으로 보일 수 있으나 대화가 쌓이면서 효율적으로 변한다.
***
### [5.3 ConversationSummaryBufferMemory](https://nomadcoders.co/fullstack-gpt/lectures/4565) 
- ConversationSummaryBufferMemory
	- ConversationBufferMemory + ConversationSummaryMemory의 결합
	- 메모리에 보내온 메시지의 수를 저장하는 것
	- limit에 다다른 순간에, 무슨 일이 일어났는지 잊어버리는것 대신 오래된 메시지들을 summarize (요약) 한다.
	- 가장 최근의 상호작용을 계속 추적한다는 것
***
### [5.4 ConversationKGMemory](https://nomadcoders.co/fullstack-gpt/lectures/4566) 
- ConversationKGMemory
	- 대화 중의 엔티티의 knowledge graph를 만든다.
	- history가 아닌 엔티티를 가져온다.
***
### [5.5 Memory on LLMChain](https://nomadcoders.co/fullstack-gpt/lectures/4567) 
- LLM chain
	- off-the-shelf chain
		- 일반적인 목적을 가진 chain을 의미한다.
***
### [5.6 Chat Based Memory](https://nomadcoders.co/fullstack-gpt/lectures/4568) 
***
### [5.7 LCEL Based Memory](https://nomadcoders.co/fullstack-gpt/lectures/4569) 

***
### [5.8 Recap](https://nomadcoders.co/fullstack-gpt/lectures/4570) 
- LLM이 가져오는 프롬프트에 기록들을 넣는건 **직접 해줘야 한다**
- langchain은 Off-the-shelf Chain이 있다
	- 자동으로 LLM으로부터 응답값을 가져오고 memory를 업데이트 한다
	- ex) LLMChain
***
