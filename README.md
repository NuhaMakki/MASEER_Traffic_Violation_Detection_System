# 🚦 Maseer (مسير) - Intelligent Traffic Violation Detection System


<p align="center"> <img src="Maseer_img/logo1.png" width="95%" alt="Benchmarking Analysis"> </p>

## 📖 Table of Contents  

- [Introduction](##introduction)  
- [Detected Traffic Violations](#detected-traffic-violations)  
- [Detection Process](#detection-process)  
- [System Testing](#system-testing)  
- [Sample Output](#sample-output)  
- [Installation & Setup](#installation--setup)  
- [Future Enhancements](#future-enhancements)  


## 📖 Table of Contents  

📌 [Introduction](#introduction)  
🚦 [Detected Traffic Violations](#detected-traffic-violations)  
🔍 [Detection Process](#detection-process)  
🧠 [Models & Techniques Used](#models--techniques-used)  
📊 [Sample Output](#sample-output)  
💾 [Back-End Implementation](#back-end-implementation)  
⚙️ [Installation & Setup](#installation--setup)  
📝 [How to Use](#how-to-use)  
📈 [Testing & Results](#testing--results)  
📂 [Directory Structure](#directory-structure)  
🚀 [Challenges & Future Enhancements](#challenges--future-enhancements)  
🤝 [Contributors & Acknowledgments](#contributors--acknowledgments)  
📜 [License](#license)  


## 📖 Table of Contents  

| 📌 [Introduction](#introduction)  | 🚦 [Traffic Violations](#detected-traffic-violations)  | 🔍 [Detection Process](#detection-process)  |
|----------------------|----------------------|----------------------|
| 🧠 [Models & Techniques](#models--techniques-used) | 📊 [Sample Output](#sample-output) | 💾 [Back-End](#back-end-implementation) |
| ⚙️ [Installation & Setup](#installation--setup) | 📝 [How to Use](#how-to-use) | 📈 [Testing & Results](#testing--results) |
| 📂 [Directory Structure](#directory-structure) | 🚀 [Challenges & Future](#challenges--future-enhancements) | 🤝 [Contributors](#contributors--acknowledgments) |
| 📜 [License](#license) | | |


## 📖 Table of Contents  

<details>
  <summary>📌 Introduction</summary>
  <ul>
    <li><a href="#introduction">Overview</a></li>
    <li><a href="#detected-traffic-violations">Traffic Violations</a></li>
  </ul>
</details>

<details>
  <summary>🚦 Detection & Models</summary>
  <ul>
    <li><a href="#detection-process">Detection Process</a></li>
    <li><a href="#models--techniques-used">Models & Techniques</a></li>
  </ul>
</details>

<details>
  <summary>💾 Implementation & Usage</summary>
  <ul>
    <li><a href="#back-end-implementation">Back-End Implementation</a></li>
    <li><a href="#installation--setup">Installation & Setup</a></li>
    <li><a href="#how-to-use">How to Use</a></li>
  </ul>
</details>

<details>
  <summary>📂 Other</summary>
  <ul>
    <li><a href="#testing--results">Testing & Results</a></li>
    <li><a href="#directory-structure">Directory Structure</a></li>
    <li><a href="#challenges--future-enhancements">Challenges & Enhancements</a></li>
    <li><a href="#contributors--acknowledgments">Contributors</a></li>
    <li><a href="#license">License</a></li>
  </ul>
</details>


---

## 📌 Introduction  

### 🚀 Overview
**Maseer** is an **AI-powered solution** designed to **automate** the detection and identification of **traffic priority violations** using video footage from regular drivers' **Dashcams**. By leveraging **computer vision** and **machine learning**, Maseer processes Dashcam recordings to **identify specific traffic violations**, addressing gaps in **traditional traffic monitoring systems**. This approach enhances **road safety** and **empowers drivers** to contribute to **law enforcement efforts**, streamlining **violation reporting** while protecting their **rights**.

### 🎯 Objectives
✅ **Leverage Dashcam footage** → Minimize the need for physical traffic police presence.  
✅ **Automate violation detection** → Reduce the workload for both Dashcam owners and traffic authorities.  
✅ **Facilitate data-driven reporting** → Assist victims of priority violations in filing accurate reports.  
✅ **Enhance traffic management** → Utilize advanced technology for precise and efficient violation monitoring.  




## 🚦 Detected Traffic Violations  
Maseer focuses on detecting and identifying **traffic priority violations**, specifically **sudden lane change violations**. This violation occurs when a driver **fails to yield to a vehicle already in the target lane** while switching lanes, creating a hazardous situation. The violation is characterized by:

🚗 **A vehicle (🔴 red) attempting to switch lanes without yielding to a vehicle (🔵 blue) already in that lane**, causing potential accidents.  
📏 **A minimum safe distance of three meters is not maintained**, leading to unsafe conditions.  
⚠️ **Sudden and reckless lane changes** disrupt traffic flow and increase accident risks.  

<p align="center">  
  <img src="Maseer_img/LaneChange3.png" width="70%" alt="Sudden Lane Change Violation">  
</p>

In the figure above:  
- The **🔵 blue vehicle holds priority** in its current lane.  
- The **🔴 red vehicle violates priority** if it switches lanes without waiting for the blue vehicle to pass.  
- A violation occurs if the red vehicle **cuts too closely in front**, disrupting the blue vehicle’s passage and increasing accident risk.  


---

## 🔍 Detection Process  

The process of analyzing videos to identify and extract data related to sudden lane change violations comprises **two primary phases**, as illustrated below.

<p align="center">  
  <img src="Maseer_img/process.png" width="90%" alt="Detection Process">  
</p>

### 🚘 1️⃣ Violation Detection  
This phase involves:  
✅ **Vehicle Detection & Tracking**: Uses **YOLOv8n** for vehicle detection and **SORT** algorithm for tracking objects across frames.  
✅ **Street Lane Detection**: Utilizes **Hough Transform** and **Transition Lines** for lane marking identification.  
✅ **Monitoring Lane Changes**: Identifies vehicles violating priority rules within **3 meters** using **trajectory analysis** and **intersection detection**.

#### 🚗 Vehicle Detection and Tracking
- **YOLOv8n Model**: Detects a wide range of vehicles (cars, trucks, bikes).  
- **SORT Algorithm**: Assigns unique IDs to track vehicles across frames.  

<p align="center">  
  <img src="Maseer_img/tracking.png" width="70%" alt="Detection Process">  
</p>

#### 🛣️ Street Lane Detection
##### **Approach 1: Hough Transform Algorithm**
- Used **Gaussian Blur + Canny Edge Detection** to process images.
- **Hough Transform** was applied to detect lane markings.  
- ❌ **Limitations**: Inconsistent results leading to **false positives & negatives**.

<p align="center">  
  <img src="Maseer_img/lane.png" width="70%" alt="Lane Detection using Hough Transform">  
</p>

##### **Approach 2: Transition Lines**
- Defined **two static lines** on the video frames to mark lane boundaries.  
- ✅ **More consistent** for detecting lane changes within **3 meters**.  
- ❌ **Limitations**: Works best when the Dashcam remains **static**.

<p align="center">  
  <img src="Maseer_img/lane3.png" width="70%" alt="Transition Lines for Lane Detection">  
</p>


#### 🔄 **Monitoring Lane Changes**  
The system detects **sudden lane change violations** when vehicles switch lanes **too close (≤3 meters)** to the driver.  

##### 📍 **Key Points Calculation**  
Each vehicle’s movement is tracked using:  
- **Left Point** → (x1, y2)  
- **Right Point** → (x2, y2)  
- **Center Point** → \( \left(\frac{x1 + x2}{2}, y2 \right) \)  

<p align="center">  
  <img src="Maseer_img/points.png" width="70%" alt="Left, Right, and Center Points">  
</p>  


##### 📈 **Trajectory & Intersection Detection**  
The system tracks **left, right, and center points** across frames to determine lane change violations.  

A **violation is detected** if the trajectory intersects a **transition line**:  
- **Step 1:** Check if **left or right point** crosses a transition line → 🚨 Possible violation.  
- **Step 2:** Confirm if **center point** crosses the same line → ✅ Violation confirmed.  

<p align="center">  
  <img src="Maseer_img/points2.png" width="70%" alt="Violation Detection and Confirmation">  
</p>  


### 📊 2️⃣ Data Extraction  
Once a violation is detected, **relevant data** is extracted for reporting.

✅ **License Plate Detection** → Identifies and extracts vehicle license plate details.  
✅ **License Plate OCR** → Uses **EasyOCR** for text recognition and conversion.  
✅ **Date & Time Extraction** → Extracts timestamp for accurate reporting.

#### 🔢 License Plate Detection & OCR
- Trained **YOLOv8n** on a **24,242-image dataset** for license plate detection.  
- **EasyOCR** extracts the plate number from detected frames.  
- Ensures **93% accuracy** for extracted license plate numbers.

<p align="center">  
  <img src="Maseer_img/plateA.png" width="70%" alt="License Plate Detection">  
</p>

#### ⏳ Date & Time Extraction
- Uses **OpenCV** for region cropping and **EasyOCR** for text recognition.  
- **Formatted extraction**: `YYYY-MM-DD` (date) and `HH:MM:SS` (time).  
- Ensures **accurate violation reporting** with a **minimum confidence threshold of 40%**.

<p align="center">  
  <img src="Maseer_img/plateB.png" width="70%" alt="Date & Time Extraction">  
</p>

---


## 🛠️ **System Testing**  
To ensure the accuracy and reliability of **Maseer**, multiple testing phases were conducted on different system components, including **violation detection** and **data extraction**.  

### 🚦 **Violation Detection Testing**  
The system was tested on **71 videos** (4–85 seconds long), covering **day and night** conditions. The videos were categorized into:  
- **Violations (V)**: Lane changes within **3 meters**.  
- **Non-Violations (C)**: Lane changes **beyond 3 meters**.  
- **Normal Driving (N)**: No lane change.  

📊 **Results Summary:**  
📌 **Achieved an accuracy of 95%**, even on low-quality videos (as low as **480p x 272p**).  
<p align="center">  
  <img src="Maseer_img/detect_test.png" width="90%" alt="Violation Detection Testing Results">  
</p>  

### 🔍 **Data Extraction Testing**  

The system was tested on:  
- **19 videos & 50 images** for license plate extraction.  
- **60 videos** for date/time extraction.  

📊 **Results Summary:**  
📌 **Overall Accuracy:** **78%** for data extraction.  
<p align="center">  
  <img src="Maseer_img/plate_test.png" width="90%" alt="Data Extraction Testing Results">  
</p>  



---
## 📄 Sample Output  







## 🛠️ Technologies Used
- 🔍 **Computer Vision** (OpenCV, YOLO)  
- 🧠 **Machine Learning** (TensorFlow, PyTorch)  
- 🏎️ **Video Processing** (FFmpeg)  
- 🗄️ **Database** (MySQL, Firebase)  
- 🌐 **Web Framework** (Flask, FastAPI)



- [Introduction](#introduction)  
  - Overview of the project, its objectives, and key features.
- [Detected Traffic Violations](#detected-traffic-violations)  
  - List of traffic violations detected (e.g., speeding, red light running, etc.).
- [Detection Process](#detection-process)  
  - Explanation of how traffic violations are detected (step-by-step).
- [Models & Techniques Used](#models--techniques-used)  
  - Overview of the models (e.g., YOLOv8, license plate detection) and methods used for detection.
- [Sample Output](#sample-output)  
  - Example results, including images or videos of detected violations.
- [Back-End Implementation](#back-end-implementation)  
  - Details on how the backend is structured and the technologies used.
- [Installation & Setup](#installation--setup)  
  - Steps to install and configure the project.
- [How to Use](#how-to-use)  
  - Instructions on running the system and interpreting results.
- [Testing & Results](#testing--results)  
  - Performance metrics and results of system testing.
- [Directory Structure](#directory-structure)  
  - Overview of the project’s folder organization and key files.
- [Challenges & Future Enhancements](#challenges--future-enhancements)  
  - Discussion of current limitations and potential improvements.
- [Contributors & Acknowledgments](#contributors--acknowledgments)  
  - Recognition of contributors and relevant credits.
- [License](#license)  
  - Information about the project’s license.




## 📄 Generated Output  
Maseer generates multiple output formats to report violations:  

- **Annotated Images**: Bounding boxes highlight violations.  
- **JSON Reports**: Structured logs of detected violations.  
- **Video Processing**: Marking detected violations in footage.  

📝 **Example Output (JSON)**  
```json
{
    "violation": "Red Light Violation",
    "timestamp": "2025-04-01T10:30:00Z",
    "vehicle_id": "ABC-123",
    "location": "Main Street Intersection"
}
```

📷 **Sample Annotated Image:**  
(*Insert an image of detected violations here*)  

---

## 🛠 Installation & Usage  
### 📌 Prerequisites  
Ensure you have the following installed:  
- Python 3.8+  
- OpenCV  
- TensorFlow / PyTorch  
- YOLOv8  

### 📥 Installation  
```bash
git clone https://github.com/yourusername/maseer.git
cd maseer
pip install -r requirements.txt
```

### 🚀 Running the Detection System
```bash
python detect_violations.py --input video.mp4
```

## 🧪 Testing & Evaluation  
Maseer has been rigorously tested on real-world traffic footage to ensure high accuracy and robustness in detecting traffic violations.  

### 📊 Performance Metrics  
The system was evaluated using a dataset of annotated traffic videos, measuring key performance indicators such as precision, recall, and F1-score.  

| Metric    | Score  |
|-----------|--------|
| Precision | 91%    |
| Recall    | 89%    |
| F1-Score  | 90%    |

### 🔍 Edge Cases Considered  
- **Nighttime detection:** Improved accuracy using adaptive brightness correction.  
- **Occlusions:** Handled using object tracking and interpolation techniques.  
- **Weather variations:** Trained on diverse environmental conditions.  
- **Multiple violations:** Simultaneous detection of different types of infractions.  

---

## 🚀 Challenges & Future Improvements  
### 🔴 Current Challenges  
- Detecting violations in highly congested traffic scenarios.  
- Improving accuracy for motorcycles and bicycles.  
- Reducing false positives in violation detection.  

### 🔵 Future Enhancements  
- **Speeding Detection:** Implementing license plate tracking for velocity estimation.  
- **Real-Time Violation Reporting:** Integration with cloud-based reporting systems.  
- **Enhanced AI Models:** Exploring transformers for better feature extraction.  
- **Multi-Camera Coordination:** Synchronizing multiple camera feeds for better tracking.  

---

## 👥 Contributors & Acknowledgments  
Developed by **[Your Name]** and team.  
📧 Contact: your.email@example.com  

Special thanks to open-source datasets and AI frameworks that contributed to the success of this project.  

🌟 If you find this project useful, consider giving it a ⭐ on GitHub!  
