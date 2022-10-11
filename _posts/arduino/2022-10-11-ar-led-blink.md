---
layout: single
title:  "Arduino - LED를 다양한 방법으로 깜빡이기"
---

***
Arduino를 이용하여 LED를 다양한 방법으로 깜빡이는 예제  
Arduino는 3.3V 또는 5V를 사용합니다. LED 연결시 <img width="24" alt="star1" src="https://user-images.githubusercontent.com/78655692/151471925-e5f35751-d4b9-416b-b41d-a059267a09e3.png"><span style="background-color:#FF778899">저항값 100~330Ω </span>  
정도의 저항을 같이 연결하여 주십시요.

#### 🔨 기본
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

#### 🔨 함수 만들기
```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  function();
}

void function() {
  digitalWrite(LED_BUILTIN, HIGH);   
  delay(1000);                       
  digitalWrite(LED_BUILTIN, LOW);    
  delay(1000); 
```

#### 🔨 delay함수 없이 깜빡이기
```cpp
const int ledPin =  LED_BUILTIN;
int ledState = LOW;            
unsigned long previousMillis = 0;    
const long interval = 1000;          

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  unsigned long currentMillis = millis();

  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    
    if (ledState == LOW) {
      ledState = HIGH;
    } else {
      ledState = LOW;
    }
    digitalWrite(ledPin, ledState);
  }
}
```

#### 👉 참고 사이트
- <a href="https://docs.arduino.cc/built-in-examples/basics/Blink#hardware-required">아두이노 사이트</a>

누구나 쉽게 할 수 있도록 만들고 있습니다. 수정될 부분이 있다면 연락주십시요.  
**Email : jh.choi@fixnmax.com**
{: .notice--info}

***

[TOP](#){: .btn .btn--primary }{: .align-right}
