### 펑션과 프로시저

#### 개요
펑션은 반환값이 있고, 프로시저는 반환값이 없다.

#### 등록
펑션 - 유의 선언은 `RETURNS` 키워드이고, 실제 반환에서는 `RETURN` 키워드.
```
CREATE FUNCTION [펑션명] ([파라미터1] [파라미터 타입1], [파라미터2] [파라미터 타입2] ...) RETURNS [반환타입]
BEGIN
  DECLARE [내부변수명] [내부변수타입];
  ... 내용 쿼리 ...
RETURN [반환값];
END;
```
프로시저
```
CREATE PROCEDURE [프로시저명] ([파라미터1] [파라미터 타입1], [파라미터2] [파라미터 타입2] ...)
BEGIN
  DECLARE [내부변수명] [내부변수타입];
  ... 내용 쿼리 ...
END;
```

#### 삭제
펑션이나 프로시저나 동일함
```
DROP FUNCTION IF EXISTS [펑션명];
DROP PROCEDURE IF EXISTS [프로시저명];
```

#### 호출
펑션
```
SELECT [펑션명]([변수 ...]) FROM DUAL;
```
프로시저
```
CALL [프로시저명]([변수 ...]);
```

#### 기타
- 문자열 변경시 파라미터 수집 구간에서 오류가 날 가능성이 있다. 선언부 파라미터 뒤에 `CHARSET [문자열]` 을 추가해서 해결할 수 있다.
```
FUNCTION ADDMEMBER(`v_name` VARCHAR(100) CHARSET utf8mb4) RETURNS INT(11)
BEGIN
 INSERT INTO MEMBER (name) VALUES(v_name);
 RETURN ROW_COUNT();
END;
```
- `ROW_COUNT()` 반환시, 등록/수정/삭제 시 변경된 로우 수를 반환함

#### History
- 2017.04.29 : 초안작성
