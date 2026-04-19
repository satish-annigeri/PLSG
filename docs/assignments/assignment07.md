# Assignment 7

#### Corresponds to: [Session 7](../sessions/session07.md)

### Quiz: NumPy Arrays - Creation, Basic Operations

**Time Allotted:** 45 Minutes  

**1. You have a list of material Young's Moduli: `E_values = [210e9, 70e9, 200e9]`. To convert this list into a NumPy array for performing calculations, which command is correct?**

A. `np.create_array(E_values)`  
B. `np.array(E_values)`  
C. `np.convert(E_values)`  
D. `np.list_to_array(E_values)`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** The `np.array()` function is the standard NumPy method used to convert an existing Python list or tuple into a NumPy array.  


**2. You are initializing a 4x4 global stiffness matrix and want the matrix to be pre-filled with zeros. Which command is the correct syntax?**

A. `np.zeros(4, 4)`  
B. `np.zeros_matrix(4, 4)`  
C. `np.zeros((4, 4))`  
D. `np.empty_zeros(4, 4)`  
??? success "Answer"
    **Answer: C**  

    **Explanation: The `np.zeros()` function expects the shape of the array as a single argument, which must be passed as a tuple, such as `(rows, columns)`.**  


**3. You use the command `stress_tensor = np.empty((3, 3))` to allocate memory for a 3x3 stress tensor. What can you expect regarding the initial values within this array?**

A. All values will be 0.0  
B. All values will be 1.0  
C. The values will be arbitrary values remaining in the memory location  
D. All values will be NaN  
??? success "Answer"
    **Answer: C**  

    **Explanation:** `np.empty()` allocates memory without initializing the elements to any specific value, meaning the array will contain whatever data was previously stored in those memory addresses.  


**4. You have a 1D array containing the stiffnesses of three springs: `k = np.array([500, 1200, 800])`. Which function will create a 3x3 diagonal matrix with these specific values on the main diagonal?**

A. `np.diag(k)`  
B. `np.diagonal(k)`  
C. `np.matrix_diag(k)`  
D. `np.create_diag(k)`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** `np.diag()` is used to extract a diagonal or, when passed a 1D array, construct a 2D array with the input values on the main diagonal.  


**5. You need to create a 1D array of length 6 where every element is exactly 1.0. Which command is the most efficient way to achieve this?**

A. `np.all_ones(6)`  
B. `np.ones(6)`  
C. `np.identity(6)`  
D. `np.array(1, 6)`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** `np.ones(shape)` is the built-in NumPy function specifically designed to create an array of a given shape filled entirely with the value 1.0.

**6. You want to create a 1D array that starts at 0 and increments by 5, up to but NOT including 20. Which command is correct?**

A. `np.arange(0, 20, 5)`  
B. `np.arange(0, 25, 5)`  
C. `np.linspace(0, 20, 5)`  
D. `np.arange(5, 20, 5)`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** The `np.arange(start, stop, step)` function generates values within the half-open interval `[start, stop)`. Therefore, `np.arange(0, 20, 5)` will produce `[0, 5, 10, 15]`, but will not include 20.  


**7. A structural engineer needs to create exactly 11 equally spaced points between 0 and 10 meters to represent nodes on a beam. Which command is most appropriate?**

A. `np.arange(0, 10, 11)`  
B. `np.linspace(0, 10, 11)`  
C. `np.linspace(0, 11, 10)`  
D. `np.arange(0, 11, 10)`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** `np.linspace(start, stop, num)` is used when you know the specific number of points (`num`) you want to generate between two values. To get 11 points including both 0 and 10, `np.linspace(0, 10, 11)` is the correct choice.  


**8. You have a 1D array of 12 load values. You want to convert this into a matrix with 3 rows and 4 columns, without altering the original 1D array. Which command performs this transformation?**

A. `loads.reshape(4, 3)`  
B. `loads.reshape(3, 4)`  
C. `loads.resize(3, 4)`  
D. `loads.reshape(12, 1)`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** The `reshape(rows, columns)` method reorganizes the existing elements into a new shape. For a 12-element array to become a 3x4 matrix, the dimensions must be specified as `(3, 4)`. Note the `loads.resize(3, 4)` converts the original 1D array `loads` 1D array to `3x4` **in-place**.  


**9. What is a primary difference between `np.reshape()` and `np.resize()` when the new dimensions do not contain the same number of elements as the original array?**

A. `reshape()` will change the original array, while `resize()` will not.  
B. `reshape()` will raise an error, while `resize()` will pad the array or repeat elements to fill the new shape.  
C. `resize()` only works on 1D arrays, while `reshape()` works on any dimension.  
D. There is no difference; they are aliases for the same function.  
??? success "Answer"
    **Answer: B**  

    **Explanation:** `reshape()` is strict; it requires that the total number of elements remains constant, otherwise it raises a `ValueError`. In contrast, `resize()` can change the size of the array by padding it with zeros or repeating data to match the requested shape.  


**10. Which code sequence correctly creates a 2x2 matrix where the elements are [1.0, 2.0, 3.0, 4.0]?**

A. `np.linspace(1, 4, 4).reshape(2, 2)`  
B. `np.arange(1, 4, 4).reshape(2, 2)`  
C. `np.linspace(1, 4, 2).reshape(2, 2)`  
D. `np.arange(1, 5, 2).reshape(2, 2)`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** `np.linspace(1, 4, 4)` generates the four values `[1.0, 2.0, 3.0, 4.0]`. Calling `.reshape(2, 2)` on this array successfully organizes them into two rows and two columns.


**11. You have a 1D array representing a load vector: `load = np.array([10, 20, 30])`. You need to apply a load factor of 1.5 to all loads. Which command is correct?**

A. `load @ 1.5`  
B. `load * 1.5`  
C. `load . 1.5`  
D. `np.scalar(load, 1.5)`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** Multiplication with a scalar in NumPy applies the operation to every single element in the array.  


**12. You are given two load vectors: `P1 = np.array([100, 50])` and `P2 = np.array([20, 30])`. To find the total resultant load vector, which command should you use?**

A. `P1 * P2`  
B. `P1 @ P2`  
C. `P1 + P2`  
D. `np.combine(P1, P2)`  
??? success "Answer"
    **Answer: C**  

    **Explanation:** Addition in NumPy performs element-wise addition, meaning the first element of `P1` is added to the first element of `P2`, and so on.  


**13. You have two arrays of stress values: `stress_initial = np.array([250, 300])` and `stress_final = np.array([270, 310])`. To find the change in stress (final - initial), which command is correct?**

A. `stress_final - stress_initial`  
B. `stress_final / stress_initial`  
C. `stress_final @ stress_initial`  
D. `np.diff(stress_final, stress_initial)`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** Subtraction in NumPy is an element-wise operation that subtracts the elements of the second array from the corresponding elements of the first array.  


**14. You have an array of material stiffnesses `k = np.array([100, 200, 300])` and an array of reduction factors `f = np.array([0.9, 0.8, 0.7])`. To find the reduced stiffnesses by multiplying each stiffness by its corresponding factor, which command is correct?**

A. `k @ f`  
B. `k * f`  
C. `np.matrix_mult(k, f)`  
D. `k . f`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** The `*` operator in NumPy performs element-wise multiplication. This is required when you want to multiply elements at the same index.  


**15. In structural analysis, you often need to solve the equation `F = K @ u`, where `K` is a stiffness matrix and `u` is a displacement vector. Which operator is used to perform this matrix-vector multiplication?**

A. `*`  
B. `^`  
C. `@`  
D. `&`  
??? success "Answer"
    **Answer: C**  

    **Explanation:** The `@` operator is specifically designated for matrix multiplication (the dot product of matrices) in modern Python/NumPy.  


**16. If `A` and `B` are two NumPy arrays of the same shape, what is the primary difference between the results of `A * B` and `A @ B`?**

A. `A * B` performs matrix multiplication, while `A @ B` performs element-wise multiplication.  
B. `A * B` performs element-wise multiplication, while `A @ B` performs matrix multiplication.  
C. `A * B` results in a scalar, while `A @ B` results in an array.  
D. There is no difference; both operators perform the same operation.  
??? success "Answer"
    **Answer: B**  

    **Explanation:** This is a fundamental distinction in NumPy: `*` is for element-wise operations, while `@` is for matrix/dot product operations.  


**17. You have a $3 \times 3$ stiffness matrix `K` and you want to add a constant offset (increase in value) of 5.0 to every single element in the matrix. Which command achieves this?**

A. `K + 5.0`  
B. `np.add(K, [5, 5, 5])`  
C. `K @ 5.0`  
D. `K * 5.0`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** This is an example of "broadcasting," where NumPy allows a scalar to be added to every element of an array automatically.  


**18. To perform matrix multiplication between matrix `A` and matrix `B` using the `@` operator, what is the requirement regarding their dimensions?**

A. `A` and `B` must have exactly the same dimensions (e.g., both must be $3 \times 3$).  
B. The number of columns in `A` must equal the number of rows in `B`.  
C. The number of rows in `A` must equal the number of columns in `B`.  
D. Both `A` and `B` must be 1D arrays.  
??? success "Answer"
    **Answer: B**  

    **Explanation:** For matrix multiplication $(m \times n) \times (n \times p)$, the "inner" dimensions (the columns of the first and the rows of the second) must match.  


**19. If you multiply a $2 \times 3$ matrix by a $3 \times 2$ matrix using the `@` operator, what will be the shape of the resulting matrix?**

A. $3 \times 3$  
B. $2 \times 2$  
C. $3 \times 2$  
D. $2 \times 3$  
??? success "Answer"
    **Answer: B**  

    **Explanation:** When multiplying an $(m \times n)$ matrix by an $(n \times p)$ matrix, the resulting shape is $(m \times p)$. Here, $(2 \times 3) @ (3 \times 2)$ results in a $2 \times 2$ matrix.  


**20. You have a 1D array `v = np.array([1, 2, 3])`. What is the result of the operation `v * 2`?**

A. `[2, 4, 6]`  
B. `[1, 2, 3, 1, 2, 3]`  
C. `[2, 2, 2]`  
D. `[1, 4, 9]`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** Multiplying a 1D array by a scalar results in each element of the array being multiplied by that scalar.


**21. You have a 1D array of nodal displacements: `u = np.array([0.01, 0.02, 0.03, 0.04, 0.05])`. To access the third displacement (0.03), which index should you use?**

A. `u[3]`  
B. `u[2]`  
C. `u(2)`  
D. `u[1]`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** Python uses zero-based indexing, meaning the first element is at index 0, the second at index 1, and the third at index 2.  


**22. You are working with a 2x2 stiffness matrix `K = np.array([[10, 20], [30, 40]])`. Which command correctly retrieves the value 20?**

A. `K[0, 1]`  
B. `K[1, 0]`  
C. `K[0, 0]`  
D. `K[1, 1]`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** In a 2D array, the first index refers to the row and the second to the column. The value 20 is in the first row (index 0) and the second column (index 1).  


**23. You have a list of sensor readings: `readings = np.array([12, 15, 18, 22, 25])`. You want to quickly access the very last reading in the array using negative indexing. Which command is correct?**

A. `readings[-0]`  
B. `readings[last]`  
C. `readings[-1]`  
D. `readings[0]`  
??? success "Answer"
    **Answer: C**  

    **Explanation:** Negative indexing in Python starts from the end of the array, where `-1` refers to the last element, `-2` to the second to last, and so on.  


**24. Given a 3x3 matrix `M`, you want to extract the entire second row. Which of the following is the correct syntax?**

A. `M[1, :]`  
B. `M[2, :]`  
C. `M[:, 1]`  
D. `M[1]`  
??? success "Answer"
    **Answer: D**  

    **Explanation:** While `M[1, :]` is also a valid way to select the second row in NumPy, `M[1]` is a shorthand specifically used to access the element at the first dimension (the row).  


**25. You have a displacement vector `v = np.array([10, 20, 30, 40])`. If you want to access the element 40 using its index, which is correct?**

A. `v[4]`  
B. `v[3]`  
C. `v[-2]`  
D. `v[0]`  
??? success "Answer"
    **Answer: B**  

    **Explanation: Since the array has 4 elements, the indices are 0, 1, 2, and 3. Therefore, the fourth element is at index 3.**  


**26. You have an array of temperature readings: `temp = np.array([20, 21, 22, 23, 24, 25])`. Which slicing command will return the sub-array `[21, 22, 23]`?**

A. `temp[1:3]`  
B. `temp[2:4]`  
C. `temp[1:4]`  
D. `temp[0:3]`  
??? success "Answer"
    **Answer: C**  

    **Explanation:** Slicing syntax `[start:stop]` includes the start index but excludes the stop index. To get indices 1, 2, and 3, you must use `1:4`.  


**27. You want to select every second element from an array `arr = np.array([10, 20, 30, 40, 50, 60])` to perform a downsampling. Which command should you use?**

A. `arr[::2]`  
B. `arr[1:2]`  
C. `arr[::1]`  
D. `arr[2::1]`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** The slicing syntax `[start:stop:step]` allows for a step value. Using `::2` tells NumPy to start from the beginning and take every second element.  


**28. You have a 3x3 global stiffness matrix `K`. You want to extract the top-left 2x2 sub-matrix. Which command is correct?**

A. `K[0:2, 0:2]`  
B. `K[1:3, 1:3]`  
C. `K[0:1, 0:1]`  
D. `K[:2, :2]`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** `K[0:2, 0:2]` selects rows 0 and 1, and columns 0 and 1, which constitutes the top-left 2x2 portion of the matrix. (Note: D is also technically correct, but A is the most explicit form).  


**29. Given a matrix `M = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])`, how do you extract only the last column?**

A. `M[2, :]`  
B. `M[:, 2]`  
C. `M[:, -1]`  
D. Both B and C  
??? success "Answer"
    **Answer: D**  

    **Explanation:** In NumPy, `[:, 2]` selects all rows from the column at index 2, and `[:, -1]` selects all rows from the last column. Both achieve the same result here.  


**30. You need to reverse the order of elements in a 1D array `data = np.array([1, 2, 3, 4, 5])`. Which slicing technique is the most efficient way to do this?**

A. `data[5:0:-1]`  
B. `data[::-1]`  
C. `data[1::-1]`  
D. `data[::1]`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** The slice `[::-1]` uses a step of -1, which tells Python to traverse the array backwards from the end to the beginning.


**31. You have an array of stress values: `stress = np.array([150, 250, 350, 450])`. You want to create a new array containing only the values that exceed the yield strength of 300 MPa. Which command uses a mask to achieve this?**

A. `stress.filter(stress > 300)`  
B. `stress[stress > 300]`  
C. `np.select(stress > 300)`  
D. `stress[where > 300]`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** Boolean masking allows you to pass a condition directly into the square brackets. The condition `stress > 300` creates a boolean array (a mask), and NumPy uses it to return only the elements where the condition is `True`.  


**32. You are checking nodal displacements in a structure. You need to find all displacements `d` that are both greater than 0.01 and less than 0.05. Which syntax correctly applies this double-condition mask?**

A. `d[d > 0.01 and d < 0.05]`  
B. `d[(d > 0.01) & (d < 0.05)]`  
C. `d[(d > 0.01) and (d < 0.05)]`  
D. `d[d.between(0.01, 0.05)]`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** When using multiple conditions in a NumPy mask, you must use the bitwise operator `&` (for AND) or `|` (for OR) instead of the Python keywords `and` or `or`. Additionally, each condition must be enclosed in parentheses to ensure correct operator precedence.  


**33. You have two 1D arrays representing load components: `load_x = np.array([10, 20])` and `load_y = np.array([30, 40])`. To combine them into a single 1D array `[10, 20, 30, 40]`, which command is correct?**

A. `np.concatenate((load_x, load_y))`  
B. `np.concatenate(load_x, load_y)`  
C. `np.concat([load_x, load_y])`  
D. `np.merge(load_x, load_y)`  
??? success "Answer"
    **Answer: A**  

    **Explanation:** The `np.concatenate()` function requires the arrays to be passed as a single sequence, such as a tuple `(a, b)` or a list `[a, b]`.  


**34. You have two $2 \times 3$ matrices, `A` and `B`. You want to stack them vertically to create a single $4 \times 3$ matrix. Which command should you use?**

A. `np.concatenate((A, B), axis=1)`  
B. `np.concatenate((A, B), axis=0)`  
C. `np.concatenate((A, B))`  
D. Both B and C  
??? success "Answer"
    **Answer: D**  

    **Explanation:** By default, `np.concatenate()` operates on `axis=0` (rows), which stacks arrays vertically. Therefore, both specifying `axis=0` and leaving it as the default will result in a $4 \times 3$ matrix.  


**35. You have two $2 \times 2$ matrices, `M1` and `M2`. You want to join them side-by-side (horizontally) to result in a $2 \times 4$ matrix. Which command is correct?**

A. `np.concatenate((M1, M2), axis=0)`  
B. `np.concatenate((M1, M2), axis=1)`  
C. `np.concatenate((M1, M2), axis=2)`  
D. `np.concatenate((M1, M2), axis=horizontal)`  
??? success "Answer"
    **Answer: B**  

    **Explanation:** To concatenate arrays horizontally (increasing the number of columns), you must specify `axis=1`.