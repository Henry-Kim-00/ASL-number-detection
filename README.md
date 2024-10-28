# ASL-number-detection
Hand detection &amp; ASL number classifier using Mediapipe

# 1) How to run 
This system works in anaconda and jupyter notebook environment. Check the package version. (Opencv-python 4.8.1.78 / mediapipe 0.10.8 / scikit-learn version 1.2.1)

1. Download inference_movie.ipynb file and model.p file. Save them in a directory.
2. To infer the .mp4 file, place the [filename].mp4 file in the directory. Open the inference_movie.ipynb file and modify the line cap = cv2.VideoCapture("./TermProjectSample.mp4") to: cap = cv2.VideoCapture("./filename.mp4")
3. Run the inference_movie.ipynb file.
4. If step 3 went well, you should have a file named /[your_directory_name]/answer/answers.txt. Inside that text file, you'll see the results of the system's hand gesture inference as a number from 1 to 10.

# 2) System overview &amp; idea description
Mediapipe is an open source that provides various machine learning solutions such as object detection, pose landmark detection, hand landmark detection, etc. Hand landmark detection is a program that outputs the coordinates of landmarks on the image when inputting a hand image as shown in Figure [3].

![image](https://github.com/user-attachments/assets/3bb345b6-01cd-47ad-bcd2-87148898808e)

This system is an ASL number recognition program that takes an image of a hand as input, as shown in Figure [4], and first extracts landmark coordinates using Mediapipe's hand landmark detection, and second, classifies the landmark coordinates into numbers 1 to 10 using a multi-layer perceptron (MLP).

![image](https://github.com/user-attachments/assets/4cca6c2b-d453-465d-a00a-e61e0845a8d7)

Below is an overall description of the code that makes up this system.

1. collect_imgs.ipynb \n
Use the OpenCV program to capture the hand sign language images with the built-in camera of the laptop and save them in the ./data folder. In this project, we collected a total of 6000 images.
2. create_dataset.ipynb \n
Extract the hand landmark coordinate values using Mediapipe from the 600 hand images and save them to the data.pickle file along with the label values (1~10). 
3. train_classifier.ipynb \n
Train the MLP using the ./data.pickle file containing the hand landmark coordinate values and label values, and save the MLP model parameters in the ./model.p file. 
4. inference_movie.ipynb \n
This code inferred the hand images in the ./TermProjectSample.mp4 file using the ./model.p file and saved the output values in the ./answer/answers.txt file. Because the .mp4 file is running at 30 FPS and each image lasts 0.5 seconds, there are 15 frames for each image. The inference is performed on each frame, and because saving the output value to the .txt file after each inference saves the same value 15 times, the output value for each of the 15 frames can only be saved once in the . txt file. 
5. inference.ipynb \n
Additionally, I coded code to recognize ASL numbers in real-time with the laptop's built-in camera using OpenCV. I can recognize the laptop user's hand gestures in real-time, which makes it easy to see which hand gestures the model is confused about.

# 3) Results
80% accuracy at TermProjectSample.mp4.
![image](https://github.com/user-attachments/assets/e0154c75-16cd-467a-82bd-df810a9ac3d2)

