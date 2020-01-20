## Tablespace 용량 추가 방법
### Tablespace 용량이 부족하여 DB에 데이터 적재가 안될 경우 다음과 같이 용량을 추가한다.
```
#] su - oracle             //sql에 접속하여 테이블스페이스의 현재 사용량 및 용량 체크를 위해 오라클 계정으로 변경
#] sqlplus '/as sysdba'    //sql 접속 후 용량체크
SQL> select   substr(a.tablespace_name,1,30) TEST,
         round(sum(a.total1)/1024/1024,1) "TotalMB",
         round(sum(a.total1)/1024/1024,1)-round(sum(a.sum1)/1024/1024,1) "UsedMB",
         round(sum(a.sum1)/1024/1024,1) "FreeMB",
         round((round(sum(a.total1)/1024/1024,1)-round(sum(a.sum1)/1024/1024,1))/round(sum(a.total1)/1024/1024,1)*100,2) "Used%"
     from
         (select tablespace_name,0 total1,sum(bytes) sum1,max(bytes) MAXB,count(bytes) cnt
          from dba_free_space
          group by tablespace_name
          union
          select tablespace_name,sum(bytes) total1,0,0,0
          from dba_data_files
          group by tablespace_name) a
      group by a.tablespace_name
      order by TEST;
```  
##### 사용하는 테이블스페이스 공간을 확인하여 사용중인 용량이 부족하다면 데이터파일을 추가하여 용량을 증설시켜준다.  
```
SQL> alter tablespace 테이블 스페이스명 add datafile '데이터파일경로' size 1000M autoextend on;  
예시) alter tablespce TEST_DAT add datafile '/home/oracle/db/wisiem/dat/TEST_DAT_ADD5.DBF' size 1000M autoextend on;
```
##### 위와 같이 명령어를 입력하면 데이터파일이 추가되고 테이블스페이스 공간 확장된다. 더불어 autoextend on 명령어로 자동 확장이 된다.  
##### 데이터파일 추가 시 최대 용량은 한번에 30000M 이다.
