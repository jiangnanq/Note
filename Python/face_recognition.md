## Python face recognition

- Installation (on Raspberry Pi)
    - Incread swap file size, Change 100 to 1024 and Restart swap service
	```bash
	sudo nano /etc/dphys-swapfile
	sudo /etc/init.d/dphys-swapfile stop
	sudo /etc/init.d/dphys-swapfile st
	```
    - Change Boot and RAM split
	```bash
	sudo raspi-config
	```
    - Install dlib on raspberry pi. It will takes about 40 minutes.
	[Reference](https://www.pyimagesearch.com/2017/05/01/install-dlib-raspberry-pi/)
    - Install face_recognition
    - Install open cv, follow [Official guide](https://docs.opencv.org/3.4.1/d2/de6/tutorial_py_setup_in_ubuntu.html)
	    - Install dependencies of opencv
	    - Cmake 
	    ```bash
	    cmake -D OPENCV_EXTRA_EXE_LINKER_FLAGS=-latomic -D ENABLE_PRECOMPILED_HEADERS=OFF  -D CMAKE_CXX_FLAGS=-latomic -D OPENCV_EXTRA_EXE_LINKER_FLAGS=-latomic ..
	    ```
	    - Create symbol link 
	    ```bash
	    ln -s /usr/local/lib/python3.7/site-packages/cv2/python-3.7/cv2.cpython-37m-arm-linux-gnueabihf.so cv2.so
	    ```
	


