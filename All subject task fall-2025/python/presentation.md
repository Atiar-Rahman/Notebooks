 title
-----
good afternoon, respected faculty members. my name is md. Atiar rahman and this is my partner, fazle rabbi. we are here today to present our project predefence on real time ai based suspicious activity detection in cctv footage. our work has been conducted under the invalueable of supervision dr. md. faze al fazeal

 
outline:
---
i will begin the presentation by covering the foundational aspect of our project. i will start with an introduction to the topic. define problem statement we are addressing. discuss our motivation. i will then outline our key objectives. identify the existing research gap and provides a breaf litureaure review.  after that i will hand it to cover fazle rabbi.

introduction:
---
as we know, public surveillance system are everywhere, but they are rely and havily on manual human monitoring. this manual approach has significant limitations. operators often experiance fatigue, which can lead to dely and detection and costly human error. our project explore how realtime ai can solve this automatically detection suspicius behavior, with the ultimate aim to improving safety through automation and faster decision making.


problem statement:
-----
 - manual cctv monitoring is slow and not accurate.
 - traditional systems can only find events after they happen.
 - They do not understand context or realtime actions
 - we need a system that can detect suspicious behavoir live while it happens


Motivation
---
- crime is increasing in public areas
- a single person cannot watch many camera at once
 - ai can help by detecting unusual actions instantly.
 - it can send alerts and help prevent crimes,not just analyze them later.

objective
----
to address this we have set some clear objectives for our project. our primary goal is to build realtime ai model. we accept accuracy 80-90%. todo this we will integrate  three powerfull model yolov8 for object detection, deepsort for tracking and slowfast for action recogniation. we will used standard ucf crime dataset train and test. finally  we will design an alert maehanism to flag suspicus events in real time.



Research gap
----
- existing systems work after the event happens.
- they lack real time processing
- they fails in low light or crowded scenes
- models cannot understand intent or context
- and high gpu needs make them hard to deploy


literature review:
---
- old system used manual checking or motion detection
- then machine learning model s like svm and random forest came but they were not good with time based data
- later deep learning models like cnn,lstm and 3cnn  to improve result
- then slowfast networks and yolo models made realtime analysis possible


related work:
---
specically, we reviewed  key papers in the field. while sultani and other achived good accuracy on the ucf crime dataset not realtime.  model like i3d and slowfast should strong temporal understanding but lack integrated object tracking.

our system combines the best parts from previous research
we use yolov8, deepsort and slowfast
this helps to overcome old problems and make full realtime detection pipeline.


at this point i will hand over the presentaion to my partner

