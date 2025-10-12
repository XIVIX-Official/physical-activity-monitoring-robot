# XIVIX Robot - Physical Activity Monitoring

![XIVIX Robot](./assets/xivix-robot.png)

## Overview

The **XIVIX Robot** is an advanced physical activity monitoring system developed by XIVIX. This robot leverages AI-powered pose estimation to detect physical activities such as push-ups, squats, and other exercises, providing real-time rep counting and posture feedback to users.

## Project Vision

The XIVIX Robot aims to revolutionize fitness training and rehabilitation by providing autonomous, real-time physical activity analysis. By combining robotics, computer vision, and machine learning, this project creates an intelligent fitness companion capable of monitoring, analyzing, and guiding users through their exercise routines with precision and accuracy.

## Features

- **Activity Detection**: Identifies various physical exercises using computer vision and pose estimation
- **Rep Counting**: Automatically counts repetitions for detected exercises
- **Posture Feedback**: Provides real-time feedback on exercise form and posture
- **Multi-modal Sensor Integration**: Combines visual data with additional sensor inputs for comprehensive monitoring
- **AI-Powered Analysis**: Uses deep learning models for accurate pose and activity recognition
- **Simulation Environment**: Full robot simulation in Webots for testing and development

## Technology Stack

- **CAD Design**: FreeCAD for robot model design and iterations
- **Simulation**: Webots for physics-based robot simulation and testing
- **Computer Vision**: OpenCV, MediaPipe for pose estimation
- **Machine Learning**: TensorFlow/PyTorch for activity classification
- **Programming**: Python, ROS (Robot Operating System)
- **Version Control**: Git and GitHub

## Project Structure

```
physical-activity-monitoring-robot/
├── .gitignore
├── README.md
├── LICENSE
├── assets/
│   ├── xivix-robot.png
│   ├── design-references/
│   └── documentation/
├── cad-models/
│   ├── freecad/
│   │   ├── xivix-body.FCStd
│   │   ├── xivix-arm.FCStd
│   │   ├── xivix-leg.FCStd
│   │   ├── xivix-head.FCStd
│   │   └── assemblies/
│   │       └── xivix-full-assembly.FCStd
│   └── exported/
│       ├── urdf/
│       │   └── xivix-robot.urdf
│       └── mesh/
│           └── *.obj
├── simulation/
│   ├── webots/
│   │   ├── worlds/
│   │   │   ├── xivix-training-environment.wbt
│   │   │   └── xivix-fitness-gym.wbt
│   │   ├── controllers/
│   │   │   ├── xivix_main_controller.py
│   │   │   └── activity_monitor_controller.py
│   │   ├── protos/
│   │   │   └── XIVIX.proto
│   │   └── plugins/
│   ├── configs/
│   │   └── webots-config.yaml
│   └── README.md
├── src/
│   ├── pose-estimation/
│   │   ├── pose_estimator.py
│   │   ├── models/
│   │   │   └── pose-model.pth
│   │   └── utils/
│   │       ├── keypoint_utils.py
│   │       └── visualization.py
│   ├── activity-detection/
│   │   ├── activity_classifier.py
│   │   ├── models/
│   │   │   └── activity-classifier.pth
│   │   ├── activity_definitions.yaml
│   │   └── rep_counter.py
│   ├── real-time-feedback/
│   │   ├── feedback_engine.py
│   │   ├── posture_analyzer.py
│   │   └── alert_system.py
│   ├── robot-control/
│   │   ├── robot_interface.py
│   │   ├── motion_planner.py
│   │   └── gesture_controller.py
│   └── utils/
│       ├── config_loader.py
│       ├── logger.py
│       └── constants.py
├── models/
│   ├── pretrained/
│   │   ├── pose-estimation-model.pth
│   │   └── activity-classifier-model.pth
│   └── training/
│       ├── train_pose_estimator.py
│       ├── train_activity_classifier.py
│       └── datasets/
│           ├── README.md
│           └── annotations/
├── tests/
│   ├── unit/
│   │   ├── test_pose_estimation.py
│   │   ├── test_activity_detection.py
│   │   └── test_feedback_engine.py
│   ├── integration/
│   │   ├── test_simulation.py
│   │   └── test_end_to_end.py
│   └── README.md
├── docs/
│   ├── architecture.md
│   ├── setup-guide.md
│   ├── user-manual.md
│   ├── api-reference.md
│   ├── training-guide.md
│   └── contributing.md
├── config/
│   ├── default-config.yaml
│   ├── simulation-config.yaml
│   └── hardware-config.yaml
├── scripts/
│   ├── setup-environment.sh
│   ├── download-models.py
│   ├── run-simulation.py
│   ├── run-tests.sh
│   └── build-cad.sh
├── data/
│   ├── training-datasets/
│   ├── validation-sets/
│   └── sample-recordings/
├── requirements.txt
└── setup.py
```

## Getting Started

### Prerequisites

- Python 3.9+
- FreeCAD 0.21+
- Webots 2023a+
- ROS 2 (optional, for advanced robotics features)

### Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/XIVIX-Official/physical-activity-monitoring-robot.git
   cd physical-activity-monitoring-robot
   ```

2. **Set Up Environment**
   ```bash
   bash scripts/setup-environment.sh
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download Pretrained Models**
   ```bash
   python scripts/download-models.py
   ```

### Quick Start

#### Run Simulation
```bash
python scripts/run-simulation.py
```

#### Test Pose Estimation
```bash
python src/pose-estimation/pose_estimator.py --camera webcam
```

#### Run Unit Tests
```bash
bash scripts/run-tests.sh
```

## Usage

### Basic Activity Monitoring

```python
from src.pose_estimation.pose_estimator import PoseEstimator
from src.activity_detection.activity_classifier import ActivityClassifier
from src.activity_detection.rep_counter import RepCounter

# Initialize components
pose_estimator = PoseEstimator(model_path="models/pretrained/pose-estimation-model.pth")
activity_classifier = ActivityClassifier(model_path="models/pretrained/activity-classifier-model.pth")
rep_counter = RepCounter()

# Process video/camera feed
while True:
    frame = camera.read()
    keypoints = pose_estimator.estimate(frame)
    activity = activity_classifier.predict(keypoints)
    rep_count = rep_counter.update(activity, keypoints)
    
    print(f"Activity: {activity}, Reps: {rep_count}")
```

### Webots Simulation

1. Open Webots
2. Load the world file: `simulation/webots/worlds/xivix-training-environment.wbt`
3. Press play to start simulation
4. Monitor real-time activity detection in the console

## Development Roadmap

- [ ] Phase 1: Core pose estimation implementation
- [ ] Phase 2: Activity classification model training
- [ ] Phase 3: Real-time feedback system
- [ ] Phase 4: Robot hardware integration
- [ ] Phase 5: Multi-user tracking and gym deployment
- [ ] Phase 6: Advanced metrics and analytics dashboard

## Contributing

We welcome contributions from the community! Please read our [Contributing Guidelines](CONTRIBUTING.md) for more information on how to get started.

## Documentation

- [Architecture Overview](docs/architecture.md)
- [Setup Guide](docs/setup-guide.md)
- [User Manual](docs/user-manual.md)
- [API Reference](docs/api-reference.md)
- [Training Guide](docs/training-guide.md)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact & Support

For questions, feedback, or support, please reach out to the XIVIX research division:

- **Email**: info@codexustechnologies.com
- **GitHub Issues**: [Report a bug or request a feature](https://github.com/XIVIX-Official/physical-activity-monitoring-robot/issues)
- **Discussions**: [Join our community discussions](https://github.com/XIVIX-Official/physical-activity-monitoring-robot/discussions)

---

**Powered by XIVIX**