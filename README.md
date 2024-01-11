# Staff-Detection
Detecting presence of staff based on work tag detection, tracking the timestamp and coordinates when the staff is present in the video

## Objective
1.	To determine the timestamps when staff members appear in the video.
2.	To extract the x and y coordinates of staff members.

## Installation
Clone this repository or download as zip file:
```bash
git clone https://github.com/alexy208/Staff-Detection.git
```
Install python if you havent, and install the required libraries using this command:
```bash
pip install -r requirements.txt
 ```
## Process Flow
1.	Identification of Work Tags: The system begins by detecting work tags on staff, using a custom trained YOLOv8 model. This model was trained with 60 images and validated with 10 images.
2.	Determining Staff Presence: A person is identified as a staff member if the work tag's bounding box is inside the person's bounding box.
3.	Staff Tracking: Upon detecting a work tag, the system identifies and tracks the staff member. Each staff is assigned an ID, and the system records the time and their location in the video. We used a ByteTrack model (bytetrack.yaml) for this purpose.
4.	Model Training for People Detection: Initially, a pre-trained YOLOv8 model was used. However, due to the top-down fisheye view of the camera in our test video, this model struggled with accurate detection of human. To address this, a new model was specifically trained to recognize people in this unique camera view, using 80 images for training and 20 for validation.
5.	Data Recording: The system logs the time in milliseconds and records the centre point of the staff's bounding box as their x and y coordinates.

## Limitations
•	Data Source: Both the training and validation datasets were derived from frames of the same video, leading to very similar datasets. This approach may affect the model's ability to generalize and perform accurately on different videos.
Reidentification Challenges
•	Tracking Consistency: Although the pre-trained YOLO tracking model offers basic reidentification capabilities, it sometimes loses track and hence assigning multiple IDs to the same person. The re-detection of work tag aids in reidentifying staff, but further improvements are needed. Future enhancements could include integrating advanced tracking algorithms such as SSD or DeepSort for more reliable reidentification.

## Results
Model training results are stored under folder runs/detect/train2 (tag detection model) or runs/detect/train8 (person detection model). The timestamp and coordinates of the detected staff is stored in staff_data.csv. The demo video can be obtained here: https://youtu.be/ykvuHomF7SU.
