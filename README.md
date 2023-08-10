# IOT TASK 1
#include <WiFi.h>
#include <HTTPClient.h>

const char* ssid = "Wokwi-GUEST";
const char* password = "";

//const String url = "https://s-m.com.sa/smtc/test/hbvfd/retrieve.php";
const String url = "https://s-m.com.sa/f.html";


String payload = "";
void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  pinMode(25, OUTPUT);//forward
  pinMode(27, OUTPUT);//backward
  pinMode(14, OUTPUT);//right
  pinMode(12, OUTPUT);//left
  Serial.print("Connecting to WiFi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.print("OK! IP=");
  Serial.println(WiFi.localIP());

  Serial.print("Fetching " + url +"... ");

  


}

void loop() {
  HTTPClient http;
  http.begin(url);

  int httpResponseCode = http.GET();
  if (httpResponseCode > 0) {
    Serial.print("HTTP ");
    Serial.println(httpResponseCode);
    payload = http.getString();
    Serial.println();
    Serial.println(payload);
    
    if( payload == "stop" ){
      digitalWrite(25, LOW);
      digitalWrite(14, LOW);
      digitalWrite(27, LOW);
      digitalWrite(12, LOW);

    }
    if( payload == "forward" ){
      digitalWrite(25, HIGH);
    }
     if( payload == "right" ){
      digitalWrite(14, HIGH);
    }
    if( payload == "backward" ){
      digitalWrite(27, HIGH);
    }
    if( payload == "left" ){
      digitalWrite(12, HIGH);
    }
  }
  else {
    Serial.print("Error code: ");
    Serial.println(httpResponseCode);
    Serial.println(":-(");
  }
  
}
![المهمه الأولى ](https://github.com/rahafasiri/IOT-Task1/assets/139389205/9233345e-6924-4c92-8e12-1809b108a70d)
![المهمه الأولى 1](https://github.com/rahafasiri/IOT-Task1/assets/139389205/9b3f2420-06cf-45e5-872c-bff5e4bdfa6e)

