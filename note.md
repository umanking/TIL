

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

