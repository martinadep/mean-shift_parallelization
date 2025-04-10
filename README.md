# Mean-Shift Parallelization
A parallel implementation of the Mean-Shift algorithm applied 
to image segmentation. This project optimizes the performance 
of the Mean-Shift algorithm through parallelization techniques, 
enabling more efficient and scalable image segmentation.

## Technical Background
Mean-Shift is a non-parametric density-based clustering algorithm 
used in computer vision and machine learning. In this project, the 
algorithm is applied to image segmentation, a process that divides 
an image into multiple uniform regions, making the image easier to analyze.

The parallel version implemented in this project leverages 
modern multi-core architectures to significantly accelerate 
processing while maintaining the quality of segmentation results.

## Examples
![asto](examples/sample_astro.jpg)
![astoB10](docs/astro_B10.jpg)
![astoB30](docs/astro_B30.jpg)
![flower](examples/sample_flower.jpg)
![flowerB10](docs/flower_B10.jpg)
![flowerB40](docs/flower_B40.jpg)


## Prerequisites
- A C++ compiler compatible with C++11 or higher (GCC, Clang, or MSVC)
- Python 3.12 with required packages (NumPy, pandas)
- Optional, [CMake](https://cmake.org/download/) (version 3.10 or higher)

## Complete Workflow - example
The following steps use default example configurations defined in `config.py`.
However, arguments can be configured to customize the execution as shown [below](#complete-workflow---custom).

1. **Clone** the repository:

   ```bash
   git clone https://github.com/martinadep/meanshift_parallelization
   cd meanshift_parallelization
   ```

2. **Convert input image to CSV** format:

   ```bash
   python .\py_utils\img_to_csv.py
   ```
  
   This will generate a CSV file that will be processed by the C++ program.

3. **Run the Mean-Shift algorithm**:
   - **Using CMake from command line**:
      
      On Windows (MinGW):
     ```bash
     cmake -G "MinGW Makefiles" -B build
     cmake --build build
     ./mean_shift_segmentation.exe
     ```

      On Linux/macOS:
     ```bash
     cmake -B build
     cmake --build build
     ./mean_shift_segmentation.exe
     ```

   This will process the CSV file and generate a new output CSV file.

4. **Convert the output CSV** back to an image:

   ```bash
   python .\py_utils\csv_to_img.py
   ```

   This will transform the processed data back into a ***segmented image***.


## Complete Workflow - custom
The following steps allows to configure the input image path and enables Mean-Shift bandwidth and kernel selection

1. **Clone** the repository:

   ```bash
   git clone https://github.com/martinadep/meanshift_parallelization
   cd meanshift_parallelization
   ```

2. **Convert input image to CSV** format:

   You can specify the input image and output CSV file paths by providing arguments in the command line:

   ```bash
   python .\py_utils\img_to_csv.py -i image.jpg -o output.csv
   ```

   This will generate a CSV file that will be processed by the C++ program.

3. **Run the Mean-Shift algorithm**:
   - **Using CMake from command line**:
      
      On Windows using MinGW:
     ```bash
     cmake -G "MinGW Makefiles" -B build
     cmake --build build
     ```

      On Linux/macOS:
     ```bash
     cmake -B build
     cmake --build build
     ```

   You can specify the bandwidth, and the input and output CSV file paths, by providing arguments in the command line:
   ```bash
   ./mean_shift_segmentation.exe [bandwidth] [input.csv] [output.csv]
     ```

   This will process the CSV file and generate a new output CSV file.

4. **Convert the output CSV** back to an image:
   
   You can specify the output image and input CSV file paths by providing arguments in the command line:

   ```bash
   python .\py_utils\img_to_csv.py -i input.csv -o image.jpg
   ```

   This will transform the processed data back into your ***segmented image***.

## Project Structure

```
.
├── CMakeLists.txt
├── src/
│   ├── include/
│   │    ├── point.hpp
│   │    ├── cluster.hpp
│   │    └── mean_shift.hpp
│   └── main.cpp
├── examples/
│   ├── sample_flower.jpg
│   └── sample_astro.jpg
├── py_utils/
│   ├── config.py
│   ├── csv_to_img.py
│   └── img_to_csv.py
├── data/
├── docs/ 
└── README.md
```

## Performance

The parallel version of the algorithm offers significant performance improvements over the sequential version, especially for large images:

| Image Size | Sequential Version | Parallel Version | Speedup |
|------------|-------------------|-----------------|---------|
| ...        | x.xx seconds      | x.xx seconds    | x.xx    |
| ...        | x.xx seconds      | x.xx seconds    | x.xx    |
| ...        | x.xx seconds      | x.xx seconds    | x.xx    |
