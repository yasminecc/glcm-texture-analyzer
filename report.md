
### **Step 1: Problem Identification and Statement**

Create the GLCM matrix of a given image where direction θ = 0 and distance d = 1 to derive statistics from it like ‘contrast’, ‘energy’, and ‘homogeneity’ that provide information about the texture of an image.

### **Step 2: Gathering Information**

To open file, file name should be known.
Read image matrix from file.
To create the GLCM matrix, number of rows and columns in file should be known.
To normalize matrix: p(i, j) = (M(i, j)/( ∑i,jM(i, j))
Contrast: p(i, j) = ∑i,j|i-j|2 x p(i, j)
Energy = ∑i,jp(i,j)2
Homogeneity =  ∑i,j (p(i, j))/(1+|i - j|2)

### **Step 3: Test Cases**

Test1: testing the output in case 2 and 3 in printing the GLCM and calculating the statistical parameters
5 4
1 1 5 6 8
2 3 5 7 1
4 5 7 1 2
8 5 1 2 5
Test2: Using a data file that contains a matrix of only 0 to check if GLCM and statistical parameters are calculated correctly
5 5
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
Test3: Using a data file that contains a matrix of all 0 except 1 value to check if GLCM and statistical parameters are calculated correctly
5 2
0 0 0 0 0
0 0 0 0 6
Test4: Using a data file that contains a matrix of all 1’s to check if it calculates GLCM and statistical parameters correctly
3 3
1 1 1
1 1 1
1 1 1
Test 5: If file name entered incorrectly or file does not exist then error message “file fail” should appear on screen and program exists with code -1.
Test 6: if case 4 chosen then program should print “exit program” and program should end.
Test 7: if case chosen is not 1, 2, 3 or 4 then program prints “invalid input, chose either 1, 2, 3 or 4” menu items reappear.

### **Step 3: Algorithm**

Declare row and col as integers
Declare variable fname as string
Print enter file name of image pixels
Read fname
Open file fname
If fname fails
Print file fail
(Exit program abnormally exit code -1)
Exit -1
Read file fname into col
Read file fname into row
Declare double pointer imdata as integer, allocate a block of memory each of type int pointer and assign to imdata.
Repeat While( i = 0 and i < row)
Allocate memory block each of type integer and assign it to imdata[i]
Increment i
Repeat while(i = 0 and i < row)
Repeat while(j =0 and j<col)
Read file fname into imdata[i][j]
Increment j
Increment i
Initialize graytone = 0
Repeat While( i=0 and i<row)
Repeat while( j=0 and j< col)
If (imdata[i][j]> graytone)
Assign imdata[i][j] to greytone
Increment j
Increment i
Close file fname
declare double pointer normalarr of type double and initialize it to null pointer
declare glcm as double pointer type int, and allocate to it a memory block each of type double pointer and size graytone +1
Repeat while( i=0 and i<greytone +1)
Allocate memory block size greytone + 1 to glcm[i]
Increment i
Repeat while(i = 0 and i < greytone)
Repeat while(j =0 and j<greytone)
Assign 0 to glcm[i][j]
Increment j
Increment i
Declare repeat as bool and initialize it to true
Repeat while( repeat is true)
print "enter menu item", newline, "press 1 to create and normalize GLCM matrix", newline, "press 2 to compute statistical parameters of texture", newline, "press 3 to print GLCM matrix" ,newline, "press 4 to exit program", newline
Declare choice as char and initialize it to ‘0’
Print newline
Read choice
Print newline
If (choice is ‘1’)
Call function (generate) with arguments (imdata, row, col, glcm)
Call function (normalize) with arguments (glcm, greytone)
Print “GLCM normalized and created”
If (choice is ‘2’)
print "Contrast:"
print function (contrast) with argumets (normalarr, graytone), newline
print "Energy:"
print function (energy) with arguments (normalarr, graytone) , newline
print "Homogeneity:"
print function homogeneity with arguments (normalarr, graytone), newline
if (choice is ‘3’)
Repeat while(i = 0 and i < greytone)
Repeat while(j =0 and j<greytone)
print glcm[i][j]
Increment j
Print newline
Increment i
If (choice is ‘4’)
Print “exit program”
Assign false to repeat
Exit 0
Repeat while (choice is not ‘1’or ‘2’or ‘3’ or’4’)
Print "invalid input, chose either 1, 2, 3 or 4"
Read choice
Print "...BACK TO MAIN MENU..."
Repeat while ( i=0 and i<row)
Delete double pointer normalarr[i]
Delete double pointer glcm[i]
Increment i
Repeat while ( i=0 and i<row)
Delete double pointer imdata[i]
Increment i
delete pointer normalarr
delete pointer glcm
delete pointer imdata
Function definitions:
Normalize:
Initialize total to 0
Repeat while(i = 0 and i < greytone +1)
Repeat while(j =0 and j<greytone +1)
assign glcm[i][j] + total to total
Increment j
Increment i
Declare double pointer normalarr as double,
allocate a block of memory type double pointer and size graytone +1 and assign to normalarr
Repeat while(i = 0 and i < greytone +1)
allocate a block of memory type double pointer and size graytone +1 and assign to normalarr[i]
Increment i
Repeat while(i = 0 and i < greytone +1)
Repeat while(j =0 and j<greytone +1)
assign glcm[i][j] / total to normalarr[i][j]
Increment j
Increment i
Return the values of normalarr
contrast:
initialize cont to 0
Repeat while(i = 0 and i < greytone +1)
Repeat while(j =0 and j<greytone +1)
Assign (i-j)2* normalarr[i][j] to cont
Increment j
Increment i
Return value of cont
energy:
initialize energy to 0
Repeat while(i = 0 and i < greytone +1)
Repeat while(j =0 and j<greytone +1)
Assign energy + (normalarr[i][j])2 to energy
Increment j
Increment i
Return value of energy
homogeneity:
initialize homo to 0
Repeat while(i = 0 and i < greytone +1)
Repeat while(j =0 and j<greytone +1)
Assign homo + (normalarr[i][j])/(1+ (i-j)2) to homo
Increment j
Increment i
Return value of homo

### **Step 4: Code or implementation**

#include <iostream>
#include <fstream>
#include <cmath>
using namespace std;
void generate(int** imdata, int row, int col, int** glcm); //function prototypes
double** normalize(int** glcm, int graytone);
double contrast(double** normalarr, int graytone);
double energy(double** normalarr, int graytone);
double homogeneity(double** normalarr, int graytone);
int main()
{
int row, col;
string fname; //creating variable for user t input file name
ifstream fin;
cout << "enter file name of image pixels " << endl;
cin >> fname;
fin.open(fname); //opening file the user inputs
if (fin.fail()) //validating user input of file and exiting program if file fails
{
cout << "file fail";
exit(-1);
}
fin >> col >> row; //reading the first line of the file to know the number of rows and columns in the matrix
int** imdata = new int* [row]; //creating dynamic 2D array that will read the pixel matrix from file into it
for (int i = 0; i < row; i++)
{
imdata[i] = new int[col];
}
for (int i = 0; i < row; i++) //loop to read pixel matrix from file into imdata dynamic 2D array
{
for (int j = 0; j < col; j++)
{
fin >> imdata[i][j];
}
}
int graytone = 0;
for (int i = 0; i < row; i++) //finding the gray levels to know the maximum size of the GLCM
{
for (int j = 0; j < col; j++)
{
if (imdata[i][j] > graytone)
{
graytone = imdata[i][j];
}
}
}
fin.close(); //close file
double** normalarr = nullptr; //declaring and initializing dynamic 2D array that will contain the normalized matrix
int** glcm = new int* [graytone + 1]; //declaring and initializing the dynamic GLCM 2D array
for (int i = 0; i < graytone + 1; i++)
{
glcm[i] = new int[graytone + 1];
}
for (int i = 0; i < graytone + 1; i++) //initializing all elments in GLCM 2D array to 0
{
for (int j = 0; j < graytone + 1; j++)
{
glcm[i][j] = 0;
}
}
bool repeat = true;
while (repeat == true) //creating loop to repeat menu
{
cout << "enter menu item" << endl << "press 1 to create and normalize GLCM matrix" << endl << "press 2 to compute statistical parameters of texture" << endl << "press 3 to print GLCM matrix" << endl << "press 4 to exit program" << endl;
//presenting menu options
char choice='0';
cout << endl;
cin >> choice; //user inputs menu item
cout << endl;
switch (choice) //creating cases for each menu item
{
case '1': //creat and normalize GLCM matrix
cout << "...";
generate(imdata, row, col, glcm); //calling generate function to create GLCM matrix
normalarr = normalize(glcm, graytone); //calling normalize funtion to normalize GLCM and store it in 2D dynamic array (normalarr)
cout << "GLCM normalized and created"<<endl<<endl;
break;
case'2'://compute statistical parameters of texture
cout << "Contrast:" << contrast(normalarr, graytone) << endl; //calling contrast func. to calculate contrast using the normalized array
cout << "Energy:" << energy(normalarr, graytone) << endl; //calling energy func. to calculate energy using the normalized array
cout << "Homogeneity:" << homogeneity(normalarr, graytone) << endl; //calling homogeneity func. to calculate homogeneity using the normalized array
break;
case '3'://print GLCM matrix
for (int i = 0; i < graytone + 1; i++) //loop to print all elemnts in the glcm array
{
for (int j = 0; j < graytone + 1; j++)
{
cout << glcm[i][j] << " ";
}
cout << endl;
}
break;
case '4'://exit program
cout << "exit program"; //terminating message
repeat = false; //to end menu loop
exit(0);
default:
{
cout << "invalid input, chose either 1, 2, 3 or 4"; // validating user input to ensure it is menu item 1, 2, 3 or 4
}
}
cout << endl << "...BACK TO MAIN MENU..." << endl << endl;
}
for (int i = 0; i < graytone+1; i++) //releasing all dynamically created memory
{
delete[] normalarr[i];
delete[] glcm[i];
}
for (int i = 0; i < row; i++)
{
delete[] imdata[i];
}
delete[] normalarr;
delete[] glcm;
delete[] imdata;
return 0;
}
void generate(int **imdata, int row, int col, int **glcm) // function that creates GLCM matrix and stores it in the dynamic 2D array GLCM
{
for (int i = 0; i < row; i++)
{
for (int j = 0; j < col - 1; j++)
{
glcm[imdata[i][j]][imdata[i][j + 1]]++;
}
}
}
double** normalize(int **glcm,int graytone) //function that normalizes GLCM matrix and returns array that stores normalized matrix
{
int total=0;
for (int i = 0; i < graytone + 1; i++) //loop to calculate the total of all the elements in the GLCM
{
for (int j = 0; j < graytone + 1; j++)
{
total += glcm[i][j];
}
}
double **normalarr = new double* [graytone + 1]; //declaring and initializing dynamic 2D array that will contain normalized matrix
for (int i = 0; i < graytone + 1; i++)
{
normalarr[i] = new double[graytone + 1];
}
for (int i = 0; i < graytone + 1; i++) //loop to normalize all the elements in the glcm and assign them to the normalarr array
{
for (int j = 0; j < graytone + 1; j++)
{
normalarr[i][j] = (double) glcm[i][j] / total; //formula to normalize eac elemnt in the glcm
}
}
return normalarr; //return the normalized array
}
double contrast(double **normalarr, int graytone) //function to calculate contrast using the normalized matrix
{
double cont=0;
for (int i = 0; i < graytone+1; i++) //loop to calculate contrast using all the elements in the normalized array
{
for (int j = 0; j < graytone + 1; j++)
{
cont += pow((i - j), 2) * normalarr[i][j];
}
}
return cont; //return the contrast
}
double energy(double** normalarr, int graytone) //function to calculate energy using the normalized matrix
{
double energy=0;
for (int i = 0; i < graytone + 1; i++) //loop to calculate energy using all the elements in the normalized array
{
for (int j = 0; j < graytone + 1; j++)
{
energy += pow((normalarr[i][j]), 2);
}
}
return energy; //return energy
}
double homogeneity(double** normalarr, int graytone) //function to calculate homogeneity using the normalized matrix
{
double homo=0;
for (int i = 0; i < graytone + 1; i++) //loop to calculate homogeneity using all the elements in the normalized array
{
for (int j = 0; j < graytone + 1; j++)
{
homo += (normalarr[i][j])/(1+pow((i-j),2));
}
}
return homo; //return homogeneity
}

### **Step 5: Test and Verification**

Test1
Test2
Test3
Test4
Test5
Test6
Test7