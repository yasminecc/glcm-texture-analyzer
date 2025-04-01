### **Step 1: Problem Identification and Statement**

Create the GLCM (Gray Level Co-occurrence Matrix) of a given image, using direction θ = 0 and distance d = 1, and compute the following texture statistics:
- Contrast
- Energy
- Homogeneity

These features provide insights into the texture of an image, which are valuable in image analysis and computer vision applications.

---

### **Step 2: Gathering Information**

- **Input**: Grayscale image matrix from a file  
- **Output**: GLCM matrix, normalized matrix, and texture statistics

**Key formulas:**
- **Normalize**:  
  \[ p(i, j) = \frac{M(i, j)}{\sum_{i,j} M(i,j)} \]
- **Contrast**:  
  \[ \sum_{i,j}(i-j)^2 \cdot p(i, j) \]
- **Energy**:  
  \[ \sum_{i,j} p(i,j)^2 \]
- **Homogeneity**:  
  \[ \sum_{i,j} \frac{p(i, j)}{1 + (i - j)^2} \]

---

### **Step 3: Test Cases**

**Test 1:** Random matrix to check GLCM construction and statistics calculation  
5 4 1 1 5 6 8 2 3 5 7 1 4 5 7 1 2 8 5 1 2 5


**Test 2:** Matrix of all zeros  
5 5 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0


**Test 3:** Matrix of zeros with one distinct value  
5 2 0 0 0 0 0 0 0 0 0 6


**Test 4:** Matrix of all ones  
3 3 1 1 1 1 1 1 1 1 1


**Test 5:** File does not exist → should print `file fail` and exit with code -1  
**Test 6:** If user chooses menu option 4 → program prints `exit program` and ends  
**Test 7:** If user enters invalid menu choice → program prints `invalid input...` and re-displays menu  

---

### **Step 4: Algorithm**

1. Prompt user for file name and attempt to open it  
   - If failed, print error and exit  
2. Read number of columns and rows from file  
3. Dynamically allocate 2D array `imdata[row][col]`  
4. Read grayscale values into `imdata`  
5. Determine maximum grayscale value (`graytone`)  
6. Dynamically allocate 2D array `glcm[graytone+1][graytone+1]` and initialize to 0  
7. Show menu with options:
   - **1:** Generate and normalize GLCM  
     - Call `generate(imdata, row, col, glcm)`  
     - Call `normalize(glcm, graytone)` → returns `normalarr`
   - **2:** Compute and display:
     - `contrast(normalarr, graytone)`
     - `energy(normalarr, graytone)`
     - `homogeneity(normalarr, graytone)`
   - **3:** Print GLCM matrix  
   - **4:** Exit
8. Loop menu until user exits  
9. Clean up all dynamically allocated memory

---

### **Function Descriptions**

- **generate(imdata, row, col, glcm)**  
  Updates `glcm[i][j]` counts for pixel pairs in horizontal (θ = 0°) direction.

- **normalize(glcm, graytone)**  
  Normalizes `glcm` values to form a probability matrix `normalarr`.

- **contrast(normalarr, graytone)**  
  Computes contrast using weighted squared difference.

- **energy(normalarr, graytone)**  
  Computes energy as the sum of squared probabilities.

- **homogeneity(normalarr, graytone)**  
  Computes homogeneity considering closeness of values.

---

### **Step 5: Test and Verification**

The above test cases were run, and the outputs for contrast, energy, and homogeneity were verified manually and against expected mathematical behavior. The program handles:
- Edge cases (zero matrices, all same values)
- File read failures
- Menu input validation
