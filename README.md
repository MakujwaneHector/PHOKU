#include<iostream>
#include<string>
#include<fstream>

using namespace std;

const int SIZE = 4;


//funtion prototypes
void getInfo(string [], string [], int [], char [], int );
void displayInfo(string [], string [], int [], char [], int);
string findOldest(string [], string [], int [], int );

int main()
{
	string NAME[SIZE], SURNAME[SIZE];
	int AGE[SIZE];
	char GENDER[SIZE];

	string OLDEST;

	//Calling funtions
	getInfo(NAME, SURNAME, AGE, GENDER, SIZE);

	displayInfo(NAME, SURNAME, AGE, GENDER, SIZE);

	OLDEST = findOldest(NAME, SURNAME, AGE, SIZE);

	cout << "The oldest person is: " << OLDEST << endl;

	system("pause");
	return 0;
}

//populate the information and names of people written inside INFO file
void getInfo(string nm[], string sn[], int ag[], char gn[], int sz)
{
	string line;
	int ind=0;
	int pos = 0;

	ifstream inFile;

	inFile.open("INFO.txt");

	if (inFile.fail())
	{
		cout << "The file did not open!!!!!" << endl;
	}
	else

	{
		while (getline(inFile, line))
		{
			//getting name
			pos = line.find("#");
			nm[ind] = line.substr(0, pos);
			line = line.erase(0, pos + 1);


			//getting surname
			pos = line.find("#");
			sn[ind] = line.substr(0, pos);
			line = line.erase(0, pos + 1);

			//getting age
			pos = line.find("#");
			ag[ind] = atoi(line.substr(0, pos).c_str());
			line = line.erase(0, pos + 1);

			//geting gender
			gn[ind] = line.at(0);

			//uptade the index
			ind++;

		}
	}
}

//Display the infomation and names of each person that is written inside the INFO file
void displayInfo(string nm[], string sn[], int ag[], char gn[], int sz)
{
	
	for (int i = 0;i < sz;i++)
	{
		cout << "INDIVIDUAL " << i + 1 << endl;

		cout << nm[i] << endl;
		cout << sn[i] << endl;
		cout << ag[i] << endl;
		cout << gn[i] << endl;
		
		cout << endl;
	}
}

//finding the oldest person from displayed above
string findOldest(string nm[], string sn[], int ag[], int sz)
{
	int older=ag[0];
	string oldestPerson;
	int ind;

	for (int i = 0;i < sz;i++)
	{
		if (ag[i] > older)
		{
			older = ag[i];
			ind = i;
		}
	}
	oldestPerson = nm[ind] + " " + sn[ind];

	return oldestPerson;

}
