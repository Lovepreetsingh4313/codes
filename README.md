# codes

#include <iobb.h> // Library to access GPIO of Beaglebone
#include <time.h>  //Time Library
#include <stdio.h> // Standard IO library
#include <unistd.h>

long int start, stop, count; // Variables to store values

clock_t before, end, difference; // To store Time of UltraSonic Sensor

int cflag = 1; // Flag to stabilize count
int cflag1 = 1; // Flag to stabilize count
int personCount = 0;

int main(void)
{
  iolib_init();  // Initialize the IOBB Library
  iolib_setdir(8, 10, DigitalOut);  // Setting Pin 10 or Port 8 as Output for Sensor -1
  iolib_setdir(8, 9, DigitalIn);    // Setting Pin 9 or Port 8 as Inputfor Sensor -1

  printf("STARTED \n");
  iolib_delay_ms(500); // Small Delay



  while(1)
  {
    pin_high(8, 10);  // Trigger Ultrasonic Sensor
    usleep(10);
    pin_low(8, 10);

    
    while(is_low(8, 9))  // Wait until Echo Pulse starts
    {
			count+= 1;
			before = clock(); //Current Clock Time

	}

	while(is_high(8, 9)) // Wait and store Echo pulse time
	{
		count += 0;
		end = clock();

	}

    difference = end - before; // Get Absolute time of Echo Pulse


    difference = difference/30; // Get a rough value in centimeters
    printf("Distance for entry : %d cm. \n",difference);


  }
  iolib_free();
  return(0);
  }
