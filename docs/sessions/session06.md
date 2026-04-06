# Session 6

#### Planned Schedule: 11-04-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Reading and writing files
4. NumPy


## Reading and writing files
Reading from or writing to a file involves opening the file, reding from or writing to it and closing the file.It is good programming practice to close files that have been opened even though all open files will be closed when a program terminates.

The data in a file can be text or binary format. Text data consists of ASCII or UTF-8 characters and can be displayed on the screen and be understood by humans. Binary data consists of bytes and when displayed on the screen, it cannot be read by humans although computers can interpret the contents.

Python provides the context manager `with` so that when the program goes out of the scope of the context manager, the file is autmatically closed without having to explicitly close it.

### Reading text files

Create a text file named `sample.txt` using a text editor such as Notepad on Windows or `nano` or `gedit` on GNU/Linux and type the following lines in it and save it in the same directory as the program `read_file.py`.

``` title="File: samle.txt"
Hello, world!
10, 20, 30

```

Now let us open this file, read its contents and then close it in the traditional way:

```pycon
>>> f = open("sample.txt", "r")
>>> type(f)
<class '_io.TextIOWrapper'>
>>> lines = f.readlines()
>>> type(lines)
<class 'list'>
>>> len(lines)
3
type(lines[0])
<class 'str'>
>>> lines[0]
'Hello, world!\n'
>>> ;ines[1]
'10, 20, 30\n'
>>> lines[2]
'\n'
f.close()
```
**Note**

1. `f = open("sample.txt", "r")` opens the file and and stores a reference to the opened file for future use. `f` is of type `<class '_io.TextIOWrapper'>`.
2. The `"r"` argument specifies the file is to be opened for reading. To write to a file, one must use `"w":"`.
3. By default, the file is opened in text format, which can be explicitly specified as `"rt"` or `"wt"`. The other mode is binary format, which is specified by `"rb"` or `"wb"`.
5. `f.readlines()` reads all lines from the file as a `list` of `str`. Each string ends with the newline character `\n`. The entire file is read in as `str`, the programmer must split and convert the strings into the required type.
6. The last line is an empty line, and contains only a newline character `\n`.
7. File must be closed when no more operations are required t be performed on it.


## NumPy


