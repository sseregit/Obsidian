# BFT 계열
- 블록체인에서 Byzantine Fault Tolerance(비잔틴 장애 허용) 기반의 합의 알고리즘 계열
- 일부 노드가 악의적으로 행동하거나 장애가 나더라도 전체 시스템이 정상적인 합의를 유지할 수 있는 기술
### 종류

| 알고리즘               | 특징                        | 사용 사례                |
| ------------------ | ------------------------- | -------------------- |
| PBFT(Pracical BFT) | 성숙된 기술, 노드 수 증가에 따른 성능 저하 | Hyperledger Fabric   |
| Tendermint         | 블록체인 친화적 설계, 빠른 확장성       | Cosmos Hub           |
| HotStuff           | 체인 기반 BFT, 효율적인 리더 교체     | Facebook Libra(Diem) |
| SBFT               | 고성능, 가변 리더 구조             | 금융 기관 기반 시스템         |
