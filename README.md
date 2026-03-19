#include <iostream>   // Allows input/output using cin and cout
#include <cmath>      // Needed for pow() function in wind chill formula
using namespace std;

void take_input(double& temp, double& windSpeed, double& dewPoint);
// function used to gather input from the user 
void calcwindChill(double& temp, double& windSpeed, double& windChill);
// function used to take user input and use it to calculate for Wind Chill
void calccloudBase(double& temp, double& dewPoint, double& cloudBase);
// function used to take user input and use it to calculate for Cloud Base Height
void show_output(double& temp, double& windSpeed, double& dewPoint, double& cloudBase, double& windChill);
// function used to take the output the Wind Chill and the Cloud Base Height

int main() {
	// Variables for temperature, wind speed, dew point, and calculated results
	double temp, windSpeed, dewPoint, cloudBase, windChill;

	cout << "Good morning New Jersey and this is your weather forecast for today." << endl;

	// Get user input
	take_input(temp, windSpeed, dewPoint);

	// Calculate weather values
	calcwindChill(temp, windSpeed, windChill);
	calccloudBase(temp, dewPoint, cloudBase);

	// Display the results
	show_output(temp, windSpeed, dewPoint, cloudBase, windChill);

	return 0;
}

// Function to collect user input and validate numeric values
void take_input(double& temp, double& windSpeed, double& dewPoint) {

	cout << "Enter the Temperature: ";

	// Loop until a valid number is entered
	while (!(cin >> temp)) {
		cout << "Invalid input. Try again: ";
		cin.clear();                // Reset error state
		cin.ignore(10000, '\n');    // Remove invalid input from buffer
	}

	cout << "Enter the Wind Speed: ";

	while (!(cin >> windSpeed)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}

	cout << "Enter the Dew Point: ";

	while (!(cin >> dewPoint)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}
}

// Function that calculates the wind chill using the meteorological formula
void calcwindChill(double& temp, double& windSpeed, double& windChill) {

	windChill = 35.74 + (0.6215 * temp)
	         - (35.75 * pow(windSpeed, 0.16))
	         + (0.4275 * temp * pow(windSpeed, 0.16));
}

// Function that calculates the Cloud Base Height (CBH)
// based on the difference between temperature and dew point
void calccloudBase(double& temp, double& dewPoint, double& cloudBase) {

	cloudBase = 1000.0 * (temp - dewPoint) / 4.4;
}

// Function to display the calculated weather information
void show_output(double& temp, double& windSpeed, double& dewPoint, double& cloudBase, double& windChill) {

	cout << "The wind chill for today is " << windChill << " F" << endl;
	cout << "The Cloud Base Height for today is " << cloudBase << " ft" << endl;
} 
