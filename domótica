#include <LiquidCrystal.h>
//Inicializando variables y pines  
LiquidCrystal lcd(8, 9, 4, 5, 6, 7); 

const int pin3 = 3;
const int pin11 = 11;
const int pin13 = 13;
const int pin12 = 12;

int temperatura;
int ruido;
int botones;
int humedad;
const int sensor = A1;
int b1;

int control = 1;
int control_aire = 1;
int control_luz = 1;
int control_deshumidificador = 1;
int control_ruido = 1;

void setup(){  
  	//Setup lcd de 16 columnas, 2 filas
    lcd.begin(16,2); 
    lcd.setCursor(0,0); 
    lcd.print("PRESIONA UNA TECLA");   
	//Setup de los pines analógicos como input
    pinMode(A0, INPUT);
    pinMode(A1, INPUT);
    pinMode(A2, INPUT);
    pinMode(A3, INPUT);
    pinMode(A4, INPUT);
    //Setup de los pines digitales como output
  	pinMode(pin3, OUTPUT);
    pinMode(pin11, OUTPUT);
    pinMode(pin12, OUTPUT);
    pinMode(pin13, OUTPUT);

    Serial.begin(9600);
}  
  
void loop(){  
  	//Set el cursor inicial en el led a columna 0, fila 1
    lcd.setCursor(0,1); 
  	//Calcula los valores de temperatura, ruido, botones y humedad
  	//Con base en lectura de los pines analógicos
    b1 = int((float(analogRead(A1))*1/(1))/1);
    temperatura = ((b1^2)*0.01)+(0.18 * b1);
    ruido = analogRead(A3);
    botones = analogRead(A0);
  	humedad = analogRead(A4);
	
  	//Permite desactivar o activar sistemas separados o globales
  	//Si el botón global es presionado se desactivan todos los sistemas
  	//Si los botones individuales son presionados se desactiva solo ese sistema
    if (botones < 60) { 
        if(control==1){
            control=0;
            lcd.print("Sistema Desactivado");
          	digitalWrite(pin3, LOW);
            digitalWrite(pin11, LOW);
            digitalWrite(pin12, LOW);
            digitalWrite(pin13, LOW);
        }
        else{
            control=1;
            lcd.print("Sistema Activado");
        }
    }  
    else if (botones < 180) { 
        if(control_aire==1){
            control_aire=0;
            lcd.print("Aire Desactivado");
            digitalWrite(pin11, LOW);
        }
        else{
            control_aire=1;
            lcd.print("Aire Activado");
        }
    }  
    else if (botones < 380){ 
        if(control_luz==1){
            control_luz=0;
            lcd.print("Luces Desactivadas");
            digitalWrite(pin12, LOW);
        }
        else{
            control_luz=1;
            lcd.print("Luces Activadas");
        }
    }  
    else if (botones < 580){ 
        if(control_deshumidificador==1){
            control_deshumidificador=0;
            lcd.print("Deshumidificador Desactivado");
          	digitalWrite(pin3, LOW);
        }
        else{
            control_deshumidificador=1;
            lcd.print("Deshumidificador Activado");
        }
    }  
    else if (botones < 780){ 
        if(control_ruido==1){
            control_ruido=0;
            lcd.print("Bocinas Desactivadas");
            digitalWrite(pin13, LOW);
        }
        else{
            control_ruido=1;
            lcd.print("Bocinas Activadas");
        }
    }  
	
  	//Mientras el sistema global esté activo procede a verificar los controles individuales
    if (control == 1){  
        if (control_aire == 1){
          	//Si el control del AC está activo, verifica si la temperatura es mayor a 30°
          	//Si es mayor a 30° enciende el AC, de lo contrario lo apaga.
            if (temperatura > 30)  
            {
            digitalWrite(pin11, HIGH); 
            lcd.setCursor(0,0);
            lcd.print ("Temperatura Alta");
            lcd.setCursor(0,1);           
            lcd.print("Aire Encendido");
            }
            else
            {
            digitalWrite(pin11, LOW);
            lcd.clear();
            }
        }
        
        if (control_luz == 1){
          	//Si el control de las lámparas está activo, verifica si la luz es muy baja
          	//Si la luz ambiental es baja, enciende la lámpara, de lo contrario la apaga.
            int analogValue1 = analogRead(A2);
            if (analogValue1 < 100)
            {
            lcd.setCursor(0,0);
            lcd.print ("Poca Luz");
            lcd.setCursor(0,1);           
            lcd.print("Lamparas Encendidas");
            digitalWrite(pin12, HIGH);
            }
          	else
            {
            digitalWrite(pin12, LOW);
            }
        }
      
      	if (control_deshumidificador == 1){
          	//Si el control del deshumidificador está activo, verifica si la humedad es mayor al 50%
          	//Si es mayor al 50% enciende el deshumidificador, de lo contrario lo apaga.
            if (humedad > 488)
            {
              digitalWrite(pin3, HIGH); 
              lcd.setCursor(0,0);
              lcd.print ("Humedad Alta");
              lcd.setCursor(0,1);           
              lcd.print("Deshumidificador Encendido");
            }
            else
            {
              digitalWrite(pin3, LOW);
              lcd.clear();
            }
      	}
        
        if (control_ruido == 1){
          	//Si el control del ruido está activo, verifica si el ruido es muy alto.
          	//El sensor de ruido está simulado con un potenciómetro
          	//Si es mayor a la mitad del potenciómetro (arriba de 80dB), de lo contrario lo apaga.
            if (ruido > 511)
            {
            digitalWrite(pin13, HIGH); 
            lcd.setCursor(0,0);
            lcd.print ("Ruido Alto");
            lcd.setCursor(0,1);           
            lcd.print("Bocinas Encendidas");
            }
            else
            {
            digitalWrite(pin13, LOW);
            lcd.clear();
            }
        }
    }
  	//Espera 250 ms para volver a repetir el loop
    delay(250);
}
