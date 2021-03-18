# HaziqHakimie
DE97624 Arduino Uno Texting Angela
// include the LiquidCrystal library
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

#define start 13



int x = 0;
char direction = 'L';
boolean game = 0;
int a = 0,b=0;
float dis=0;
double temp,sensor;
int gas = 0;
float sensorG;




void Greeting(){

  lcd.begin(16, 2);				
  lcd.setCursor(2, 0);
  lcd.print("Hello");
  delay(1000);
  lcd.clear();
  lcd.setCursor(3, 0);
  lcd.print("konnichiwa");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Ya hallo");
  lcd.setCursor(2,2);
  lcd.print("Angela Here!");
  delay(4000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Developed by:");
  lcd.setCursor(b, 1);
  lcd.print("Haziq Hakimi");
  delay(3000);
  
  

}




void setup() {

  

  pinMode(start, INPUT);
  Greeting();//greet User
  Serial.begin(9600);//troubleshoot
  
}


void loop() {

  //executes this while loop untill start button is pressed
  while (game == 0) {
    for (a; a < 1; a++) {
      
      lcd.clear();
      lcd.setCursor(3, 0);
      lcd.print("Press start");
      lcd.setCursor(3, 1);
      lcd.print("button   ->");
    }

    // check whether the start button is pressed
    if (digitalRead(start) == HIGH) {
     
      for (int i = 3; i > 0; i--) {
        lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("Let me hold you");
        lcd.setCursor(8, 1);
        lcd.print(i);
        delay(1000);
      }
      a = 0;
      game = 1;							
    }
    delay(100);
    }

  
  
  
  //-----Game to begin-----
  
  
    //for Distance sensing
    dis = GiveDis(8,7);
    
      if(dis > 150)
    {
        Far();//far output
    

 
  }else{
    Close();//Close Output
  	
  }
  delay(4000);

  
   
//temp sensing calculation
  sensor = analogRead(A2);
  temp = (sensor-20)*3.04;
  temp = map(temp,0,1023,-40,125);
  
  TempCond();//temp condition
  delay(4000);
  
  
  //Gas sensing
  sensorG = analogRead(A0);
  Smoking();
  delay(4000);
  game = 0 
  
  
  Serial.println(sensorG);//troubleshooting
  delay(100);
  


}

 
void Far (){

  	lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Did i make");
    lcd.setCursor(4,1);
    lcd.print("you mad?");
    delay(4000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("why are you ");
    lcd.setCursor(0,1);
    lcd.print("distance with me.");
     delay(2000);




}

void Close(){

lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Did i make");
    lcd.setCursor(4,1);
    lcd.print("you miss me?");
    delay(4000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("why so close");  
    lcd.setCursor(5,1);
    lcd.print("(^-^) ");
    delay(2000);





}


void TempCond(){

if(temp >37.6){
    lcd.clear();
  	lcd.setCursor(0,0);
    lcd.print("I got a fever");  
    lcd.setCursor(5,1);
    lcd.print("(@.@) ");
    delay(1000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Stay with");
    lcd.setCursor(0,1);
    lcd.print("me please");
    delay(4000);
  }
  else{
    lcd.clear();
  	lcd.setCursor(0,0);
    lcd.print("I'm cold");
    lcd.setCursor(1,1);
    lcd.print("Can you hug me");
    delay(4000);
  
  }


}






void Smoking(){


if(sensorG >=200){
    
  	lcd.clear();
  	lcd.setCursor(4,0);
    lcd.print("Wait!!!!!");
    delay(2000);
    lcd.setCursor(0,0);
    lcd.print("Are you smoking?");
    delay(2000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("i'm mad at you");
    delay(3000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Dont find me");
    delay(3000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("untill you ");
    delay(3000);
    lcd.clear();
    lcd.setCursor(0,1);
    lcd.print("stop smoking");
    delay(3000);
   
  }
  else{
  
  	lcd.clear();
  	lcd.setCursor(4,0);
    lcd.print("hey baby");
    delay(1000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("you not smoking");
    delay(1000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("hihih~");
    delay(1000);
    lcd.clear();
    lcd.setCursor(4,0);
    lcd.print("LOVE YOU!!");
    delay(4000);
  
  
  }





}
//Distance sensing
float GiveDis(int trig, int echo){
	pinMode(trig,OUTPUT);
  	digitalWrite(trig,LOW);
  	delayMicroseconds(12);
  	digitalWrite(trig,HIGH);
  	delayMicroseconds(10);
  	digitalWrite(trig,LOW);
  	pinMode(echo,INPUT);
  	return pulseIn(echo,HIGH,30000)/58.0;
}

