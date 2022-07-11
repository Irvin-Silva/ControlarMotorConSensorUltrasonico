# Sensor-Ultras-nico-con-motor-ARDUINO
Código hecho para Arduino en el cual se enciende un motor con un pulsador, y este se apaga SOLAMENTE cuando detecte una distancia entre 0 y 10 Cm. Y el motor enciende solamente cuanod se vuelve a precionar el pulsador. Útil cuando se quiere utilizar como sensor de movimiento

```
unsigned long startime;
int pinPulsadorM=8;
int pinMotorM=9;
int estadoPulsadorM=0;
int distancia;
int duracion;
int trig =10;
int eco =7;

void ultrasonico() {
    digitalWrite(trig, HIGH);
    delay(1);
    digitalWrite(trig, LOW);
    duracion = pulseIn(eco, HIGH);
    distancia = duracion/58.2;
    Serial.println(distancia);
}

void setup() {
    // put your setup code here, to run once:
    pinMode(pinPulsadorM, INPUT);
    pinMode(pinMotorM, OUTPUT);
    pinMode(trig, OUTPUT);
    pinMode(eco, INPUT);
    Serial.begin(9600);
}

void loop() {

    estadoPulsadorM = digitalRead(pinPulsadorM);
    if (millis() - startime > 1000) {
        ultrasonico();
        startime = millis();
    }

    if (estadoPulsadorM==HIGH)   {
        digitalWrite(pinMotorM, HIGH);
    }
  
    if (distancia >= 0 && distancia <= 10)  {   
        digitalWrite(pinMotorM, LOW);          // apago motor
    }
}
```
