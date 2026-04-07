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
print(lines)
['Hello, world!\n', '10, 20, 30\n', '\n']
>>> type(lines[0])
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
7. File must be closed when no more operations are required to be performed on it.

The alternative way is to use a **context manager**, a protocol that sets up a resource, uses it safely inside a block, and guarantees clean upafterward. A context manager can be used with such resources as a file on the filesystem, connection to a database, connection to a server etc. The typical syntax is `#!python with resource as handle_to_resource:`, followed by an indented set of statements that is treated as a block of code to be executed safely. Upon exiting the block, the resource is cleaned up, which in the case of a file means to close the file..

Here is the code to use a context manager to read the file:
```pycon
>>> with open("sample.txt", "r") as f:
...     lines = f.readlines()
...     
>>> print(lines)
['Hello, world!\n', '10, 20, 30\n', '\n']
```

**Note**

1. The context manager is indicated by the keyword `with`.
2. The function call `open("sample.txt", "r")` returns a file object.
3. The file returned by the `open()` function call is assigned the name `f`, or any other chosen by the programmer.
4. The `with` statement is followed by a block of code, indicated by the indentation of the statements.
5. There is no need to close the file as it is automatically closed when the context manager is exited.

The file can also be read one line at a time, instead of reading the entire file in one go. This is useful when the file is very large and will use substantial amount of memory. Here is the code that uses a context manager and reads one line at a time until all lines are read:
```pycon
>>> with open("sample.txt", "r") as f:
...     for line in f:
...         print(line)
...         
Hello, world!

10, 20, 30




```

**Note**

1. Using the context manager, the file `sample.txt` is opened in read mode and a file handle `f` is assigned to the opened file for future use.
2. `for line in f:` reads one line at a time from the file using the file handle `f`.
3. The `for` loop is terminated when there are no more lines to be read.
4. An empty line is printed at the end of each line because of the newline character `\n` at the end of each line read from the file. The REPL itself prints a newline. That is the reason for two empty lines for each line read from the file. The trailing newline character can be stripped at the time of printing, with `print(line.rstrip("\n"))`.

**It is a good idea to use a context manager for file operations, and must always be used unless there is a reeason not to do so.**

### Writing text files

Writing to a text file is similar to reading from a file.
```pycon
>>> with open("demo.txt", "w") as f:
...     f.write("Hello, world!\n")
...     f.write(f"{10}, {20}, {30}\n")
...
14
11
```

**Note**

1. `f.write()` takes exactly one argument. To print multiple values, use a f-string to prepare a formatted string as the argument.
2. `f.write()` does not print a newline character `\n` at the end of each erite, like `print()` does. to write the next output on a new line, end the string with a `\n`.
3. `f.write()` return the number of characters written to the file. That is the reason for the output `14` and `11`, the number of characters, including the `\n` character in the two lines written t the file.

You can open the `demo.txt` file in a text editor and read its contents.

!!! warning
    Remember what happens when you open a file for writing:

    1. If a file with the specified name exists, it overwritten from the beginning of the file.
    2. If a file with the specified name does not exist, a new file with the specified name is created.
    3. A file can be opened for writing from the end of the file, that is, appending, instead of from the start of the file. The write mode must then be specified as `"a"`. In this case, the file is not overwritten if it exists.

### Writing to a binary file

Writing to a binary file is identical to writing to a text file, except that the argument must be of type `byte` or byte-like. 

```pycon
>>> with open("demo2", "wb") as f:
...     f.write(b"Hello, world!")
```

Open the file `demo2" in a text editor and the contents can be read.

Attempting to write a `str` to a file opened for writing in binary mode raises a `typeError` exception.

```pycon
>>> with open("demo2", "wb") as f:
...     f.write("Hello, world!")
...     
Traceback (most recent call last):
  File "<python-input-9>", line 2, in <module>
    f.write("Hello, world!")
    ~~~~~~~^^^^^^^^^^^^^^^^^
TypeError: a bytes-like object is required, not 'str'
```

To write values other than strings in binary format, the value must first be converted to binary format. Here is a way to convert an integer to binary format:
```pycon
>>> import struct
>>> with open("demo3", "wb") as f:
...     f.write(struct.pack("i", 10))    # Write the integer 10 as a 4-byte signed-integer
```

Opening the file `demo2` n a text editor does not display anything human-readable. A binary editor can display the contents, but as a sequence of bytes, which is indecipherable to humans. However, reading file fetches the exact value of the file.



## NumPy


