---
layout: single
title:  "Arduino - LED 깜빡이기"
---

Arduino를 이용하여 LED를 깜빡이는 방법입니다.

Arduino는 5V 또는 3.3V를 사용합니다. LED 연결시 <span style="background-color:yellow">저항값 100~330Ω </span>
정도의 저항을 같이 연결하여 주십시요.

### 🔨 `기본` 예시 
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

### 👉 참고 사이트

- [아두이노 사이트](https://modoocode.com/66)
- [유튜브](https://www.inflearn.com/course/following-c/dashboard)  
{: .notice--warning}



***
[TOP](#){: .btn .btn--primary }{: .align-right}
