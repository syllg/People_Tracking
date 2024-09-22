# 📹 Real-Time Object Tracking and Warning System for ROI Monitoring

**Input and Output Videos:** [View Videos](https://bit.ly/Realtime-Prople-Tracking)

## 1. Objective:
The project aims to analyze a video feed in real-time to monitor and track objects (e.g., people) within a defined rectangular area of interest (ROI). If 4 or more objects stay in the area for at least 2 minutes, a warning message is triggered. The project utilizes object detection, tracking, and time-based conditions to achieve this goal.

## 2. Key Features:
- **Real-Time Object Detection:** Detects objects within the video frames using a YOLO-based object detection model.
- **Object Tracking:** Tracks object movement across multiple frames, utilizing the center points of the detected bounding boxes.
- **Region of Interest (ROI) Monitoring:** A rectangular area is defined in which the object count is monitored. The system continuously counts how many objects enter and stay in the ROI.
- **Warning System:** If there are 4 or more objects in the ROI for a duration of 120 seconds (2 minutes), a warning message is triggered and displayed on the video.
- **Scaling and Optimization:** The video can be resized based on the provided scaling percentage, and object tracking is optimized by filtering out old tracks after a set patience period.

## 3. System Workflow:
### Video Input:
- The system reads a video file (input_video.mp4) using OpenCV.
- Optionally, the video can be resized based on a configurable scale percentage.

### Object Detection:
- A pre-trained object detection model (YOLO) is used to predict objects in each frame.
- Only specified object classes (e.g., person, ID 0) are considered for tracking and monitoring.
- The bounding boxes, confidence scores, and class labels are extracted for each detected object.

### Object Tracking:
- The center point of each bounding box is calculated to track objects across frames.
- A tracking system compares the current frame's object positions to previous frames' positions using Euclidean distance.
- Objects that move into the defined ROI are tracked for their duration inside the area.
- Tracking data is filtered periodically to remove outdated or irrelevant tracks.

### Region of Interest (ROI):
- A specific rectangular area within the frame is defined by the coordinates (area_x1, area_y1) to (area_x2, area_y2).
- Objects inside this area are counted, and a red bounding box is drawn around them.
- A counter for the number of objects in the ROI is displayed on the video.

### Warning System:
- If the count of objects inside the ROI reaches or exceeds 4 for a duration of 120 seconds (2 minutes), the system triggers a warning.
- A timer displays the remaining time before triggering the warning. Once the condition is met, an alert message (ALERT: people in area >= 4 for 2 mins) appears on the video.

### Video Output:
- Each processed frame is saved to an output video file (rep_result.mp4).
- The output video includes bounding boxes, object IDs, object counts, and warning messages.

## 4. Configurations:
- **Scaling and Resolution:** The video can be resized using the scale_percent parameter.
- **Object Detection Confidence:** The minimum confidence level for object detection is set by conf_level.
- **Object Tracking Threshold:** The maximum allowed distance between consecutive frames to track the same object is controlled by thr_centers.
- **Patience:** The duration after which old tracks are filtered out is set by patience.
- **Warning Duration:** The time (in seconds) that triggers the warning system is set by warning_duration (e.g., 120 seconds or 2 minutes).
- **Area Transparency:** The transparency of the ROI overlay is determined by alpha.

## 5. Modules and Functions:
- **update_tracking():** Updates the position of tracked objects or assigns a new ID to a new object.
- **filter_tracks():** Filters out objects that haven't been detected within the set patience period.
- **put_text_with_background():** Adds text labels with background on the video frames.

## 6. Dependencies:
- OpenCV for video handling and object rendering.
- YOLO model for object detection.
- NumPy and Pandas for matrix manipulation and data handling.

## 7. Use Case:
This project is particularly useful for security surveillance, people counting, and crowd control in sensitive areas. For instance, it could be used in a store or a public event to trigger an alert when a crowd exceeds a certain number within a specific zone.
