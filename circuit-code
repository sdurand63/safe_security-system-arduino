// Include necessary libraries
#include <Keypad.h>
#include <stdlib.h>


// LED declarations
const int led1 = 13; // red
const int led2 = 12;
const int led3 = 11;
const int led4 = 10;
const int led5 = 9; // green - card reader
const int led6 = 15; // MA1
const int led7 = 16; // MA2
const int led8 = 17; // MA3
const int led9 = 18; // MA4
const int led10 = 19; // blue - safe open

//						----------KEYPAD----------
// Keypad creation
const byte ROWS = 4; // four rows
const byte COLS = 3; // three columns
char keys[ROWS][COLS] = {
  {'1','2','3'},
  {'4','5','6'},
  {'7','8','9'},
  {'*','0','#'}
};

// Declaration of row and column pins for the keypad
byte rowPins[ROWS] = {7, 6, 5, 4};
byte colPins[COLS] = {3, 2, 8}; 
Keypad keypad = Keypad( makeKeymap(keys), rowPins, colPins, ROWS, COLS );

//						----------KEYPAD----------

//				 ---------Security Levels----------
bool validation = false;
//				 ---------Security Levels----------

// Variables used in multiple authentication methods
int compteur = 0;
int compteur_erreur = 0;

//						----------MA1----------
bool MA1_valide = false;
//  					----------MA1----------

// 						----------MA2----------
bool MA2_valide = false;
//						----------MA2-----------

//						----------MA3-----------
bool MA3_valide = false;
//						----------MA3-----------

//						----------MA4-----------
bool MA4_valide = false;
//						----------MA4-----------




void setup()
{
  Serial.begin(9600);
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT); 
  pinMode(led5, OUTPUT); 
  pinMode(led6, OUTPUT);
  pinMode(led7, OUTPUT);
  pinMode(led8, OUTPUT);
  pinMode(led9, OUTPUT);
  pinMode(led10, OUTPUT);

  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  digitalWrite(led5, LOW);
  digitalWrite(led6, LOW);
  digitalWrite(led7, LOW);
  digitalWrite(led8, LOW);
  digitalWrite(led9, LOW);
  digitalWrite(led10, LOW);
}



void loop()
{
  double tension = analogRead(A0); // Read output voltage
  tension /= 204; // Convert to correspond to our voltage values in volts
  
  if (tension > 0.86 && tension < 0.90){
	digitalWrite(led5, HIGH);
    Serial.print("\n\> First level passed, continuing authentication... \n\n");
    niveau4();
    if (validation == true){
      coffre_ouvert();
    }
  }

  else if (tension > 1.50 && tension < 1.54){
    digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau2();
    if (validation == true){
      coffre_ouvert();
    }
  }

  else if (tension > 1.89 && tension < 1.93){
	digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau4();
    if (validation == true){
      coffre_ouvert();
    }
  }

  else if (tension > 2.33 && tension < 2.37){
	digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau2();
    if (validation == true){
      coffre_ouvert();
    }
  }

  else if (tension > 2.53 && tension < 2.57){
	digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau4();
    if (validation == true){
      coffre_ouvert();
    }
  }

  else if (tension > 2.71 && tension < 2.75){
	digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau3();
    if (validation == true){
      coffre_ouvert();
	}
  }

  else if (tension > 3.07 && tension < 3.11){
	digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau2();
    if (validation == true){
      coffre_ouvert();
	}
  }

  else if (tension > 3.38 && tension < 3.42){
	digitalWrite(led5, HIGH);
    Serial.print("\n\n> First level passed, continuing authentication... \n\n");
    niveau1();
    if (validation == true){
      coffre_ouvert();
	}
  }         
  
  else 
   {
     Serial.print("\n> Error, incorrect voltage \n");
     delay(8000);
   }
  
}

// 				----------Creation of authentication methods----------

void MA1()
{
  delay(2000);
  const char question1[] = {"What is your dog's first name?"};
  const char question2[] = {"In what year was America discovered?"};
  const char question3[] = {"What is your mother-in-law's first name?"};
  const char question4[] = {"What grade did you get on your philosophy exam?"};

  const char reponses1[] = {"1. Nesquick  2. Thibou  3. Thiago  4. Wilson"};
  const char reponses2[] = {"1. 1492  2. 1501  3. 1486  4. 1481"};
  const char reponses3[] = {"1. Sylvie  2. Michelle  3. Germaine  4. Jacqueline"};
  const char reponses4[] = {"1. 8/20  2. 18/20  3. 11/20  4. 14/20"};

  const char indice_bonne_rep[] = {'3', '1', '2', '1'};
  char indice_rep[] = {'0', '0', '0', '0'};
  bool bonne_rep[] = {false, false, false, false};
  
  compteur = 1;
  if (compteur == 1)
  {
    while(bonne_rep[0] == false) {
      Serial.println(question1); // Display the question
      delay(500);
      Serial.println(reponses1); // Display the answers
      char key = keypad.getKey();
      
      while(bonne_rep[0] == false){
      key = keypad.getKey(); // Get the answer
      if (key != NO_KEY){  
        indice_rep[0] = key; // Store the answer
        bonne_rep[0] = true;

      }
      }
    // Compare answers for validation              
	    if (indice_bonne_rep[0] != indice_rep[0]) { 
          Serial.print("Wrong answer \n\n");  
          delay(1000);
          compteur_erreur++; // Increment error counter
          bonne_rep[0] = false; // Reset correct answer to false
       
        }
        else {
         Serial.print("Correct answer \n\n");
         compteur++;
         digitalWrite(led1, HIGH); // Turn on corresponding LED
         delay(1000);
        }
      	if (compteur_erreur == 4)
  		{
    		Serial.println("4 errors, locked for 30 seconds."); 
    		digitalWrite(led1, LOW);
 			digitalWrite(led2, LOW);
  			digitalWrite(led3, LOW);
  			digitalWrite(led4, LOW);
            delay(30000); // Lock the keypad for 30 seconds
          	compteur = 1; // Return to first question
    		compteur_erreur = 0; // Reset error counter to 0
            break;
  		}
    }
  } 
  
  
  if (compteur == 2)
  {
    while(bonne_rep[1] == false){
      Serial.println(question2);
      delay(500);
      Serial.println(reponses2);
      char key = keypad.getKey();
      
      while(bonne_rep[1] == false){
      key = keypad.getKey();
      if (key != NO_KEY){  
        indice_rep[1] = key;
        bonne_rep[1] = true;
      }
      }
            
	    if (indice_bonne_rep[1] != indice_rep[1]) {
          Serial.print("Wrong answer \n\n");
          delay(1000);
          compteur_erreur++;
          bonne_rep[1] = false;
        }
        else {
         Serial.print("Correct answer \n\n");
         compteur++;
         digitalWrite(led2, HIGH);
         delay(1000);
        }
      	if (compteur_erreur == 4)
  		{
    		Serial.println("4 errors, locked for 30 seconds.");
            digitalWrite(led1, LOW);
 			digitalWrite(led2, LOW);
  			digitalWrite(led3, LOW);
  			digitalWrite(led4, LOW);
    		delay(30000);
          	compteur = 1;
    		compteur_erreur = 0;
            break;
  		}
    }
    }
  
  if (compteur == 3)
  {
    while(bonne_rep[2] == false){
      Serial.println(question3);
      delay(500);
      Serial.println(reponses3);
      char key = keypad.getKey();
      
      while(bonne_rep[2] == false){
      key = keypad.getKey();
      if (key != NO_KEY){  
        indice_rep[2] = key;
        bonne_rep[2] = true;
      }
      }
            
	    if (indice_bonne_rep[2] != indice_rep[2]) {
          Serial.print("Wrong answer \n\n");
          delay(1000);
          compteur_erreur++;
          bonne_rep[2] = false;
        }
        else {
         Serial.print("Correct answer \n\n");
         compteur++;
         digitalWrite(led3, HIGH);
         delay(1000);
        }
      	if (compteur_erreur == 4)
  		{
    		Serial.println("4 errors, locked for 30 seconds.");
    		digitalWrite(led1, LOW);
 			digitalWrite(led2, LOW);
  			digitalWrite(led3, LOW);
  			digitalWrite(led4, LOW);
            delay(30000);
            compteur = 1;
    		compteur_erreur = 0;
            break;
  		}      
    }
    }
  
  if (compteur == 4)
  {
    while(bonne_rep[3] == false){
      Serial.println(question4);
      delay(500);
      Serial.println(reponses4);
      char key = keypad.getKey();
      
      while(bonne_rep[3] == false){
      key = keypad.getKey();
      if (key != NO_KEY){  
        indice_rep[3] = key;
        bonne_rep[3] = true;
      }
      }
	    if (indice_bonne_rep[3] != indice_rep[3]) {
          Serial.print("Wrong answer \n\n");
          delay(1000);
          compteur_erreur ++;
          bonne_rep[3] = false;
        }
        else {
         Serial.print("Correct answer \n\n");
         compteur++;
         digitalWrite(led4, HIGH);
        }
      
      	if (compteur_erreur == 4)
  		{
    		Serial.println("4 errors, locked for 30 seconds.");
    		digitalWrite(led1, LOW);
 			digitalWrite(led2, LOW);
  			digitalWrite(led3, LOW);
  			digitalWrite(led4, LOW);
            delay(30000);
            compteur = 1;
    		compteur_erreur = 0;
            break;
  		}
    }
    }
  
  if(compteur == 5){
    MA1_valide = true;
    digitalWrite(led6, HIGH); // Turn on corresponding LED
    delay(1000);
    digitalWrite(led1, LOW); // Turn off LEDs
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
  }
  
  
   
}     

void MA2()
{
  char code_voulu[] = {'2','2','9','4'};
  char code_entre[] = {'0','0','0','0'};
  
  compteur = 0;
  delay(2000);
  Serial.println("Please enter your code");
  while(MA2_valide == false) // While code is not correct
  {
    char key = keypad.getKey(); // Get pressed key
    if (key != NO_KEY){ // If a key is pressed

    code_entre[compteur] = key; // Store pressed key at correct index
    compteur++; // Increment counter
    }
       
    if (compteur >= 1)
    { 
      digitalWrite(led1, HIGH); // Turn on corresponding LED
    }
  
  
    if(compteur >= 2)
    { 
      digitalWrite(led2, HIGH);
    }
  
    if (compteur >= 3)
    { 
      digitalWrite(led3, HIGH);
    }
    if (compteur >= 4)
    { 
      digitalWrite(led4, HIGH);
      MA2_valide = true;
    }     

// Code verification
      for (int i = 0; i < 4; i++)
      { 
        if (code_entre[i] != code_voulu[i]) { // If entered code differs from required code
          MA2_valide = false; // Code is incorrect
        }
      }
        
  
      if (MA2_valide == true){ // If code is correct
        digitalWrite(led7, HIGH); // Turn on corresponding LED
        Serial.print("Code correct \n\n"); 
        delay(1500);
        digitalWrite(led1, LOW); // Turn off LEDs
        digitalWrite(led2, LOW);
        digitalWrite(led3, LOW);
        digitalWrite(led4, LOW);
        ;
        
      }
                
         
        
        
    if (compteur == 4 and MA2_valide == false) // If code is incorrect
    {
    for (int i = 0; i < 4; i++)
    {
      digitalWrite(led1, HIGH); // Blink LEDs
      digitalWrite(led2, HIGH);
      digitalWrite(led3, HIGH);
      digitalWrite(led4, HIGH);
      delay(500);
      digitalWrite(led1, LOW);
      digitalWrite(led2, LOW);
      digitalWrite(led3, LOW);
      digitalWrite(led4, LOW);
      delay(500);
    }
     
      compteur = 0;
      compteur_erreur++; // Increment error counter
      Serial.print("Incorrect code, ");
      Serial.print(4-compteur_erreur); // Display remaining attempts
      Serial.println(" attempts left before lockout.");
    }
    
    if (compteur_erreur == 4) // If 4 errors
    {
      Serial.println("4 errors, locked for 30 seconds.");
      delay(30000); // Lock keypad for 30 seconds
      Serial.println("Please enter your code");
      compteur_erreur = 0; // Reset error counter to 0
    }
  }
}

void MA3()
{
  delay(2000);
  Serial.println("Retinal scan -- Please bring your right eye close to the keypad"); 
  delay(2000);
  Serial.println("Retinal scan in progress...");
  delay(2500);
  Serial.print("Retinal scan successful \n\n");
  delay(2000);
  MA3_valide = true; 
  digitalWrite(led8, HIGH);
}

void MA4()
{
  delay(2000);
  Serial.println("Fingerprint scan -- Please place your right thumb on the keypad"); 
  delay(2000);
  Serial.println("Fingerprint scan in progress...");
  delay(2500);
  Serial.print("Fingerprint scan successful \n\n");
  MA4_valide = true; 
  digitalWrite(led9, HIGH);
  delay(2000);  
}

// 				----------Creation of authentication methods----------

//				----------Creation of security levels----------

void niveau1()
{
  MA1();
  if (MA1_valide == true){
    Serial.print("Continuing authentication... \n\n");
    MA3();
    if (MA2_valide == true){
     validation = true;
    }
  }
}


void niveau2()
{
  MA1();
  if (MA1_valide == true){
    Serial.print("Continuing authentication... \n\n");
    MA4();
    if (MA2_valide == true){
     validation = true;
    }
  }
}


void niveau3()
{
  MA2();
  if (MA2_valide == true){
    Serial.print("Continuing authentication... \n\n");
    MA4();
    if (MA4_valide == true){
     validation = true;
    }
  }
}


void niveau4()
{
  MA1(); // Call MA1 function
  if (MA1_valide == true){ // Check if MA1 passed
    Serial.print("Continuing authentication... \n\n");
    MA2();
    if (MA2_valide == true){
      Serial.print("Continuing authentication... \n\n");
      MA3();
      if (MA3_valide == true){
        Serial.print("Continuing authentication... \n\n");
        MA4();
        if (MA4_valide == true){
          validation = true;
        }
      }
    }
  }
}



//				----------Creation of security levels----------


void coffre_ouvert()
{
  Serial.println("> Safe open");
  digitalWrite(led10, HIGH); // Turn on final blue LED
  delay(2000);
  digitalWrite(led5, LOW); 
  digitalWrite(led6, LOW);
  digitalWrite(led7, LOW);
  digitalWrite(led8, LOW);
  digitalWrite(led9, LOW);
  delay(10000);
  digitalWrite(led10, LOW);
  Serial.println("> Safe closed \n> End of simulation"); 
  delay(2000);
  exit(1); // Close safe => end simulation
  
}
