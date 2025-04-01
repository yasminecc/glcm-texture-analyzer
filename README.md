# GLCM Texture Analyzer

This C++ program calculates texture features of an image matrix using the Gray Level Co-occurrence Matrix (GLCM). It outputs:
- Contrast
- Energy
- Homogeneity

The user provides a text file containing grayscale image data, and the program generates the GLCM with direction θ = 0 and distance d = 1, then computes normalized values and the texture statistics.

---

## 📂 Files

- `main.cpp` – Full implementation
- `sample-input.txt` – Sample test file with a grayscale matrix
- `report.md` – Step-by-step project explanation, algorithm, and test cases

---

## 🚀 How to Compile & Run

```bash
g++ -o glcm_analyzer main.cpp
./glcm_analyzer
