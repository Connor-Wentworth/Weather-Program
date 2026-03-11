#include <iostream>
#include <cmath>
using namespace std;

double Temp, Wspeed, Dew, Wchill, CBH;
// Varibales Tempature, Wind Speed, Dew point, Wind Chill, and Cloud Base Height
void input(double& Temp, double& Wspeed, double& Dew);
void calcwindchill(double& Temp, double& Wspeed);
void calccloudbaseheight(double& Temp, double& Dew);

int main()
{
	cout << "Weather Boy" << endl;

	input(Temp, Wspeed, Dew);

	calcwindchill(Temp, Wspeed);

	calccloudbaseheight(Temp, Dew);

	cout << "The wind chill for today is " << Wchill << " F" << endl;
	cout << "The Cloud Base Height for today is " << CBH << endl;

	return 0;
}

void input(double& Temp, double& Wspeed, double& Dew) {
	cout << "Enter the Air Temperature ";
	while (!(cin >> Temp)) { // Keep asking until the user enters a valid number
		cout << "Invalid input. Try again: ";
		cin.clear(); // Reset input errors
		cin.ignore(10000, '\n'); // Remove bad input
	}

	cout << "Enter the Wind Speed ";
	while (!(cin >> Wspeed)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}

	cout << "Enter the Dew Point ";
	while (!(cin >> Dew)) {
		cout << "Invalid input. Try again: ";
		cin.clear();
		cin.ignore(10000, '\n');
	}
}

void calcwindchill(double& Temp, double& Wspeed) {
    // Wind Speed formula
	Wchill = 35.74 +
	         0.6215 * Temp -
	         35.75 * pow(Wspeed, 0.16) +
	         0.4275 * Temp * pow(Wspeed, 0.16);
}

void calccloudbaseheight(double& Temp, double& Dew) {
    // Cloud Base Height formula
	CBH = 1000.0 * (Temp - Dew) / 4.4;
}
