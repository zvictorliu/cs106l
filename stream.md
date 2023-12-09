---
description: push and extract
---

# Stream

> communication between a program and its environment is a stream

## console stream

stream objects:

​ `cin` character input

​ `cout` character outpt, connecting to screen

​ `endl` is also a stream object

​ `cerr`

stream operator:

​ insertaion operator: `<<`

​ extraction operator : `>>`

The problem is the `cin` doesn't have safety check, so better be careful about what you type

the **chain**:

in output, it's like connecting strings

in input, read multiple values, `Enter` or `SPACE` to sperate, I don't know why

```cpp
cin >> myInt >> myString;
```

## file stream

a file can also be a source or destination of stream, usage is just like `cin` `cout`

file stream type:

​ header file: `<fstream>`

​ two types: `ifstream` `ofstream`

since it's type, not an object

to create a corresponding object:

```cpp
ifstream myStream("myFile.txt"); // initializing while creating
```

or like this:

```cpp
ifstream myStream;
myStream.open("myFile.txt");
// xxx
myStream.close("myFile.txt");
```

this could explain why python use `with open`

and if the filename is stored in a string object, which is invented later than stream

so a convertion is needed:

```cpp
string myString="myFile.txt";
ifstream input(myString.c_str());
```

a good behavior is always be cautious:

```cpp
if(!input.is_open()) //error checking
 	cerr << "Couldn't open the file myfile.txt" << endl;
```

## stream manipulator

`endl` for example

> a stream manipulator, an object that can be inserted into a stream to change some sort of stream property

`setw()` set width, force `cout` to pad its output with the right number of spaces

`left` `right` align

```cpp
cout << '[' << left << setw(10) << "Hello!" << ']' << endl; // [  Hello!]
cout << '[' << right << setw(10) << "Hello!" << ']' << endl; // [Hello!  ]
```

`setfile()` change the char to fill when using `setw()`

you can't just set, must print some real stuff:

```cpp
cout << setfill('-') << setw(COLUMN_WIDTH) << "" << setfill(' ');
```

other useful manipulator:

​ `hex` `dec` `oct` set the format of number

​ `boolalpha` print string true/false instead of 1/0

​ `ws` ignoring the whitespace

## error state

if the transformation fails, stream enters an error state

isfail? : `cin.fail()`

leave: `cin.clear()`

```cpp
void PrintTableBody() {
     ifstream input("table-data.txt");

     /* Loop over the lines in the file reading data. */
     int rowNumber = 0;
     while(true) {
         int intValue;
         double doubleValue;
         input >> intValue >> doubleValue;

         if(input.fail()) break;

         cout << setw(COLUMN_WIDTH) << (rowNumber + 1) << " | ";
         cout << setw(COLUMN_WIDTH) << intValue << " | ";
         cout << setw(COLUMN_WIDTH) << doubleValue << endl;

         rowNumber++;
     }
 }
```

this can read arbitary lines

it can also be simplifed:

```cpp
while(input >> intValue >> doubleValue)
```

> The streams library is configured so that most stream operations, including stream insertion and extraction, yield a nonzero value if the operation succeeds and zero otherwise.

## extra data

```cpp
cin >> IntVal >> FloatVal;
```

if you type `3.14 2.07`, `IntVal` will be `3` and `FlatVal` will be `.14`, and it didn't enter error state

so the idea is, **what's left in the buffer will still be there when reading next time**

so `cin` is dangerous

## getline

`getline()` until a newline character(which will not be stored), whitespace is not an end

```cpp
getline(cin, myStr);
```

`>>` will store the newline character in the buffer, `>>` will ignores it when reading next time(skips over newline and whitespace characters before reading meaningful data)

so `cin` followed with `getline` is not right

```cpp
cin >> dummyInt;
getline(cin, dummyString);
```

`dummyString` will be empty since it meet a newline charater that left by the `cin` at the very beginning

## string stream

`<sstream>` type: `stringstream`

store data on temporary string buffers

so it's actually an buffer object

`.str()` will convert

```cpp
int levelNum = 100;
stringstream messageText;
messageText << "Level " << levelNum << " is out of bounds.";

printf(messageText.str());
```
