### 오라클과 차이점
* * *
1. 오라클에서 date 데이터타입의 컬럼 만들때 디폴트로 준 sysdate는   
mysql에서 **current_timeStamp**

2. concat()은 문자열을 합쳐준다.   
```concat('%',#{search},'%') ``` 
3. 페이징 처리가 다르다
   ``` 
   오라클은 서브쿼리로 rowNum을 1 between 10
   MySQL은 limit 사용


   select * from
		(select rownum R, N.* from
		(select * from notice order by num desc) N )
		where R between 1 and 10


    select * from notice order by num desc
		limit 시작인덱스(0부터 시작),갯수
   ```
