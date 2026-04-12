# Assignment 6

#### Corresponds to: [Session 6](../sessions/session06.md)

### Quiz: File Handling in Python (Text and Binary)

**Course:** Python for Structural Engineers  
**Topic:** Reading and Writing Files with Context Managers  
**Time Allotted:** 15 Minutes  

---

#### Instructions  
Select the most appropriate answer for each of the following questions.

---

**1. What is the primary advantage of using the `with` statement (context manager) when opening a file in Python?**  
A. It makes the file reading process significantly faster.  
B. It automatically closes the file, even if an exception/error occurs during processing.  
C. It allows you to open multiple files simultaneously in different threads.  
D. It encrypts the data being written to the disk.  
??? success "Answer"
    **Answer:** B  

**2. You are working with a CSV file containing structural load data. Which mode should you use if you want to read the file without the risk of accidentally modifying it?**  
A. `"w"`  
B. `"a"`  
C. `"r"`  
D. `"wb"`  
??? success "Answer"
    **Answer:** C  
    **Explanation:** `"w"` opens the file for writing (truncating the file first) in text mode, `"wb"` opens the file for writing in binary mode and `"a"` opens the file for writing, appending to the end of the file if it exists.

**3. You need to append a new set of sensor readings to the end of an existing log file without deleting the previous data. Which mode is correct?**  
A. `"w"`  
B. `"a"`  
C. `"r+"`  
D. `"rb"`  
??? success "Answer"  
    **Answer:** B  
    **Explanation:** `"w"` open sthe file for writing in text mode, `"r+"` opens the file for updating (reading and writing) and `"rb"` opens the file for reading in binary mode.  

**4. What is the difference between `'r'` and `'rb'` modes?**  
A. `'r'` is for reading files; `'rb'` is for writing binary files.  
B. `'r'` is for reading text files; `'rb'` is for reading files in binary format (e.g., images or compiled data)  
C. `'r'` is faster than `'rb'`.  
D. There is no difference; they are interchangeable.  
??? success "Answer"  
    **Answer:** B

**5. When using `f.readlines()` on a text file, what is the data type of the returned object?**  
A. A single long string containing all the text.  
B. A list of strings, where each element represents one line.  
C. A dictionary where keys are line numbers.  
D. A tuple of bytes.  
??? success "Answer"  
    **Answer:** B

**6. If you are processing a massive structural analysis log file (e.g., 10 GB) and want to avoid crashing your computer's RAM, which approach is most memory-efficient?**  
A. `data = f.read()`  
B. `lines = f.readlines()`  
C. `for line in f:`  
D. `data = f.read().split('\n')`  
??? success "Answer"  
    **Answer:** C  
    **Explanation:**  
    A. `data = f.read()` reads upto a specified number of bytes form the file `f`, and if the number of bytes is not specified, as in this case, it reads the entire file.  
    B. `lines = f.readlines()` reads the entire line into a list of `str`  
    D. `data = f.read().split('\n')` is similar to `data = f.read()`, except that the bytes are split into the elements of a `list` at each `\n` in the data read in.  

    Options A, B and D read the entire file into memory, which is inefficient when the file is large.

**7. Which of the following code snippets will result in an error if the file `results.txt` does not exist?**  
A. `with open('results.txt', 'w') as f:`  
B. `with open('results.txt', 'a') as f:`  
C. `with open('results.txt', 'r') as f:`  
D. `with open('results.txt', 'wb') as f:`  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** Opening a non-existent file for writing automatically creates it. Opening a file for reading requires that the file exists, and the `FileNotFoundError` exception is raised in case it does not.

**8. When writing a list of strings, such as `['Node 1\n', 'Node 2\n']`, to a file, which method is specifically designed to handle an iterable of strings?**  
A. `f.write()`  
B. `f.writelines()`  
C. `f.append()`  
D. `f.save()`  
??? success "Answer"  
    **Answer:** B  
    **Explanation:** `f.writelines()` writes a list of lines to the stream. Line separators are not added, so it is usual for each of the lines provided to have a line separator at the end. See Python [documentation for `writelines()`](https://docs.python.org/3/library/io.html#io.IOBase.writelines).  

**9. You are reading a text file that contains special mathematical symbols or non-ASCII characters (like the degree symbol `°`). Which parameter should you include in the `open()` function to ensure correct interpretation?**  
A. `format='utf-8'`  
B. `mode='binary'`  
C. `encoding='utf-8'`  
D. `type='unicode'`  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** See the *encoding* keyword argument to `open()` in the Python [documentation for `open()`](https://docs.python.org/3/library/functions.html#open) for an explanation.  

**10. When opening a file in binary mode (`'wb'`), what type of data must be passed to the `f.write()` method?**  
A. A standard `string`.  
B. An `integer` or `float`.  
C. A `bytes-like object` (e.g., `bytes` or `bytearray`).  
D. A `list` of characters.  
??? success "Answer"  
    **Answer:** C  

**11.  A binary file is often described as being "non-human readable." What does this primarily mean in the context of Python?**  
A. Python cannot open the file.  
B. The file does not follow standard text encoding (like UTF-8. and represents data as a sequence of raw 8-bit integers)  
C. The file is encrypted and requires a password.  
D. The file can only be opened by specialized engineering software.  
??? success "Answer"  
    **Answer:** B  
    **Explanation:** It refers to the lack of a text-based encoding layer.  

**12. In structural health monitoring, you receive a binary file where every 8 bytes represents a 64-bit floating-point number (a "double"). Which Python module is most commonly used to convert these raw bytes into actual Python `float` objects?**  
A. `math`  
B. `struct`  
C. `numpy` (though `struct` is the standard built-in for this)  
D. Both B and C are correct.
??? success "Answer"  
    **Answer:** D  
    **Explanation:** `struct` is the built-in standard; `numpy` is also widely used for large arrays.  

**13. When a file is opened in binary mode (`'rb'`), what is the data type of the object returned by the `.read()` method?**
A. `str` (String)  
B. `list` (List of characters)  
C. `bytes`  
D. `int` (Integer)  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** Binary mode always returns `bytes` objects.  

**14. You are reading a binary file containing raw sensor data. You only want to read the first 16 bytes to check the file header. Which command is correct?**  
A. `f.read(16)`  
B. `f.readline(16)`  
C. `f.read_bytes(16)`  
D. `f.next(16)
??? success "Answer"
    **Answer:** A  
    bExplanation: `read(n)` reads exactly *n* bytes.  

**15. When using the `struct.unpack()` method to parse binary data, what does the "format string" (e.g., `'<f'` or `'d'`) define?**  
A. The filename of the data.  
B. The compression level of the file.  
C. The data type (e.g., float, integer) and the byte order (endianness).  
D. The number of lines in the file.  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** Format strings tell Python how to interpret the raw bytes. See the Python [documentation for format strings when using `struct.unpack()`](https://docs.python.org/3/library/struct.html#format-strings) and [format characters](https://docs.python.org/3/library/struct.html#format-characters).  

---

### Quiz: Introduction to NumPy and Array Creation

**Course:** Python for Structural Engineers  
**Topic:** NumPy Basics, `ndarray`, and Dimensionality (1D, 2D, 3D)  
**Time Allotted:** 20 Minutes  

---

#### Instructions  
Select the most appropriate answer for each of the following questions.

---

**1. What is the primary purpose of the NumPy library in the Python ecosystem?**  
A. To create graphical user interfaces (GUIs) for engineering software.  
B. To provide high-performance multi-dimensional array objects and tools for working with these arrays.  
C. To manage databases containing structural inspection records.  
D. To automate the sending of emails and reports.  
??? success "Answer"  
    **Answer:** B  
    **Explanation:** NumPy is built for numerical computing and N-dimensional arrays.  

**2. Why is NumPy preferred over standard Python lists for large-scale structural calculations (e.g., Finite Element Analysis)?**  
A. NumPy arrays are more flexible and can hold different data types (strings and floats) in the same array.  
B. NumPy arrays are stored in a way that allows for much faster mathematical operations and better memory efficiency.  
C. Python lists cannot perform addition or subtraction.  
D. NumPy is the only library that allows for the use of loops.  
??? success "Answer"  
    **Answer:** B  
    **Explanation:** Vectorization and contiguous memory allocation make NumPy much faster than lists.  

**3. What is the name of the core data structure in NumPy?**  
A. `list`  
B. `matrix_object`  
C. `ndarray` (N-dimensional array)  
D. `array_structure`  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** `ndarray` is the fundamental object.  

**4. Which of the following is the standard, community-accepted way to import NumPy?**  
A. `import numpy`  
B. `from numpy import *`  
C. `import numpy as np`  
D. `import numpy as n`  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** `import numpy as np` is the universal convention.  

**5. You want to represent a simple set of 5 sensor readings as a 1D array. Which code snippet is correct?**  
A. `arr = np.array([10.5, 12.1, 11.8, 13.0, 12.5])`  
B. `arr = np.array(10.5, 12.1, 11.8, 13.0, 12.5)`  
C. `arr = np.array([ [10.5, 12.1], [11.8, 13.0] ])`  
D. `arr = np.array{10.5, 12.1, 11.8, 13.0, 12.5}`  
??? success "Answer"  
    **Answer:** A  
    **Explanation:** 1D arrays use a single set of square brackets `[]`.  

**6. In structural engineering, a stiffness matrix is typically represented as a 2D array. How is a $2 \times 2$ matrix represented using `np.array()`?**  
A. `np.array([1, 2, 3, 4])`  
B. `np.array([[1, 2], [3, 4]])`  
C. `np.array([1, 2], [3, 4])`  
D. `np.array([[1, 2, 3, 4]])`  
??? success "Answer"  
    **Answer:** B  
    **Explanation:** 2D arrays require nested square brackets `[[]]` to represent rows and columns.  

**7. If you have a 2D array representing a table of data (rows and columns), what does the `.ndim` attribute tell you?**  
A. The total number of elements in the array.  
B. The size of each dimension (e.g., 3 rows, 4 columns).  
C. The number of dimensions (e.g., 2 for a matrix).  
D. The data type of the elements (e.g., `float64`).  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** `.ndim` returns the integer number of dimensions.  

**8. You are working with a 3D array (for example, a volumetric stress distribution in a 3D cube). Which of the following best describes the structure of the input list required for `np.array()`?**  
A. A single list of numbers.  
B. A list of lists (a 2D structure).  
C. A list of lists of lists (nested layers).  
D. A dictionary containing lists.  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** A 3D array is essentially a collection of 2D arrays (a list of lists of lists, or a list of cards, where a card is a list of rows and a row is a list of elements).  

**9. Consider the following code: `arr = np.array([[1, 2, 3], [4, 5, 6]])`. What is the result of `arr.shape`?**  
A. `(2,)`  
B. `(3,)`  
C. `(2, 3)`  
D. `(6,)`  
??? success "Answer"  
    **Answer:** C  
    **Explanation:** Shape returns `(rows, columns)`. Here, 2 rows and 3 columns.    

**10. Unlike Python lists, NumPy arrays are "homogeneous." What does this mean?**  
A. All elements in the array must be of the same data type (e.g., all floats).  
B. The array can only contain integers.  
C. The array size cannot be changed once created.  
D. The array only works with positive numbers.  
??? success "Answer"  
    **Answer:** A  
    **Explanation:** Homogeneity (same type) is what allows NumPy to be so fast.  

---

### Answer Key

| Question | Answer | Explanation |
| :--- | :--- | :--- |
| 1 | B | NumPy is built for numerical computing and N-dimensional arrays. |
| 2 | B | Vectorization and contiguous memory allocation make NumPy much faster than lists. |
| 3 | C | `ndarray` is the fundamental object. |
| 4 | C | `import numpy as np` is the universal convention. |
| 5 | A | 1D arrays use a single set of square brackets `[]`. |
| 6 | B | 2D arrays require nested square brackets `[[]]` to represent rows and columns. |
| 7 | C | `.ndim` returns the integer number of dimensions. |
| 8 | C | A 3D array is essentially a collection of 2D arrays (a list of lists of lists). |
| 9 | C | Shape returns `(rows, columns)`. Here, 2 rows and 3 columns. |
| 10 | A | Homogeneity (same type) is what allows NumPy to be so fast. |
