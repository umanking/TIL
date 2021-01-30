## Note!

### block, non-blocking , sync async

- block, non-block: 제어권에 관한이야기

- - blocking: 제어권을 넘겨준다. block 되어있다. 
  - non-blocking: 제어권을 바로 넘겨준다. 
  - 여기서 궁금한것? 그럼 결과값은? 

- Sync, Async: (시간 관점) **제어권을** **반환하는** **시간**과 **결과값을** **반환하는** **시간**이 같으면 동기, 같지 않으면 비동기

```java
// 랜덤문자열 만들기 
public static String generateString(int size) {
        char[] randomStringArray = new char[size];
        IntStream.range(0, size).forEach(i -> randomStringArray[i] = (char) (Math.random() * 26 + 'A'));
        return new String(randomStringArray);
    }

// Math.random() 0 ~ 1.0 사이의 값 
// 26 알파벳 개수 
// 'A'는 아스키코드 대문자 알파벳 시작위치 65
// (char) 형변환 double형을 char형 변환하면 문자열을 얻음
```

## 

### mysql

```sql
// mysql timezone 확인하기
select @@system_time_zone, @@global.time_zone, @@session.time_zone; 
```



### 비트연산 

```java
// 해당bit에 CAR_CALL_BAN 값이 존재하면 != 0 
// 해당bit에 CAR_CALL_BAN == 0 값이 없는경우 
bit & PassengerStateBit.CAR_CALL_BAN  == 0 
```



- &~ 해서 기존꺼 빼고 |= 해서 새로운거 넣고



## Database

- 동일한 subject인경우 version 최신순으로 데이터 조회 할때 (CTE, rank() over(partiton by) 이용)

```sql
with target as (
  select *, rank() over(partition by subject order by version) rk from table 
)
select * from target where rk = 1;
```



- 데이터의 정합성을 위해서, unique_key 인덱스를 걸어줘야 한다. 

  - ```sql
     당연하지만, 인덱싱 순서도 중요함!
    ALTER TABLE `terms` 
    ADD UNIQUE INDEX `unique_key` (`subject` ASC, `version` ASC,) VISIBLE;
    ```

  - applicaiton단에서는 그에 맞는 Wrapping 해서 exception을 처리해야 한다. 

  

