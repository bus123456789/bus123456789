#define SSID        "123456"    //SSID Wifi
#define PASSWORD    "123456789"   //Pass Wifi
#define LINE_TOKEN  "VIebjRDroCMmpgj5iM02sa2RmGQPI8IoBUKElBloce3"    //Token ที่ได้จากการสมัคร ID Line

int waterlevel = 300;   //ปรับระดับน้ำ

void setup()
{
  Serial.begin(9600);
  Serial.println();
  Serial.println(LINE.getVersion());
  WiFi.begin(SSID, PASSWORD);
  Serial.printf("WiFi connecting to %s\n",  SSID);
  while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(400);
  }
  Serial.printf("\nWiFi connected\nIP : ");
  Serial.println(WiFi.localIP());

  // กำหนด Line Token
  LINE.setToken(LINE_TOKEN);
}

void loop()
{
  int val = analogRead(A1); // read input value
  Serial.print("Water Level :  ");
  Serial.println(val);
  delay(2000);

  if (val >= waterlevel) {
    Serial.println("Send Line");
    LINE.notify("น้ำล้นแล้วจ่า !!");
    while (val >= 200) delay(10);
  } else {

  }
}
