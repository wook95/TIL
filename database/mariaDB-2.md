### 오라클과 차이점
* * *
1. 오라클에서 date 데이터타입의 컬럼 만들때 디폴트로 준 sysdate는   
mysql에서 **current_timeStamp**이다. 데이터 타입은 DATE(년월일)와 DATETIME중 DATETIME을 쓴다(연월일시간분초까지 표현 가능)

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
 4. 테이블 자기 자신을 표현하는 서브쿼리를 쓸땐 엘리아스(별칭)를 써줘야한다
   ```
   insert into qna(title,writer,contents,ref,step,depth)
				    values(#{title},#{writer},#{contents},
				(select ref from qna Q where num=#{num}),
				(select step+1 from qna Q where num=#{num}),
				(select depth+1 from qna Q where num=#{num})
					)
```
