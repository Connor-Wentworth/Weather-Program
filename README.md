#include <iostream>   // Library for input and output (cin, cout)
#include <cmath>      // Library for mathematical functions like pow()
using namespace std;

// Global variables used throughout the program
double Temp, Wspeed, Dew, Wchill, CBH;
// Temp   = Air Temperature
// Wspeed = Wind Speed
// Dew    = Dew Point
// Wchill = Wind Chill result
// CBH    = Cloud Base Height result

// Function prototypes (tell the compiler these functions exist)
void input(double& Temp, double& Wspeed, double& Dew); 
// Gets user input for temperature, wind speed, and dew point

void calcwindchill(double& Temp, double& Wspeed); 
// Calculates the wind chill based on temperature and wind speed

void calccloudbaseheight(double& Temp, double& Dew); 
// Calculates the cloud base height using temperature and dew point

int main()
{
	// Program introduction message
	cout << "Good morning New Jersey and this is your weather forcast for today." << endl;

	// Call the function that gathers user input
	input(Temp, Wspeed, Dew);

	// Call function to calculate wind chill
	calcwindchill(Temp, Wspeed);

	// Call function to calculate cloud base height
	calccloudbaseheight(Temp, Dew);

	// Display the calculated wind chill
	cout << "The wind chill for today is " << Wchill << " F" << endl;

	// Display the calculated cloud base height
	cout << "The Cloud Base Height for today is " << CBH << endl;

	return 0;
}

// Function to collect user input with validation
void input(double& Temp, double& Wspeed, double& Dew) {

	// Ask the user to enter the air temperature
	cout << "Enter the Air Temperature ";

	// Keep asking until a valid number is entered
	while (!(cin >> Temp)) { 
		cout << "Invalid input. Try again: ";
		cin.clear(); // Reset the error flag on cin
		cin.ignore(10000, '\n'); // Discard invalid input from buffer
	}

	// Ask the user to enter wind speed
	cout << "Enter the Wind Speed ";

	// Validate wind speed input
	while (!(cin >> Wspeed)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}

	// Ask the user to enter dew point
	cout << "Enter the Dew Point ";

	// Validate dew point input
	while (!(cin >> Dew)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}
}

// Function that calculates wind chill
void calcwindchill(double& Temp, double& Wspeed) {

	// Wind Chill formula used by meteorologists
	// Uses temperature and wind speed to estimate how cold it feels
	Wchill = 35.74 +
	         0.6215 * Temp -
	         35.75 * pow(Wspeed, 0.16) +
	         0.4275 * Temp * pow(Wspeed, 0.16);
}

// Function that calculates cloud base height
void calccloudbaseheight(double& Temp, double& Dew) {

	// Cloud Base Height formula
	// Estimates the altitude where clouds will begin forming
	// based on temperature and dew point difference
	CBH = 1000.0 * (Temp - Dew) / 4.4;
}
