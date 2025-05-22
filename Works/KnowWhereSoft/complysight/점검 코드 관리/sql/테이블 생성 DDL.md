create table inspection_code_group
(
    grp_cd     varchar(255) not null
        primary key,
    chg_dtm    timestamp(6),
    chg_id     varchar(255),
    grp_cd_epl varchar(255),
    grp_cd_nm  varchar(255),
    grp_order  integer,
    ref1       varchar(255),
    ref2       varchar(255),
    ref3       varchar(255),
    reg_dtm    timestamp(6),
    reg_id     varchar(255),
    sys_div    varchar(255),
    use_yn     varchar(255)
);

COMMENT ON TABLE inspection_code_group IS '점검 코드 그룹 테이블';

COMMENT ON COLUMN inspection_code_group.grp_cd     IS '점검 코드 그룹 코드 (PK)';
COMMENT ON COLUMN inspection_code_group.grp_cd_nm  IS '점검 코드 그룹 이름';
COMMENT ON COLUMN inspection_code_group.grp_cd_epl IS '점검 코드 그룹 설명';
COMMENT ON COLUMN inspection_code_group.grp_order  IS '점검 코드 그룹 정렬 순서';

COMMENT ON COLUMN inspection_code_group.ref1       IS '참조 필드 1';
COMMENT ON COLUMN inspection_code_group.ref2       IS '참조 필드 2';
COMMENT ON COLUMN inspection_code_group.ref3       IS '참조 필드 3';

COMMENT ON COLUMN inspection_code_group.sys_div    IS '시스템 구분;
COMMENT ON COLUMN inspection_code_group.use_yn     IS '사용 여부 (Y: 사용, N: 미사용)';

COMMENT ON COLUMN inspection_code_group.reg_dtm    IS '등록 일시';
COMMENT ON COLUMN inspection_code_group.reg_id     IS '등록자 ID';
COMMENT ON COLUMN inspection_code_group.chg_dtm    IS '수정 일시';
COMMENT ON COLUMN inspection_code_group.chg_id     IS '수정자 ID';

****
create table inspection_code_detail
(
    dts_cd     varchar(255) not null,
    grp_cd     varchar(255) not null,
    chg_dtm    timestamp(6),
    chg_id     varchar(255),
    dts_cd_eng varchar(255),
    dts_cd_epl varchar(255),
    dts_cd_nm  varchar(255),
    dts_order  integer,
    ref1       varchar(255),
    ref2       varchar(255),
    reg_dtm    timestamp(6),
    reg_id     varchar(255),
    use_yn     varchar(255),
    primary key (dts_cd, grp_cd)
);

COMMENT ON TABLE inspection_code_detail IS '점검 코드 상세 테이블 (그룹별 상세 항목 정의)';

COMMENT ON COLUMN inspection_code_detail.dts_cd      IS '점검 상세 코드 (PK)';
COMMENT ON COLUMN inspection_code_detail.grp_cd      IS '상위 점검 그룹 코드 (FK)';

COMMENT ON COLUMN inspection_code_detail.dts_cd_nm   IS '점검 상세 항목 이름';
COMMENT ON COLUMN inspection_code_detail.dts_cd_eng  IS '점검 상세 항목 영문 이름';
COMMENT ON COLUMN inspection_code_detail.dts_cd_epl  IS '점검 상세 항목 설명';
COMMENT ON COLUMN inspection_code_detail.dts_order   IS '정렬 순서';

COMMENT ON COLUMN inspection_code_detail.ref1        IS '참조 필드 1';
COMMENT ON COLUMN inspection_code_detail.ref2        IS '참조 필드 2';

COMMENT ON COLUMN inspection_code_detail.use_yn      IS '사용 여부 (Y: 사용, N: 미사용)';

COMMENT ON COLUMN inspection_code_detail.reg_dtm     IS '등록 일시';
COMMENT ON COLUMN inspection_code_detail.reg_id      IS '등록자 ID';
COMMENT ON COLUMN inspection_code_detail.chg_dtm     IS '수정 일시';
COMMENT ON COLUMN inspection_code_detail.chg_id      IS '수정자 ID';