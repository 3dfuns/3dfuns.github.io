---
layout: single
text-decoration: none
title:  "Arduino - ESP32C3 Wifi Tank"
---

***
Xiao ESP32C를 이용한 Wifi Tank Code입니다.
IP ⚔️ 192.168.4.1 : 9876 로 접속하면 됩니다. 

#### 🔨 기본
```cpp
// IP --> 192.168.4.1 : 80  --> 기본 값
// IP --> 192.168.4.1 : 23  --> 현재 값

#include <WiFi.h>
#include "ESP32_C3_ISR_Servo.h"    // esp32c3 dev module로 board 선택

#define D0 2   // xiao esp32c3 입출력 핀 재정의
#define D4 6
#define D5 7
#define D8 8

// Replace with your network credentials
const char* ssid     = "ESP32-Access-Point";
const char* password = "123456789";
const int port = 9876;

const int ledPin = D0;

int servoIndex1  = -1;
int servoIndex2  = -1;

// Set web server port number to 80
WiFiServer server(port);
WiFiClient client;

char cmd[100];
int cmdIndex;
unsigned long lastCmdTime = 600000;
unsigned long alivesentTime = 0;
uint8_t ledState;

void setup() {
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin,LOW);

  ESP32_ISR_Servos.useTimer(1);
  servoIndex1 = ESP32_ISR_Servos.setupServo(D4, 550, 2350);
  servoIndex2 = ESP32_ISR_Servos.setupServo(D5, 550, 2350);

  ESP32_ISR_Servos.setPosition(servoIndex1, 90);
  ESP32_ISR_Servos.setPosition(servoIndex2, 90);

  cmdIndex = 0;

  WiFi.softAP(ssid, password);
  IPAddress IP = WiFi.softAPIP();
  
  server.begin();
}

void loop(){
  if(!client.connected()) {
  client = server.available();
  return;
  }

  if(client.available()) {
    char c = (char)client.read();

    if(c == '\n') {
      cmd[cmdIndex] = 0;
      Serial.println(cmd);
      exeCmd();
      cmdIndex = 0;     
    }
    else {
      cmd[cmdIndex] = c;
      if(cmdIndex < 99) cmdIndex++;
    }
  }
}

void exeCmd() {
  lastCmdTime = millis();

  if(cmdStartsWith("W")) {
  ledState = (ledState == LOW) ? HIGH: LOW;
  digitalWrite(ledPin,ledState);
  }

  if(cmdStartsWith("f")) {
    ESP32_ISR_Servos.setPosition(servoIndex1, 0);
    ESP32_ISR_Servos.setPosition(servoIndex2, 180);
  }
  if(cmdStartsWith("b")) {
    ESP32_ISR_Servos.setPosition(servoIndex1, 180);
    ESP32_ISR_Servos.setPosition(servoIndex2, 0);
  }
  if(cmdStartsWith("l")) {
    ESP32_ISR_Servos.setPosition(servoIndex1, 0);
    ESP32_ISR_Servos.setPosition(servoIndex2, 0);
  }
  if(cmdStartsWith("r")) {
    ESP32_ISR_Servos.setPosition(servoIndex1, 180);
    ESP32_ISR_Servos.setPosition(servoIndex2, 180);
  }
  if(cmdStartsWith("s")) {
    ESP32_ISR_Servos.setPosition(servoIndex1, 90);
    ESP32_ISR_Servos.setPosition(servoIndex2, 90);
  }
}

boolean cmdStartsWith(const char *st) {
  for(int i = 0; ; i++) {
    if(st[i] == 0) return true;
    if(cmd[i] == 0) return false;
    if(cmd[i] !=st[i]) return false;    
  }
  return false;
}
```
  ❓ 휴대폰 App은 Roboremo를 이용하여 구동하였습니다.

#### 👉 참고 사이트
- <a href="https://www.roboremo.app/">RoboRemo</a>

누구나 쉽게 이해할 수 있도록 만들고 있습니다. 수정될 부분이 있다면 연락주십시요.  
{: .notice--info}

***

[TOP](#){: .btn .btn--primary }{: .align-right}
