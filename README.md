SerialSMS by Meir Michanie
meirm@riunx.com
Released under GPL3

Modified for ease of use by Farzeen
farseenabdulsalam@gmail.com

SerialSMS is a library for arduino to be used with a GPRS/GSM shield.
In fact, it can be used with a GSM Module without a shield.
If you have TTL interface on your module, connect it to your arduino digital
pins and you are done.
If you only have RS232 interface, you will have to convert it to TTL
using a MAX232 or similar IC. Then connect the TTL rx and tx to arduino.

The library allows you to send/receive SMS with simple calls.

Install:
========

	* Create a folder named "SerialGSM" under libraries.
	* Copy the content of this repository into it.



Samples: (NOTE: The following interface is going to be changed)
========
Attention: I will be reworking the API for readability and ease of use.
If you want to continue using the below API, please use original
SerialSMS by Meir Michanie: https://github.com/meirm/SerialGSM
This sample section will be removed as soon as the rework is completed

Sample program to receive SMS for parsing:

//############### ReceiveSMS ############


	#include <SerialGSM.h>
	#include <SoftwareSerial.h>
	SerialGSM cell(2,3);

	boolean sendonce=true;
	void setup(){
	  Serial.begin(9600);
	  cell.begin(9600);
	  cell.Verbose(true);
	  cell.Boot();
	  cell.DeleteAllSMS();
	  cell.FwdSMS2Serial();
	 }


	void loop(){
	  if (cell.ReceiveSMS()){
		 Serial.print("Sender: ");
		 Serial.println(cell.Sender());
		 Serial.print("message: ");
		 Serial.println(cell.Message());
		 cell.DeleteAllSMS();
	  }
	}

//#######################################


Sample program demostrating how to send a SMS.


//############### SendSMS ################

	#include <SerialGSM.h>
	#include <SoftwareSerial.h>
	SerialGSM cell(2,3);
	void setup(){
	 Serial.begin(9600);
	 cell.begin(9600);
	  cell.Verbose(true);
	  cell.Boot();
	  cell.FwdSMS2Serial();
	  cell.Rcpt("+972123456789");
	  cell.Message("hello world");
	  cell.SendSMS();
	}


	void loop(){
	  if (cell.ReceiveSMS()){
	    Serial.println(cell.Message());
	    cell.DeleteAllSMS();
	  }

	}

//####################################
