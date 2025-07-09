```sql
CREATE TABLE contract_inspection_result (
    id SERIAL PRIMARY KEY, -- 고유 식별자 (자동 증가)
    
    contract_id INTEGER NOT NULL, -- 계약 ID (cm_contract_mg.contract_id 참조)
    
    grp_cd VARCHAR(50) NOT NULL, -- 검사 그룹 코드 (contract_inspection_map.grp_cd 참조)
    
    ins_cd VARCHAR(50) NOT NULL, -- 검사 항목 코드 (inspection_code_detail.ins_cd 참조)
    
    result BOOLEAN NOT NULL, -- 검사 결과 (true: 합격, false: 불합격)
    
    remark TEXT, -- 검사 비고 (특이사항 등)
    
    reg_dtm TIMESTAMP WITHOUT TIME ZONE NOT NULL DEFAULT now(), -- 등록 일시
    
    reg_id VARCHAR(50) NOT NULL -- 등록자 ID
);

COMMENT ON TABLE contract_inspection_result IS '계약별 검사 결과를 저장하는 테이블';

COMMENT ON COLUMN contract_inspection_result.id IS '기본 키, 자동 증가 ID';
COMMENT ON COLUMN contract_inspection_result.contract_id IS '계약 ID (cm_contract_mg 참조)';
COMMENT ON COLUMN contract_inspection_result.grp_cd IS '검사 그룹 코드 (grp_cd)';
COMMENT ON COLUMN contract_inspection_result.ins_cd IS '검사 항목 코드 (inspection_code_detail 참조)';
COMMENT ON COLUMN contract_inspection_result.result IS '검사 결과 (true: 합격, false: 불합격)';
COMMENT ON COLUMN contract_inspection_result.remark IS '검사 관련 비고 또는 특이사항';
COMMENT ON COLUMN contract_inspection_result.reg_dtm IS '데이터 등록 일시';
COMMENT ON COLUMN contract_inspection_result.reg_id IS '데이터 등록자 ID';
```

-- 인덱스
CREATE INDEX idx_result_grp_contract_regdtm
ON contract_inspection_result (grp_cd, contract_id, reg_dtm DESC);
