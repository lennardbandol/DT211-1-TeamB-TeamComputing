#pragma config(Sensor, S1,     lightsensor,    sensorLightActive)
#pragma config(Sensor, S4,     touchsensor,    sensorTouch)
#pragma config(Motor,  motorA,          rightmotor,    tmotorNXT, PIDControl, encoder)
#pragma config(Motor,  motorB,          leftmotor,     tmotorNXT, PIDControl, encoder)
//*!!Code automatically generated by 'ROBOTC' configuration wizard               !!*//

/* Team computing Assignment */

//declaring global variables 
int lightValue;
int darkValue;
int sumValue;
int thresholdValue;
int countValue = 0;
int lastSeen;

//function prototype
void turnleft( int speed );
void forward( int speed );
void turnright( int speed );
void forwardlines();
void findthreshold();

task main()
{
	int speed = 40;

	forwardlines();
	turnleft();
	forwardlines();
	turnright();
}

//function to turn left
void turnleft( int speed )
{
	
	nMotorEncoder[rightmotor] = 0;
	while(nMotorEncoder[rightmotor] < 160)
	{
		motor[leftmotor] = -speed;
		motor[rightmotor] = speed;
	}
	
	motor[rightmotor] = 0;
	motor[leftmotor] = 0;
	
}

//function to turn right
void turnright( int speed )
{
	
	nMotorEncoder[rightmotor] = 0;
	while(nMotorEncoder[rightmotor] < 160)
	{
		motor[leftmotor] = -50;
		motor[rightmotor] = 50;
	}
	
	motor[rightmotor] = 0;
	motor[leftmotor] = 0;
	
}

//unfinished function
void forward( int speed )
{
	
	
	nMotorEncoder[rightmotor] = 0;
	while(nMotorEncoder[rightmotor] < 230)
	{
		motor[leftmotor] = speed;
		motor[rightmotor] = speed;
	}

		motor[rightmotor] = 0;
		motor[leftmotor] = 0;
}

//function to move forward
void forwardlines()
{
	lastSeen = 1;
	countValue = 0;
	
	while(countValue < 3 )
	{
		nxtDisplayStringAt(0,31,"light value %d", SensorValue(lightsensor));
		nxtDisplayStringAt(1,10,"countvalue %d", countValue);
		motor[rightmotor] = 30;
		motor[leftmotor] = 30;
		
		if(SensorValue(lightsensor) < 37)
		{
			if(lastSeen == 1)
			{
				countValue = countValue + 1;
				lastSeen = 0;
			}
		}
		else
		{
			lastSeen = 1;
		}
	}
}

//function to find the threshold values.
void findthreshold()
{
	
	while(SensorValue(touchsensor) == 0)
  {
    nxtDisplayStringAt(0,31,"Read Light Now");
  }

  lightValue = SensorValue(lightsensor);

  wait1Msec(1000);

  while(SensorValue(touchsensor) == 0)
  {
    nxtDisplayStringAt(0,31,"Read Dark Now");
  }

  darkValue = SensorValue(lightsensor);

  sumValue = lightValue + darkValue;
  thresholdValue = sumValue/2;

}


	
