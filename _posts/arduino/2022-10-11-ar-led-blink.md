---
layout: single
title:  "Arduino - LED 다양한 방법으로 깜빡이기"
---

***
Arduino를 이용하여 LED를 깜빡이는 방법입니다.  
Arduino는 3.3V 또는 5V를 사용합니다. LED 연결시 <img width="12" alt="star1" src="https://user-images.githubusercontent.com/78655692/151471925-e5f35751-d4b9-416b-b41d-a059267a09e3.png"><span style="background-color:yellow">저항값 100~330Ω </span>  
정도의 저항을 같이 연결하여 주십시요.

#### 🔨 기본 예시 
```cpp
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

#### 👉 참고 사이트
- <a href="naver.com">아두이노 사이트</a>
- <a href="naver.com">유튜브</a>
{: .notice--info}
***

[TOP](#){: .btn .btn--primary }{: .align-right}
