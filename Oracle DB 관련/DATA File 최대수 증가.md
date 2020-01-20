## 데이터 파일 최대수 증가 방법
### 오라클 테이블스페이스를 용량을 증설하기위해 데이터파일을 추가하다보면 ORA-00059와 같은 에러가 발생할 수 있다.
### 에러의 내용인 즉슨 최대 데이터파일 수를 초과하여 생성할 수 가 없다는 것이다. 이럴경우 최대생성수를 증가시켜주면 해결된다.
```
#] su - oracle                                        // 오라클 접속위한 오라클 계정 접속
#] sqlplus '/as sysdba'                               // sql 접속
SQL> alter system set db_files = 1500 scope=spfile;   // 데이터파일 최대생성수를 1500개로 늘리기(기본 최대수는 200개이다.SQL
SQL> shutdown immediate;                              // 변경된 값을 적용하기위해 재기동진행
SQL> startup
SQL> show parameter db_files                          // 값이 변경되었는지 확인
```
