# human-follower-smart-trolley
A small trolley, which detects the presence of the user and then detects the user position and follows it.
RFID ACCESS CODE: 
#include <SPI.h> 
#include <MFRC522.h> 
#define SS_PIN 10 
#define RST_PIN 9 
MFRC522 mfrc522(SS_PIN, RST_PIN); 
void setup() 
{ 
Serial.begin(9600); 
SPI.begin(); 
mfrc522.PCD_Init();
Serial.println("Scan the card to be accessed...");
Serial.println();
} 
void loop()
{ 
// Look for new cards if ( ! mfrc522.PICC_IsNewCardPresent()) 
{
return;
} 
// Select one of the cards 
if ( ! mfrc522.PICC_ReadCardSerial()) 
{
return;
} 
//Show UID on serial monitor
Serial.print("UID tag :");
String content= ""; 
byte letter; 
for (byte i = 0; i < mfrc522.uid.size; i++) 
{
Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
Serial.print(mfrc522.uid.uidByte[i], HEX);
content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ")); 
content.concat(String(mfrc522.uid.uidByte[i], HEX)); 
} 
Serial.println(); 
Serial.print("Message : "); 
content.toUpperCase();
if (content.substring(1) == "----------------------") // enter the UID of the tag 
{
Serial.println("Authorized access");
Serial.println(); 
// if required we can add led blink 
delay(3000); 
}
else 
{ 
Serial.println(" Access denied") // can add buzzer 
delay(3000);
}
}
