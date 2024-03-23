
# Project Title

Handwritten Math Equation Solver

## Authors

- [@RF-UV-11](https://github.com/RF-UV-11)


## Overview

This project aims to develop a handwritten math equation solver application. The application takes handwritten math equations as input, processes them using image segmentation and deep learning models, and returns the solved equation. The project primarily utilizes the EMNIST dataset for character recognition and a custom dataset of images for math symbols.
## Roadmap
![RoadMap](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/Images/Roadmap.png)

1. **Problem Identification:**
   - Recognize the challenge of solving handwritten math expressions, necessitating accurate character recognition to decipher equations effectively.

2. **Handwritten Character Recognition:**
   - Employ the ``EMNIST dataset``, covering both handwritten alphabets and digits, as it provides a comprehensive foundation for character recognition.
   - Develop a custom CNN model, ensuring high accuracy (``99.4%``), which is crucial for precise identification of handwritten characters in math expressions.

   ![Handwritten Character Recognition](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/Images/Screenshot%202024-03-21%20170451.png)

3. **Math Symbol Dataset Integration:**
   - Incorporate images of math symbols (e.g., ``"+", "-", "(", ")"``) to expand recognition capabilities beyond characters.
   - Merge datasets into various formats ([`image`](https://www.kaggle.com/datasets/yuvrajjoshi1110/balanced-emnist-maths-symbol-dataset), [`CSV`](https://www.kaggle.com/datasets/yuvrajjoshi1110/shuffled-digit-char-symbol-merged-dataset) , `idx3 ubyte`) for flexibility, enabling users to choose the format that best suits their requirements.

4. **Modeling:**
   - Initially explore [`MobileNetV3 small model`](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/mobilenetv3-handwritten-char-math-symbol-recotion.ipynb) for its efficiency and speed, achieving moderate accuracy (`84-90%`) suitable for preliminary testing.

   - Further refine modeling with a [`Custom CNN`](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/handwritten-char-math-symbol-cnn.ipynb) approach, achieving superior accuracy (``97% training, 93% testing``) necessary for robust recognition in diverse handwriting styles.
    ![Handwritten Character Math Symbol Recognition Training](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/Images/Screenshot%202024-03-21%20170714.png)

    ![Handwritten Character Math Symbol Recognition Loss](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/Images/Screenshot%202024-03-21%20170725.png)


5. **Deployment for Equation Solving:**
   - Implement segmentation to isolate individual characters within handwritten equations, facilitating accurate character recognition.
   - Utilize trained models to predict characters, enabling the translation of handwritten equations into digital format.

6. **Equation Solving with Wolfram Alpha:**
   - Integrate ``Wolfram Alpha`` for its comprehensive computational capabilities, enabling accurate and efficient solution generation for predicted equations.
   - Provide an alternative custom logic option for equation solving, allowing flexibility based on user preferences or specific requirements.

7. **Future Work - Flutter Application Development:**
   - Develop a ``Flutter application`` to enhance user accessibility and interaction with the handwritten math equation solver.
   - Leverage Flutter's cross-platform compatibility and intuitive UI framework to create a seamless user experience.
   - Integrate backend functionalities for image processing and communication with Wolfram Alpha or custom equation solving logic, ensuring efficient and reliable equation solving capabilities.
   - Enhance user experience with ``real-time feedback`` and ``error handling`` features, optimizing usability and reliability of the application.


## Dataset
#### [EMNIST](https://www.kaggle.com/datasets/crawford/emnist)
#### [MATH SYMBOL](https://www.kaggle.com/datasets/yuvrajjoshi1110/math-symbol/code)


## Model

#### MobileNetV3
![App Screenshot](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/Images/MobileNetV3.png)

#### Custom Final CNN 
![App Screenshot](https://github.com/RF-UV-11/Handwritten-Math-Equation-Solver/blob/main/Handwritten-Math-Equation-Solver/Images/CNN_Model_EMNIST.png)
## Segmentizer

The `image_segmentation` function provided here serves as a crucial component of the handwritten math equation solver project. It performs the segmentation of handwritten text from input images, enabling the extraction of individual characters for further processing and recognition.

### Functionality
1. **Image Preprocessing**: The input image is preprocessed by resizing it to a standard width while maintaining aspect ratio. Adaptive thresholding is applied to binarize the image, making text regions more distinguishable.
2. **Noise Removal**: Morphological operations are employed to remove noise from the binarized image, enhancing the quality of segmentation.
3. **Character Segmentation**: Text lines are identified by analyzing the distribution of white pixels along the vertical axis. Lines are then separated, forming bounding boxes around individual characters.
4. **Character Extraction**: Contours are detected within each text line, and bounding rectangles are drawn around them. These rectangles represent individual characters segmented from the input image.

### Usage
- Ensure the `image_segmentation` function is properly imported and called with the filepath of the input image.
- Adjust parameters such as kernel size, normalized mean, and contour area threshold as needed for optimal segmentation performance.
- Review the output directory for the segmented image (`segmented_image.jpg`) containing annotated character bounding boxes.

### Example
```python
image_segmentation('/path/to/input/image.jpg')
```

### Dependencies
- OpenCV (`cv2`)
- NumPy

### Note
- This segmentation algorithm assumes handwritten text is primarily horizontally aligned. Adjustments may be required for images with skewed or rotated text.

### Future Improvements
- Enhance noise removal techniques to handle complex backgrounds or noisy input images.
- Implement advanced text line detection algorithms for improved segmentation accuracy.
- Explore deep learning-based approaches for character segmentation and recognition in handwritten text.

This segmentizer function forms a fundamental component of the handwritten math equation solver, facilitating the extraction and processing of handwritten text inputs.
## Custom Check Fucntion

### Custom Segmentation Function: `chek()`

In the process of segmenting handwritten text for recognition within the handwritten math equation solver project, a custom function named `chek()` is introduced. This function plays a crucial role in handling specific symbols such as division and the equal sign. Due to their unique segmentation requirements, these symbols are separated into distinct segments before being passed to the recognition model. This ensures accurate interpretation and processing of handwritten math equations.

### Functionality
- **Symbol Segmentation**: `chek()` function identifies and separates the division and equal sign symbols from the rest of the handwritten text segments.
- **Custom Handling**: By isolating these symbols, the function ensures that they are processed appropriately, accounting for their distinct visual characteristics and spatial arrangements.
- **Enhanced Recognition**: Segregating division and equal sign symbols prior to recognition helps improve the accuracy of the overall equation solving process, preventing misinterpretation and errors.

### Usage
- Integrate the `chek()` function into the segmentation pipeline after initial character segmentation.
- Call the function to identify and separate division and equal sign symbols from other text segments.
- Pass the segmented symbols, including divisions and equal signs, to the recognition model for accurate processing.

### Example
```python
# After initial character segmentation
# Call the chek() function to handle division and equal sign symbols
division_symbol, equal_sign_symbol, other_segments = chek(segmented_symbols)
```

### Dependencies
- None

### Note
- The `chek()` function assumes a specific segmentation strategy tailored to the handwritten math equation solver project's requirements.
- Adjustments may be necessary based on the complexity and variability of handwritten text inputs.

### Future Improvements
- Explore advanced symbol detection and segmentation techniques to further enhance the accuracy and robustness of the custom function.
- Integrate machine learning or deep learning approaches for automatic symbol recognition and segmentation in handwritten equations.

By incorporating the `chek()` function into the segmentation pipeline, the handwritten math equation solver project achieves more accurate and reliable recognition of division and equal sign symbols, contributing to the overall effectiveness and usability of the application.

## Wolfram Alpha API

The handwritten math equation solver application integrates with the Wolfram Alpha computational engine to provide accurate and comprehensive solutions to user queries. This section outlines the usage of the `wolframalpha` Python module for querying Wolfram Alpha and retrieving answers to user questions.

### Functionality
- **Wolfram Alpha API Integration**: The application utilizes the `wolframalpha` module to interact with Wolfram Alpha's computational engine via its API.
- **Answer Retrieval**: User queries are sent to Wolfram Alpha, and the resulting answers are retrieved and displayed within the application.
- **Error Handling**: The application gracefully handles any errors or invalid input during the query process, ensuring a smooth user experience.

### Usage
1. **Wolfram Alpha App ID**: Obtain a Wolfram Alpha app ID by signing up for an API account on the Wolfram Alpha website. Replace `'API'` in the code snippet with your actual Wolfram Alpha app ID.
2. **Input Question**: Run the provided Python script, and it will prompt you to input a question.
3. **Answer Display**: After inputting the question, the script will fetch the answer from Wolfram Alpha and display it for the user.

### Example Code
```python
# Importing the wolframalpha module
import wolframalpha

# Define a function to find answers
def find_answer(question):
    """This function will return the answer
    for the input query from the users"""

    # Replace 'E3RYX3-G73QUJ4VY7' with your actual Wolfram Alpha app ID
    app_id = 'API'

    # Create an object of the Client() class using the APP ID
    the_client = wolframalpha.Client(app_id)

    # Query Wolfram Alpha with the input question
    response = the_client.query(question)

    # Extract the answer text from the response
    answer = next(response.results).text

    # Return the answer
    return answer

# Main function
if __name__ == '__main__':

    # Prompt the user to input a question
    question = input("Question: ")

    # Retrieve the answer using the find_answer() function
    answer = find_answer(question)

    # Display the answer for the user
    print("Answer:", answer)
```

### Dependencies
- `wolframalpha` Python module
- Python 3.x

### Note
- Ensure you have a stable internet connection while running the script, as it relies on the Wolfram Alpha API for retrieving answers.
- Be mindful of Wolfram Alpha's API usage policies and any associated usage limits or restrictions.

By leveraging Wolfram Alpha's computational capabilities, the handwritten math equation solver application provides users with accurate and reliable answers to a wide range of queries, enhancing its utility and effectiveness in solving mathematical problems.

