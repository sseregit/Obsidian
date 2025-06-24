1. 화면 만들기.
    1-1 CM21000 copy
    1-2 AUIGrid 제거 -> /inspectioncode/group -> complysite/inspection-code/code-group-list의 table로 변경
    1-3 저장 버튼 활성화
2. 테이블 작성 contract_inspection_map
```sql
CREATE TABLE contract_inspection_map (
    contract_id BIGINT NOT NULL,
    grp_cd VARCHAR(255) NOT NULL,
    reg_id VARCHAR(255),
    reg_dtm TIMESTAMP(6),
    PRIMARY KEY (contract_id, grp_cd)
);
```
1. Entity, Repository 작성
2. 저장 버튼 API 작성
3. 테스트