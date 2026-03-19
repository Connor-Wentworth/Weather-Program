#include <iostream>   // Allows input/output using cin and cout
#include <cmath>      // Needed for pow() function in wind chill formula
using namespace std;

void take_input(double& temp, double& wSpeed, double& dew);
// function used to gather input from the user 
void calcwChill(double& temp, double& wSpeed, double& wChill);
// function used to take user input and use it to calculate for Wind Chill
void calccbh(double& temp, double& dew, double& cbh);
// function used to take user input and use it to calculate for Cloud Base Height
void show_output(double& temp, double& wSpeed, double& dew, double& cbh, double& wchill);
// function used to take the output the Wind Chill and the Cloud Base Height
int main() {
	// Variables for temperature, wind speed, dew point, and calculated results
	double temp, wSpeed, dew, cbh, wChill;

	cout << "Good morning New Jersey and this is your weather forecast for today." << endl;

	// Get user input
	take_input(temp, wSpeed, dew);

	// Calculate weather values
	calcwChill(temp, wSpeed, wChill);
	calccbh(temp, dew, cbh);

	// Display the results
	show_output(temp, wSpeed, dew, cbh, wChill);

	return 0;
}

// Function to collect user input and validate numeric values
void take_input(double& temp, double& wSpeed, double& dew) {

	cout << "Enter the Temperature: ";

	// Loop until a valid number is entered
	while (!(cin >> temp)) {
		cout << "Invalid input. Try again: ";
		cin.clear();                // Reset error state
		cin.ignore(10000, '\n');    // Remove invalid input from buffer
	}

	cout << "Enter the Wind Speed: ";

	while (!(cin >> wSpeed)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}

	cout << "Enter the Dew Point: ";

	while (!(cin >> dew)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}
}

// Function that calculates the wind chill using the meteorological formula
void calcwChill(double& temp, double& wSpeed, double& wChill) {

	wChill = 35.74 + (0.6215 * temp)
	         - (35.75 * pow(wSpeed, 0.16))
	         + (0.4275 * temp * pow(wSpeed, 0.16));
}

// Function that calculates the Cloud Base Height (CBH)
// based on the difference between temperature and dew point
void calccbh(double& temp, double& dew, double& cbh) {

	cbh = 1000.0 * (temp - dew) / 4.4;
}

// Function to display the calculated weather information
void show_output(double& temp, double& wSpeed, double& dew, double& cbh, double& wChill) {

	cout << "The wind chill for today is " << wChill << " F" << endl;
	cout << "The Cloud Base Height for today is " << cbh << " ft" << endl;
} 
