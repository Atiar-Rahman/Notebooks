## Activity diagram:

---------
This activity diagram explains how the AI-Based Suspicious Activity Detection System works from login to alert generation.

First, the operator logs into the system by entering valid credentials. The frontend sends these details to the Django backend, where the user is authenticated using JWT tokens. If the credentials are incorrect, an error message is displayed. Otherwise, access is granted and the dashboard is loaded.

Next, the operator selects a camera feed, and the live video stream is sent for analysis. The backend forwards the stream to the AI model, where frame sequences are processed using CNN-LSTM or 3D CNN techniques to detect suspicious activities.

If no suspicious activity is found, the system simply shows the status as normal. However, if suspicious activity is detected, the AI classifies it as suspicious, stores the activity logs in the database, and generates an alert.

Finally, the system triggers alert services such as email notifications and sound alarms, while displaying the alert on the dashboard for the operator to take action.

Overall, this workflow demonstrates an automated and intelligent real-time surveillance and alert system.

----------
## Sequence Diagram
-------

This sequence diagram shows how the Suspicious Activity Detection System works step by step. First, the user logs in through the React frontend, and the Django backend authenticates the user using JWT tokens with the database.

After successful login, the video stream starts and video frames are sent to the AI model for analysis. The AI model checks for suspicious activity and returns the result.

If suspicious activity is detected, the system stores the detection log in the database and sends an alert to the frontend, where the operator sees a critical warning. Otherwise, the system continues normal monitoring.

Overall, this diagram explains the real-time communication between the frontend, backend, AI model, and database.

---------
## Database Schema diagram

----------

This schema diagram presents the database structure for a Suspicious Activity Detection system in CCTV footage. The system is designed to manage users, cameras, alerts, detections, and permissions efficiently.

At the center of the schema is the users_user table, which stores user information such as email, password, contact details, and account status. This table connects to several other modules, including cameras, reviews, and alerts.

The camerss_camera table manages CCTV camera information and links each camera to a specific user. Suspicious activity predictions are stored in the detection_videoprediction table, which contains detection results, timestamps, and extracted frames from the video footage.

The alert_alert table is responsible for generating alerts whenever suspicious activity is detected. It stores alert details, confidence levels, and timestamps for monitoring purposes.

Additionally, the schema includes authentication and authorization tables such as permissions, user groups, and admin logs to ensure secure system access and activity tracking.

Overall, this database schema provides a structured and scalable foundation for real-time CCTV surveillance and suspicious activity detection systems.

----------
## Development steps

-----
This diagram shows the implementation steps of our AI-Based Suspicious Activity Detection System. The project is divided into three main parts: Model Development, Backend Development, and Frontend Development.

In the model section, we first collected and preprocessed datasets, then trained and evaluated the AI model before integrating it with the backend system.

In the backend section, we set up the Django project, created the database model, authentication API, camera and suspicious detection APIs, and finally deployed the backend using Docker and Render.

In the frontend section, we developed the React project, designed the dashboard layout, integrated APIs and authentication, and deployed the final application using Vercel.

Overall, this workflow explains the complete development process from AI model creation to full system deployment.

--------
## Gantt Chart

-----
This Gantt chart represents the project timeline and development schedule of our AI-Based Suspicious Activity Detection System. It shows how the project was completed step by step over different months.

At the beginning, we focused on topic selection, literature review, and dataset collection. After that, we learned and developed the frontend using React and the backend using Django.

Next, we worked on data preprocessing and developed AI models such as CNN-LSTM and 3D CNN for suspicious activity detection. Then, we trained and tested the models to improve accuracy and performance.

After completing the AI model, we developed backend APIs, integrated the database, authentication, and alert systems, including email and alarm notifications.

Finally, we performed system integration, debugging, performance evaluation, report writing, and presentation preparation.

Overall, this chart demonstrates the complete project planning and implementation process from research to final deployment.

---
## Budget plane

This slide presents the budget plan for our AI-Based Suspicious Activity Detection System. Most of the tools and technologies used in this project are open-source and free, which helped reduce development costs significantly.

We used a personal laptop for development, model training, and testing, while the internet connection supported research, dataset downloading, and deployment activities.

For software technologies, we used React for frontend development, Django REST Framework for backend APIs, PostgreSQL for database management, TensorFlow/Keras for deep learning, and OpenCV for video processing. Tools like GitHub and Swagger/OpenAPI were also used for code management and API documentation, all at no cost.

Additionally, we used publicly available CCTV datasets for training the AI model. The only estimated cost is system hosting or cloud deployment, which is around 100 USD.

Overall, this budget plan shows that the project is cost-effective and can be developed using mostly free and open-source technologies.

-----------
# Testing
This slide describes the testing process of our AI-Based Suspicious Activity Detection System. We performed several types of testing to ensure the system works correctly and efficiently.

First, we conducted unit testing to verify individual modules such as login, camera streaming, and alert generation. Then, integration testing was performed to check communication between the frontend, backend, AI model, and database.

We also carried out user testing to confirm that the dashboard, notifications, and live monitoring features work properly from the user’s perspective.

For API testing, we used tools like Postman to test authentication APIs, video stream APIs, and alert responses. We also verified that suspicious activity detection correctly generated alerts and stored logs in the database.

The test results showed that the system successfully detected suspicious activities, triggered alerts in real time, and maintained stable performance during monitoring.

Overall, the testing phase confirmed that the system is functional, reliable, and ready for real-world surveillance applications.

-----------


## summary of project
This slide summarizes the key findings of our project. We successfully developed an AI-based suspicious activity detection system for CCTV surveillance by integrating the frontend, backend, AI model, and database.

The system performs real-time video analysis using deep learning techniques and automatically detects suspicious activities. It also generates instant alerts and notifications, which improves monitoring efficiency and security response time.

Overall, the project provides a scalable, secure, and intelligent real-time surveillance solution for practical use.

------
## contribution
This project contributes to public safety by providing real-time AI-based suspicious activity detection, instant alerts, and reduced manual CCTV monitoring effort.

--------
## limitiation
One limitation of this project is handling different lighting conditions, high computational costs, and maintaining efficient real-time video processing and alert accuracy.

------
## feature work

In future work, this system can be deployed on cloud infrastructure, support multiple CCTV streams, improve detection accuracy, and include mobile or SMS alert notifications for smarter surveillance.

-------

## Slide 1 — Title Slide

Good morning/afternoon everyone.
Today, I am going to present our project titled **“A Real-Time AI-Based Suspicious Activity Detection in CCTV Footage.”**
This project focuses on using Artificial Intelligence and deep learning techniques to automatically detect suspicious activities from CCTV video streams in real time.

---

## Slide 2 — Introduction

In recent years, the demand for smart surveillance systems has increased significantly. Traditional CCTV monitoring depends heavily on human operators, which is time-consuming and prone to errors.
To solve this problem, our project proposes an AI-based suspicious activity detection system that can monitor CCTV footage automatically and generate instant alerts in real time.

---

## Slide 3 — Problem Statement

Traditional CCTV systems rely on manual monitoring, which is inefficient and difficult to manage continuously.
Human monitoring can lead to fatigue, delayed response, and missed suspicious incidents.
Additionally, analyzing large amounts of video data manually is challenging, and many systems lack intelligent alert mechanisms and secure access control.

---

## Slide 4 — Objectives

The main objective of this project is to develop an intelligent surveillance system that can detect suspicious activities automatically from CCTV footage.
Other objectives include real-time monitoring, instant alert generation, reducing manual effort, and improving overall security and response time.

---

## Slide 5 — Literature Review

We studied several research papers and existing surveillance systems related to suspicious activity detection using AI and deep learning.
From the literature review, we found that deep learning models such as CNN, LSTM, and 3D CNN are widely used for video analysis and activity recognition.

---

## Slide 6 — Proposed System

Our proposed system combines a React frontend, Django backend, AI model layer, and PostgreSQL database.
The system captures live CCTV streams, processes video frames using AI models, detects suspicious activities, and generates alerts for operators in real time.

---

## Slide 7 — System Architecture

This architecture diagram shows the communication between the frontend, backend, AI model, and database.
The frontend handles user interaction, the backend processes APIs and authentication, the AI model analyzes video frames, and the database stores users, logs, and alerts.

---

## Slide 8 — Activity Diagram

This activity diagram explains the complete workflow of the system.
After login authentication, live video streams are processed by the AI model. If suspicious activity is detected, the system generates alerts and stores logs in the database; otherwise, monitoring continues normally.

---

## Slide 9 — Sequence Diagram

This sequence diagram shows how different components communicate step by step.
The user logs in, the frontend sends requests to the backend, and the AI model processes video frames. Based on the result, the system either triggers alerts or continues normal surveillance.

---

## Slide 10 — Class Diagram

This class diagram represents the main classes of the system, including User, Camera, VideoStream, DetectionResult, and Alert.
It shows how these classes interact to support authentication, video processing, suspicious activity detection, and notification services.

---

## Slide 11 — Database Schema

This schema diagram illustrates the database structure of our project.
It includes tables for users, cameras, alerts, permissions, activity logs, and detection results, ensuring secure and organized data management.

---

## Slide 12 — Implementation Steps / Modules

This slide shows the implementation workflow of our project.
We first prepared datasets and trained AI models, then developed backend APIs and frontend interfaces, and finally integrated and deployed the complete system.

---

## Slide 13 — Technologies Used

We used React for frontend development, Django REST Framework for backend APIs, PostgreSQL for database management, TensorFlow/Keras for AI model development, and OpenCV for video processing.

---

## Slide 14 — Testing

We performed unit testing, integration testing, and user testing to verify system functionality.
Tools like Postman were used to test APIs and ensure proper communication between the frontend, backend, AI model, and database.

---

## Slide 15 — Gantt Chart

This Gantt chart represents the project timeline and task distribution throughout the development process.
It includes research, dataset preparation, AI model development, backend and frontend integration, testing, and final deployment stages.

---

## Slide 16 — Budget Plan

Most of the technologies and tools used in this project are free and open-source, which helped minimize development costs.
The only estimated expense is cloud hosting and deployment services.

---

## Slide 17 — Key Findings

We successfully developed a real-time AI-based suspicious activity detection system using deep learning techniques.
The system can automatically monitor CCTV footage, detect suspicious activities, and generate alerts efficiently.

---

## Slide 18 — Contributions

This project contributes to public safety by providing intelligent surveillance, real-time monitoring, instant alerts, and reduced manual CCTV monitoring effort.

---

## Slide 19 — Limitations

Some limitations of the project include varying lighting conditions, high computational requirements, and challenges in maintaining real-time processing accuracy.

---

## Slide 20 — Future Work

In the future, the system can be deployed on cloud infrastructure, support multiple CCTV streams, improve detection accuracy, and integrate mobile or SMS notification services.

---

## Slide 21 — Conclusion

In conclusion, our project demonstrates how Artificial Intelligence can improve modern surveillance systems through automated suspicious activity detection and real-time alert generation.
Overall, the system provides a scalable, intelligent, and secure surveillance solution for real-world applications.

---

## Slide 22 — Thank You

Thank you everyone for your attention.
Now, we are ready to answer your questions.
