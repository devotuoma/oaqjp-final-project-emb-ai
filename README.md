
# Final Project


Emotion Detection Web Application

Overview

This project is an AI-based web application that detects the emotions expressed in a piece of text. It uses IBM Watson NLP's Emotion Predict library to analyze text and identify five core emotions — anger, disgust, fear, joy, and sadness — along with the dominant emotion overall. The application is packaged as a reusable Python module and deployed as a Flask web app.

Features


Detects and scores five emotions (anger, disgust, fear, joy, sadness) from any input text
Identifies the dominant (highest-scoring) emotion
Packaged as an importable Python module (EmotionDetection)
Includes unit tests validating detection across all five emotions
Deployed as a Flask web application with a simple browser-based interface
Handles blank/invalid input gracefully with a clear error message
Passes static code analysis with a perfect Pylint score (10/10)


Project Structure

final_project/
├── EmotionDetection/
│   ├── __init__.py              # Exposes emotion_detector at the package level
│   └── emotion_detection.py     # Core emotion detection logic
├── templates/
│   └── index.html               # Front-end landing page
├── static/
│   └── mywebscript.js           # Front-end JS that calls the Flask endpoint
├── test_emotion_detection.py    # Unit tests for the emotion_detector function
└── server.py                    # Flask server exposing the /emotionDetector endpoint

How It Works


The user enters a sentence into the web interface and submits it.
The front-end JavaScript sends the text to the Flask /emotionDetector endpoint.
emotion_detector() sends the text to the Watson NLP EmotionPredict function via a POST request.
The raw JSON response is parsed to extract scores for anger, disgust, fear, joy, and sadness.
The emotion with the highest score is identified as the dominant emotion.
The result is returned to the browser as a formatted, human-readable sentence.


If the input text is blank or invalid, Watson returns a 400 status code, and the application responds with:

Invalid text! Please try again!

Installation

Ensure you have Python 3 installed, then install the required dependencies:

bashpython3 -m pip install requests flask pylint

Usage

Running the web application

From the final_project directory, start the Flask server:

bashpython3 server.py

The application will be available at:

http://localhost:5000

Enter a sentence in the text box and submit it to see the detected emotions and the dominant emotion.

Using the package directly

The EmotionDetection package can also be imported and used independently of the web app:

pythonfrom EmotionDetection import emotion_detector

result = emotion_detector("I love this new technology.")
print(result)

Example output:

python{
    'anger': 0.0136,
    'disgust': 0.0017,
    'fear': 0.0090,
    'joy': 0.9719,
    'sadness': 0.0552,
    'dominant_emotion': 'joy'
}

Running Unit Tests

Unit tests validate that the correct dominant emotion is returned for five representative statements (joy, anger, disgust, sadness, and fear).

bashpython3 test_emotion_detection.py

A successful run ends with:

Ran 1 test in X.XXXs

OK

Static Code Analysis

The server.py file follows PEP 8 standards and includes docstrings for the module and all functions, achieving a perfect Pylint score.

bashpylint server.py

Expected output:

Your code has been rated at 10.00/10

Error Handling

Submitting blank or invalid text does not crash the application. Instead:


emotion_detector() detects a 400 status code from the Watson service and returns a dictionary with all values set to None.
server.py checks for a None dominant emotion and returns a friendly message instead of attempting to format missing data.


Technologies Used


Python 3
Flask – web framework for serving the application
Requests – for making HTTP calls to the Watson NLP service
IBM Watson NLP Library (Emotion Predict) – for emotion analysis
Pylint – for static code analysis and code quality
unittest – for automated testing


Notes


This project was built as part of an IBM Skills Network course on AI-based application development and deployment.
The Watson NLP Emotion Predict service is embedded in the lab environment and does not require a separate API key when running within that environment.
