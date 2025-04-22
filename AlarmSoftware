/* Home Security Alarm by William Lam
 *
 * The goal of my project is to build as a simple low-cost intruder alarm for students living in apartments.
 * When activated, my circuit will provide a warning light at intruders that crack open the door. If the intruder continues further,
 * a siren will begin to alarm as well as the light flashing to draw attention. However, if a user accidentally activates
 * the alarm, they may enter a pass code with push buttons to disarm the system. In this proof of concept, I will be using a red LED and
 * WT-1205 buzzer, but this model can be easily transfered to larger applications for homes and businesses.
 */

//Here I will declare the pins I plan to use with my sensors for input(Ultrasonic Sensor[microphone] and Pushbutton)
//and output (Ultrasonic Sensor [Speaker]LED and Speaker).


const int trigPin = 10; //Sent signal by ultrasonic sensor
const int echoPin = 9; //Recieved signal by ultrasonic sensor

void setup() {

  //Ultrasonic Sensor
  pinMode(echoPin, INPUT);
  pinMode(trigPin, OUTPUT);

  //INPUTS
  pinMode(6, INPUT); //Pushbutton 1
  pinMode(4, INPUT); //PushButton 2
  pinMode(5, INPUT); //PushButton 3

  //OUTPUTS
  pinMode(8, OUTPUT); //LED
  pinMode(7, OUTPUT); //Speaker

  //Sets the bit rate at 9600 bits per second for data communication
  Serial.begin(9600);
  
}

// gathers the distance of the ultrasonic sensor.

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH);
  float distance = duration * 0.034/2; // time * speed of sound/2 = distance

  Serial.print("Distance: ");
  Serial.println(distance);


  //This provides the first warning light for the intruder

  if (distance < 50)
  {
    digitalWrite(8, HIGH);  
  }
  if (distance < 20) //If the intruder continues, the alarm and flashing light begins
  {
    while (true)
    {
      digitalWrite(8, LOW);
      for (int i = 400; i < 600; ++i) //This sets the low to high pitch on the buzzer
      {
        for (int j = 10; j > 1; --j)
          {
          tone(7, i);
          }
      if ((digitalRead(6)) == LOW) //If user wishes to exit, the first requirement to turn off alarm (hold pushbutton 1)
        {
          if (digitalRead(5) == LOW) //Second requirement to turn off alarm (tap pushbutton 3)
          {
            digitalWrite(8, LOW);
            digitalWrite(7, LOW);
            exit(0);
          }
        }
      }
      digitalWrite(8, HIGH); //This is the code to flash the light on
      delay(100);
      digitalWrite(8, LOW); //This is the code to flash the light off
    }
  }
}
