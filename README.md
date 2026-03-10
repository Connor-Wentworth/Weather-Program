#include <iostream>
#include <cmath>
using namespace std;
double calcwindchill(double Temp, double Wspeed) {
	double Wchill = 35.74
	                + 0.6215 * Temp
	                - 35.75 * pow(Wspeed, 0.16)
	                + 0.4275 * Temp * pow(Wspeed, 0.16);
	return Wchill;
}
double calccloudbaseheight(double Temp, double Dew) {
	double CBH = 1000.0 * (Temp - Dew) / 4.4;
	return CBH;
}
int main()
{
	double Temp,Wspeed,Dew;
	cout << "Enter the Air Tempature ";
	cin >> Temp;
	cout << "Enter the Wind Speed ";
	cin >> Wspeed;
	cout << "Enter the Dew Point ";
	cin >> Dew;
	
	double Wchill = calcwindchill(Temp, Wspeed);
	double CBH = calccloudbaseheight(Temp,Dew);
	
	cout << "The wind chill for today is " << Wchill << " F" << endl;
	cout << "The Cloud Base Height for today is " << CBH;

	return 0;
}
