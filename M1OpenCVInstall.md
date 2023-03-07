# Install OpenCV on M1
Summary and clean up from this [blog](https://opencv.org/opencv-python-for-apples-m1-chip-a-detective-story-with-a-happy-ending/)
## Requirement

1. Homebrew
2. [pyenv](https://github.com/pyenv/pyenv) (python version management)

## Installation

### Install Python & Python packagees

1. clone OpenCV [repository](https://github.com/opencv/opencv) in your default terminal
2. install python 3.9 - `pyenv install 3.9.5`
3. set active version of python to 3.9.5 - `pyenv local 3.9.5`
4. make pip is up to date - `python3 -m pip install --upgrade pip`
5. install python packages - `python3 -m pip install numpy`

### Create a build directory and run cmake

1. find those three paths
    - PYTHON3_EXECUTABLE
    - PYTHON3_INCLUDE_DIR
    - PYTHON3_NUMPY_INCLUDE_DIRS
        
        run - `pyenv which python3` 
        
        my path is: /Users/username/.pyenv/versions/3.9.5/bin/python3
        
        run - `python3-config --includes`
        
        my path is :I/Users/username/.pyenv/versions/3.9.5/include/python3.9 -I/Users/username/.pyenv/versions/3.9.5/include/python3.9
        
        run - `python3 -c "import numpy; print(numpy.get_include())”`
        
        my path is: /Users/username/Library/Python/3.9/lib/python/site-packages/numpy/core/include
        
2. create build directory - `mkdir opencv_build`
3. redirect to opencv_build - `cd opencv_build`
4. run cmake 
    
    `cmake -DPYTHON3_EXECUTABLE=$(pyenv which python3) \
    -DPYTHON3_INCLUDE_DIR=~/.pyenv/versions/3.9.5/include/python3.9 \
    -DPYTHON3_NUMPY_INCLUDE_DIRS=~/Library/Python/3.9/lib/python/site-packages/numpy/core/include \
    ../opencv`
    
5. build with cmake - `cmake --build . -j8`