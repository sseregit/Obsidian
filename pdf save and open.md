- 적용할 화면
	- RA3000A
		- 인쇄 버튼 -> PDF OPEN 으로
- 작업 내용
	1. PM10000에 시스템 SM050에 Rack 지역(RM000) 코드를 모두 추가한다.
		1. 운영에 적용할 DML을 정리해야한다.
	2. PM60000에 신규등록을 한다
		1. RACK 관련 파일은 반드시 pdf 여야한다.
	4. RA3000A PDF OPEN 버튼 클릭시 PDF가 뜬다.

코드 저장 DML
```sql
select 'insert into cm_dts_cd (chg_dtm, chg_id, dts_cd_eng, dts_cd_epl, dts_cd_nm, dts_order, ref1, ref2, reg_dtm, reg_id, use_yn, dts_cd, grp_cd) values (NULL, NULL, NULL, '''||DTS_CD_EPL||' 실장도 PDF'', '''||DTS_CD_EPL||' 실장도 PDF'','||(DTS_ORDER+7)||','||''''''||', NULL,sysdate, ''hcinfotest'',''Y'','''||DTS_CD||''',''SM050'');'
  from cm_dts_cd
 where grp_cd = 'RM000'
 order by dts_order;
```
	
