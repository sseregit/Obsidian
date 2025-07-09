CREATE TABLE contract_inspection_result (
    id SERIAL PRIMARY KEY,
    contract_id INTEGER NOT NULL,
    grp_cd VARCHAR(50) NOT NULL,
    ins_cd VARCHAR(50) NOT NULL,
    result BOOLEAN NOT NULL,
    remark TEXT,
    reg_dtm TIMESTAMP WITHOUT TIME ZONE NOT NULL DEFAULT now(),
    reg_id VARCHAR(50) NOT NULL
);

-- 인덱스 (성능 및 중복 방지에 유용)
CREATE INDEX idx_contract_inspection_result_contract_id ON contract_inspection_result(contract_id, grp_cd);
CREATE INDEX idx_contract_inspection_result_ins_cd ON contract_inspection_result(ins_cd);

-- (선택) 중복 결과 방지: 계약별 grp_cd-ins_cd는 1건만 기록
-- ALTER TABLE contract_inspection_result ADD CONSTRAINT uq_contract_result UNIQUE (contract_id, grp_cd, ins_cd);