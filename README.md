# jarakaman
<img src="https://drive.google.com/drive/u/1/folders/1aVLeB6GBu-x0q52QX4aV5CMIfvsI9uD_">
Ultrasonic.ino

    #include <Wire.h>
    #include <LCD.h>
    #include <LiquidCrystal_I2C.h>
    LiquidCrystal_I2C lcd(0x27, 2, 1, 0, 4, 5, 6, 7, 3, POSITIVE); // Addr, En, Rw, Rs, d4, d5, d6, d7, backlighpin, polaritydCrystal_I2C lcd(0x3F, 2, 1, 0, 4, 5, 6, 7, 3, POSITIVE);
    /*-----------------------------------------------------
    '     
    '     TRIG --> Pin 7
    '     ECHO --> Pin 6
    '     Baud Rate 9600 bps
    '     Ogi sinatra
    '     AT-MO PRODUCTION
    '-----------------------------------------------------*/

    //pin Ultrasonik
    #define trigPin 7
    #define echoPin 6

    #define ledAman 8
    #define led1 9
    #define led2 10
    #define led3 11



    void setup() {
      Wire.begin();
      lcd.begin(16,2);
      lcd.backlight();
      lcd.setCursor(0, 0);
      lcd.print("Jarak Aman");
      lcd.setCursor(0, 1);
      lcd.print("Mobil JAVSOUL");
      Serial.begin (9600);
      pinMode(trigPin, OUTPUT);
      pinMode(echoPin, INPUT);
      pinMode(ledAman, OUTPUT);
      pinMode(led1, OUTPUT);
      pinMode(led2, OUTPUT);
      pinMode(led3, OUTPUT);

    }

    void loop() {

      long duration, distance;
      digitalWrite(trigPin, LOW); 
      delayMicroseconds(2);
      digitalWrite(trigPin, HIGH);
      delayMicroseconds(10);
      digitalWrite(trigPin, LOW);
      duration = pulseIn(echoPin, HIGH);
      distance = (duration/2) / 29.1;


      if (distance >= 50) 
      {
        digitalWrite(ledAman, HIGH);
          digitalWrite(led1, LOW);
          digitalWrite(led2, LOW);
          digitalWrite(led3,LOW);
          lcd.clear();
          lcd.setCursor(0, 0);
          lcd.print("   MOBIL DALAM");
          lcd.setCursor(0, 1);
          lcd.print("   JARAK AMAN");      
      }
      if (distance <= 40) 
      {
          digitalWrite(ledAman, LOW);
          digitalWrite(led1, HIGH);
          digitalWrite(led2, LOW);
          digitalWrite(led3,LOW);
          lcd.clear();
          lcd.setCursor(0, 0);
          lcd.print("   MOBIL DALAM");
          lcd.setCursor(0, 1);
          lcd.print(" JARAK WASPADA");
      }

      if (distance < 30) {
          digitalWrite(ledAman, LOW);
          digitalWrite(led2, HIGH);
          digitalWrite(led1, LOW);
          digitalWrite(led3,LOW);      
          lcd.clear();
          lcd.setCursor(0, 0);
          lcd.print("   MOBIL DALAM");
          lcd.setCursor(0, 1);
          lcd.print("  JARAK BAHAYA");      
      }

      if (distance < 20) {
        digitalWrite(ledAman, LOW);
        digitalWrite(led3, HIGH);
        digitalWrite(led2, LOW);
        digitalWrite(led1, LOW);
        lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print(" MOBIL ANDA AKAN ");
        lcd.setCursor(0, 1);
        lcd.print("   MENABRAK!!");
    } 

      delay(1000);
    }
