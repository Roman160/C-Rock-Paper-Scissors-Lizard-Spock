# Rock-Paper-Scissors-Lizard-Spock
Rock Paper Scissors Lizard Spock Game that can be run on a microcontroller with Serial Terminal

// Amount of Memory assigned for the Microcontroller t0 accecpt characters in the serial terminal is made

char command[0x20];

void setup() {
  Serial.begin(115200);
  while (!Serial);
  delay(3000);
  Serial.println("Rock Paper Scissors Lizard Spock");
}

uint8_t receive_function(char* buff, uint8_t sizevar)
{
  static uint8_t ctr = 0; // store the current position in the buff array
  uint8_t ch; // store the last character received
  if (Serial.available() > 0) // true when characters in serial input buffer
  {
    ch = Serial.read(); // store character from buffer in ch
    if ( ctr < sizevar) { // if the ctr is less than your buffer yet
      buff[ctr++] = ch; // add it to your buffer
    }
    if (ch == '\r') // if that character is a carriage return
    {
      buff[ctr - 1] = 0; // replace '\r' with '\0' (string termination)
      ctr = 0; // reset the pointer
      Serial.print("Command: "); // print a string and stay on the same line
      Serial.println(buff); // print received followed by a new line
      return 1;
    }
    else
      return 0;
  } //end serial was available
  return 0;
}

// Each Function is the 'Computer's choice'
// These are the possible outcomes of the game depending on what the User input is and what the Computer 'chose'
// The outcome is then printed on the Serial Monitor

void rock(void) {
  if (receive_function(command, sizeof(command)))
  {
    if (strcmp(command, "rock") == 0)
    {
      Serial.println("Tie Game"); 
    }
    else if (strcmp(command, "paper") == 0)
    {
      Serial.println("You Win!"); 
    }
    else if (strcmp(command, "scissors") == 0)
    {
      Serial.println("You Lose!"); 
    }
    else if (strcmp(command, "lizard") == 0)
    {
      Serial.println("You Win!"); 
    }
    else if (strcmp(command, "spock") == 0)
    {
      Serial.println("You Win!");
    }
  }
}

//Possible outcomes depending on User input from the Serial Terminal when the Computer chooses Paper
// The outcome is then printed on the Serial Monitor

void paper(void) {
  if (receive_function(command, sizeof(command)))
  {
    if (strcmp(command, "rock") == 0)
    {
      Serial.println("You Lose!");
    }
    else if (strcmp(command, "paper") == 0)
    {
      Serial.println("Tie Game");
    }
    else if (strcmp(command, "scissors") == 0)
    {
      Serial.println("You Win!");
    }
    else if (strcmp(command, "lizard") == 0)
    {
      Serial.println("You Win!");
    }
    else if (strcmp(command, "spock") == 0)
    {
      Serial.println("You Lose!");
    }
  }
}

//Possible outcomes depending on User input from the Serial Terminal when Computer chooses Scissors
// The outcome is then printed on the Serial Monitor

void scissors(void) {
  if (receive_function(command, sizeof(command)))
  {
    if (strcmp(command, "rock") == 0)
    {
      Serial.println("You Win!");
    }
    else if (strcmp(command, "paper") == 0)
    {
      Serial.println("You lose!");
    }
    else if (strcmp(command, "scissors") == 0)
    {
      Serial.println("Tie Game!");
    }
    else if (strcmp(command, "lizard") == 0)
    {
      Serial.println("You Lose!");
    }
    else if (strcmp(command, "spock") == 0)
    {
      Serial.println("You Win!");
    }
  }
}

//Possible outcomes depending on User input from the Serial Terminal when Computer chooses Lizard
// The outcome is then printed on the Serial Monitor

void lizard(void) {
  if (receive_function(command, sizeof(command)))
  {
    if (strcmp(command, "rock") == 0)
    {
      Serial.println("You Win!");
    }
    else if (strcmp(command, "paper") == 0)
    {
      Serial.println("You Lose!");
    }
    else if (strcmp(command, "scissors") == 0)
    {
      Serial.println("You Win!");
    }
    else if (strcmp(command, "lizard") == 0)
    {
      Serial.println("Tie Game!");
    }
    else if (strcmp(command, "spock") == 0)
    {
      Serial.println("You Lose!");
    }
  }
}

//Possible outcomes depending on User input from the Serial Terminal when Computer chooses Spock
// The outcome is then printed on the Serial Monitor

void spock(void) {
  if (receive_function(command, sizeof(command)))
  {
    if (strcmp(command, "rock") == 0)
    {
      Serial.println("You Lose!");
    }
    else if (strcmp(command, "paper") == 0)
    {
      Serial.println("You Win!");
    }
    else if (strcmp(command, "scissors") == 0)
    {
      Serial.println("You Lose!");
    }
    else if (strcmp(command, "spock") == 0)
    {
      Serial.println("Tie Game!");
    }
    else if (strcmp(command, "lizard") == 0)
    {
      Serial.println("You Win!");
    }
  }
}


 //The Computer creates a number between 0 - 5 and a 'choice' for the computer is assisnged based on the number generated
 // User enters their choice into Serial Terminal and the Computer generates a random number triggering a function 
// The winner is decided based on the random number generated and the function assigned to that number and the user input
// The game resets after  and another choice can be made 

void loop() {
  uint8_t randomNumber;
  randomNumber = random(0, 5);
  if (randomNumber == 0) {
    rock();
  }
  else if (randomNumber == 1) {
    paper();
  }
  else if (randomNumber == 2) {
    scissors();
  }
  else if (randomNumber == 3) {
    lizard();
  }
  else if (randomNumber == 4) {
    spock();
  }
}

