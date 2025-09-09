
# temperature
## 값이 낮을 수록
- 정확성이 높아진다.
- 일관적이고 예측 가능하다.
## 값이 높을 수록
- 창의성이 높아진다.
- 가끔 비논리적이거나 사실에서 벗어난 답이 나올 수 있다.
****
# LLM과 ChatModel은 다르다!
## LLM
- 거대한 언어 예측 엔진
## ChatModel
- LLM을 기반으로, 대화 시나리오에 맞게 래핑모델
### HumanMessage
- 사용자가 보낸 프롬프트
### AIMessage
- 과거에 응답한 메시지
- role = assistant
### SystemMesage
- 지침, 규칙, 역할을 주는 메시지
****
## OutputParser
- LLM의 output을 구조별로 parse 할수 있게 해준다.
- LLM의 응답을 변형해야 할때가 있기 때문에
****
## Streaming
- LLM의 응답이 생성되는대로 볼수 있게 해준다.
****
## Callbacks
- LLM에 일어나는 event를 감지하는 아주 쉬운방법
****
# Model I/O
- input == prompt | language model | outputparser
- ouput == 응답
## 사용법
- 미리 예제를 넣어놓거나. (few-shot)
- 예제를 길이 or Token등으로 제한을 할수도 있고 (Selector)
- 파일(json, yaml)로도 전달이 가능하다
- pipeline으로 prompt를 이어 붙여 활용 가능하다.