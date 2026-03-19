#include <iostream>   // Allows input/output using cin and cout
#include <cmath>      // Needed for pow() function in wind chill formula
using namespace std;

// Function prototypes
void take_input(double& Temp, double& Wspeed, double& Dew);
void calcWchill(double& Temp, double& Wspeed, double& Wchill);
void calcCBH(double& Temp, double& Dew, double& CBH);
void show_output(double& Temp, double& Wspeed, double& Dew, double& CBH, double& Wchill);

int main() {

	// Variables for temperature, wind speed, dew point, and calculated results
	double Temp, Wspeed, Dew, CBH, Wchill;

	cout << "Good morning New Jersey and this is your weather forecast for today." << endl;

	// Get user input
	take_input(Temp, Wspeed, Dew);

	// Calculate weather values
	calcWchill(Temp, Wspeed, Wchill);
	calcCBH(Temp, Dew, CBH);

	// Display the results
	show_output(Temp, Wspeed, Dew, CBH, Wchill);

	return 0;
}

// Function to collect user input and validate numeric values
void take_input(double& Temp, double& Wspeed, double& Dew) {

	cout << "Enter the Temperature: ";

	// Loop until a valid number is entered
	while (!(cin >> Temp)) {
		cout << "Invalid input. Try again: ";
		cin.clear();                // Reset error state
		cin.ignore(10000, '\n');    // Remove invalid input from buffer
	}

	cout << "Enter the Wind Speed: ";

	while (!(cin >> Wspeed)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}

	cout << "Enter the Dew Point: ";

	while (!(cin >> Dew)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}
}

// Function that calculates the wind chill using the meteorological formula
void calcWchill(double Temp, double Wspeed, double& Wchill) {

	Wchill = 35.74 + (0.6215 * Temp)
	         - (35.75 * pow(Wspeed, 0.16))
	         + (0.4275 * Temp * pow(Wspeed, 0.16));
}

// Function that calculates the Cloud Base Height (CBH)
// based on the difference between temperature and dew point
void calcCBH(double Temp, double Dew, double& CBH) {

	CBH = 1000.0 * (Temp - Dew) / 4.4;
}

// Function to display the calculated weather information
void show_output(double Temp, double Wspeed, double Dew, double CBH, double Wchill) {

	cout << "The wind chill for today is " << Wchill << " F" << endl;
	cout << "The Cloud Base Height for today is " << CBH << " ft" << endl;
}
