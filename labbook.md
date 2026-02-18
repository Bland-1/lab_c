Q1

to add paramets go to porject - debug - debugging - commad arguemnts then add your params


Q2
```cpp
#include <iostream>
#include <fstream>
using namespace std;


bool Copy(char filenamein[], char filenameout[])
{
	ifstream infile(filenamein);

	if (!infile.is_open())
	{
		cout << "Error: Could not open file" << endl;
		return false;
	}

	ofstream outfile(filenameout);

	if (!outfile.is_open())
	{
		cout << "Could not create output file!" << endl;
		infile.close();
		return false;
	}

	char ch;
	while (infile.get(ch))
	{
		outfile.put(ch);
	}

	infile.close();
	outfile.close();

	return true;
}

int main(int argn, char* argv[])
{
	if (argn != 3) {
		cerr << "Usage: " << argv[0] << " <input filename> <output filename>" << endl;
		int keypress; cin >> keypress;
		return -1;
	}

	if (Copy(argv[1], argv[2]))
	{
		cout << "Copy successful" << endl;
	}
	else
	{
		cout << "Copy error" << endl;
	}

	system("PAUSE");
}
```

Q3

```cpp

#include <iostream>
using namespace std;

// Custom function with 3 different types for investigation
void TestParams(int x, char y, double z) {
    cout << "Int: " << x << ", Char: " << y << ", Double: " << z << endl;
}

int mymax(int a, int b) {
   if(a > b)
     return a;
   else
     return b;
}

int main(int, char **) {
   int a = 10;
   int b = 20;

   // Investigating the call to mymax
   int max = mymax(a, b);

   // Investigating custom function passing
   TestParams(5, 'A', 12.5);

   return 0;
}

```


Watching the code run in the Disassembly window was interesting. I could see the program literally pushing the variables onto the stack before jumping into the function. I noticed that when I called mymax(a, b), the assembly code actually pushed b first and then a, which felt backwards to me until I read about how the stack works. Checking the Memory window confirmed that my integers were 4 bytes each, stored as 0a 00 00 00 for the number 10. It really helped me visualize how the computer actually manages data behind the scenes instead of just trusting the C++ code to work.
