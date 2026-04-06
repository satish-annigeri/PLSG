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
Hello, world
10, 20, 30
```

Now let us open this file, read its contents and then close it in the traditional way:

```pycon
>>> f = open("sample.txt", "r")
>>> lines = f.readlines()
>>> len(lines)
```

## NumPy


