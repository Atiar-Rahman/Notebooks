
To overcome these drawbacks, the proposed system combines CNN-LSTM models with 3D CNN models, which is integrated with a web-based surveillance platform with role-based access control, camera ownership management, automatic email notifications, and sound alarm notifications.


\subsection{Deep Learning Technologies}

For CCTV suspicious activity detection, the proposed system employs CNN-LSTM model and 3D CNN model. The CNN extracts the visual features from the video frames and the LSTM learns the temporal information from sequential data. CNN-LSTM fuses both spatial and temporal learning to achieve better activity recognition.

The 3D CNN models work on multiple video frames simultaneously and directly extract the information related to motion, thus being suitable for real-time video analysis. The models were built and trained using TensorFlow and Keras.The models were created and trained with TensorFlow and Keras.

\subsection{Dataset Description}
The UCF-Crime Dataset\cite{ucfcrime_dataset} and the Violence Detection Dataset for suspicious activity recognition were used to develop the proposed system. The datasets were split into two classes (Normal and Suspicious) because of the binary classification of the project.

The fighting, violence, intrusion, abnormal human behaviours were the suspicious class, and the daily activities were the normal class.

The videos were preprocessed by OpenCV prior to the training which involved extracting the frames, resizing the videos, normalizing the videos and creating video sequences. Real-time suspicious activity detection was performed with the help of trained and tested models: CNN-LSTM and 3D CNN, and the processed data was utilized for training and testing.


\subsection{Frontend Development}

The Frontend Development was done using React due to its speed of rendering, component based structure and the responsive UI design. The frontend dashboard enables user login, CCTV monitoring, camera management and visualization of suspicious activity.

\subsection{Backend Development}

Backend development was done using Django REST Framework (DRF), which provided a secure and scalable way to create REST APIs. 


\subsection{Database Management}

PostgreSQL is used to store all the information about users, camera details, alert data and authentication data. It offers trustworthy performance, security, and data management for web applications.


\subsection{Authentication and Security}

JWT authentication has been added to protect user login and access to the API. Role Based Access Control (RBAC) was also implemented to ensure that users have access to only the cameras to which they are assigned and the features of the system that they are given access to.

\subsection{Alert and Notification System}

Automated email and sound alarm notifications for suspicious activity detection is provided. Reduce repeated alerts by only notifying users of activity changing from "normal" to "suspicious.

\subsection{Video Processing}

The video has been preprocessed, extracted, resized and handled on real-time basis in OpenCV. It assisted in creating video information for training and predicting Deep Learning models.

\subsection{API Documentation}

API documentation and testing were done using Swagger/OpenAPI. It was very convenient to test API endpoints and easier to develop the front end and back end integration.