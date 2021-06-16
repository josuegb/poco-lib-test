# Files Presentation Echo
## [Project UML](https://lucid.app/lucidchart/invitations/accept/inv_10c2d877-8c72-44c9-bd6f-9469c7c74cd2)

## Binary Files
### File size and indexation
In C++, files are considered a stream or an array of uninterpreted bytes, 
each byte can also be considered a `char`, with the file contents considered
as a char array: `(char *)myFile`. 

The "array" of bytes stored in a file is indexed from zero to len-1, 
where len is the total number of bytes in the entire file.

### Opening Files
There are two main ways of opening files in binary mode:

1. Set a file name and necessary flags in the constructor when declaring the object.
```c++
fstream myFile ("data.bin", ios::in | ios::binary);
```
2. Declare a stream object and use the `open` method to set the file name and necessary flags.
```c++
fstream myFile;
myFile.open ("data2.bin", ios::out | ios::binary);
```

There are two main flags that need  to be used when manipulating binary files:

1. The i/o mode `ios::in` or `ios::out`
2. The binary mode `ios::binary`

### Reading and Writing to a file
#### Reading operations
The `read` method extracts a given number of bytes from the stream, 
and places them into the memory pointed to by the first parameter.

```c++
Person person;

std::string filename = "people.bin";
ifstream inFile;
inFile.open(filename, ios::binary);

inFile.read((char*)&person, sizeof(person));

cout << person.toString << std::endl;

inFile.close();
```


#### Writing operations
The write member function writes a given number of bytes on the given stream, 
starting at the position of the "put" pointer.

```c++
Person person1 = Person("Julio");

std::string filename = "people.bin";
ofstream outFile;
outFile.open(filename, ios::binary);

outFile.write((char *)&person1, sizeof(person1));
outFile.close();
```

### Accessing file positions
Each open file will have a "get" and a "put" pointer, these store a position in
the file, and are part of the stream object.

#### The GET pointer
It is the current reading position, the index of the next byte that will be read from the file.

The get pointer can be repositioned with the `istream& seekg(streampos pos)` method.

To return the index of the get pointer on a given stream use `istream& tellg()`.
```c++
Person person;

std::string filename = "people.bin";
ifstream inFile;
inFile.open(filename, ios::binary);

inFile.seekg (sizeof(person),ios::begin);
// Reading the second person in the file
inFile.read((char*)&person, sizeof(person));

cout << person.toString << std::endl;

inFile.close();
```

#### The PUT pointer

The put pointer can be repositioned with the `ostream& seekp(streampos pos)` method.

To return the index of the put pointer on a given stream use `istream& tellp()`.
```c++
Person person;

std::string filename = "people.bin";
ofstream outFile;
outFile.open(filename, std::ios::binary | std::ios::app);

std::cout << "Adding in position: " << outFile.tellp() << " byte." << std::endl;
// Adding to the end of the file.
outFile.write((char*)&person, sizeof(person));

outFile.close();
```
