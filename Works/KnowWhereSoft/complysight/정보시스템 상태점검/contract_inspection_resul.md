```sql
CREATE TABLE contract_inspection_result  
(  
    id          SERIAL PRIMARY KEY,  
    contract_id INTEGER                 NOT NULL,  
    grp_cd      VARCHAR(255)            NOT NULL,  
    ins_cd      VARCHAR(255)            NOT NULL,  
    result      BOOLEAN                 NOT NULL,  
    remark      TEXT,  
    reg_dtm     TIMESTAMP DEFAULT now() NOT NULL,  
    reg_id      VARCHAR(255)            NOT NULL,  
    version     BIGINT                  NOT NULL -- 단순 숫자 증가  
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
COMMENT ON COLUMN contract_inspection_result.version IS '검사 결과 수집 시점 버전 (숫자 증가 방식)';  
  
CREATE INDEX idx_cir_grp_contract_version_regdtm  
    ON contract_inspection_result (grp_cd, contract_id, version, reg_dtm DESC);
```