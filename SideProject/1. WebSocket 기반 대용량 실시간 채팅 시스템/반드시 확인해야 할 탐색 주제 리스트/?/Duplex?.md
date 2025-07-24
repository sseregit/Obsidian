# 전이중 (Full-Duplex)
- 양방향 통신이 동시에 가능하다.
```mermaid
flowchart TB
    A(장치 A) <-->|동시 송수신| B(장치 B)
```
# 이중 단순 (Dual Simplex)
- 양방향 통신은 동시에 가능하지만, 각각 별도의 물리적 채널을 사용한다.
```mermaid
flowchart TB
    A(장치 A) -->|채널 1| B(장치 B)
    B -->|채널 2| A
```
# 반이중 (Half-Duplex)
- 양방향 통신 가능하지만 동시에는 불가능
- 전송과 수신을 순차적으로 해야한다.
```mermaid
flowchart TB
    A(장치 A) -->|전송 시도| B(장치 B)
    B -->|응답 시도| A
```
# 심플렉스 (Simplex)
- 단방향 통신만 가능하다.
- 수신 장치는 응답할 수 없다.
```mermaid
flowchart TB
    A(송신 전용 장치) -->|일방향 통신| B(수신 전용 장치)
```



