
| [Korean 🇰🇷](#korean) | [Japanese 🇯🇵](#japanese) | [Team](#Team) |
| :---: | :---: | :---: |

</div>

---

<div id="korean">

### 🇰🇷 Korean Version

# 🌊 AI 기반 선박 제어실 보조 On-Device 시스템

## 💡 1. 프로젝트 개요

본 프로젝트는 **AI 기반 선박 제어실 보조 시스템**을 개발하여 **안개 상태에서도 선박의 주변 환경을 실시간으로 감지**하고, 이를 바탕으로 선원의 안전을 강화하는 시스템입니다. 본 시스템은 **영상 처리**, **이상 감지**, **낙상 감지**, **주변 위험 객체 인식** 등 다양한 기능을 제공합니다.

- **목표**: 안개를 제거하고, 객체를 실시간으로 탐지하여 선원에게 경고를 제공
- **기술**: OpenVINO, PyTorch, YOLO, MoveNet, CLAHE 기법, DCP 복원

## 🛠️ 기술 스택 (Tech Stack)

### 하드웨어
- **Raspberry Pi 5**: MQTT 서버, 영상 처리
- **고정 카메라**: 카메라 모듈 (VID, PID 기반 고유 인덱스)
- **센서 및 기타 장치**: 위험 구역, 낙상 감지 등

### 소프트웨어 / 언어
- **Python**: 전체 시스템 구현
- **OpenVINO**: 영상 처리 및 객체 감지
- **PyTorch**: 이상 감지 (Anomaly Detection)
- **TensorFlow**: MoveNet 모델 기반 포즈 추정
- **YOLOv8**: 객체 검출 (사람 및 위험 객체 감지)
- **MQTT**: 실시간 데이터 전송 및 경고 메시지 발행

### 라이브러리
- **cv2 (OpenCV)**: 이미지 전처리 및 시각화
- **ultralytics (YOLO)**: 객체 검출
- **paho.mqtt**: MQTT 클라이언트

## 🎯 핵심 기능 (Key Features)

1. **안개 제거 및 이미지 향상**
   - **CLAHE 기법**을 통해 저조도 환경에서 이미지를 향상시키고, **DCP(Dark Channel Prior)** 기법으로 안개를 제거하여 선박의 주변 환경을 보다 선명하게 인식합니다.
   
2. **이상 감지 (Anomaly Detection)**
   - **PyTorch 모델**을 사용하여 **이상 행동**을 감지하고, **낙상 감지**를 통해 긴급 상황 발생 시 실시간으로 경고합니다.

3. **포즈 추정 및 낙상 감지**
   - **MoveNet 모델**을 활용하여 **사람의 자세를 추정**하고, 이를 통해 **낙상 여부**를 판단하여 안전을 확보합니다.

4. **위험 객체 탐지 (Dangerous Object Detection)**
   - **YOLOv8** 모델을 사용하여 **위험 객체**(배, 섬, 등대 등)를 실시간으로 탐지하고, 충돌 위험을 예측합니다.

5. **실시간 비디오 스트리밍**
   - **MQTT**를 통해 실시간 비디오 스트리밍을 제공하며, 중요한 객체나 낙상 상황을 감지하여 경고 메시지를 전송합니다.

6. **위험 구역 감지**
   - 특정 영역을 위험 구역으로 설정하고, 해당 구역에 사람이 있을 경우 **경고**를 발행합니다.

## 🚀 시스템 구조 (System Architecture)

- **MQTT 서버**: 데이터를 실시간으로 처리하고 경고 메시지를 발행합니다.
- **카메라**: 고정 카메라에서 영상을 캡처하여 **안개 제거**, **객체 탐지**, **낙상 감지**를 처리합니다.
- **클라이언트**: 각 클라이언트는 카메라로부터 실시간 영상을 받아 **객체 검출**, **낙상 여부 판단**, **위험 구역 확인** 등을 수행합니다.

## 📘 기술 구현 (Core Implementation)

### 1. **CLAHE (Contrast Limited Adaptive Histogram Equalization)** 기법
   - **목표**: 저조도 환경에서 이미지를 향상시켜 **선명한 시야** 확보
   - **기법**: 각 이미지 영역에 대해 **대비 향상**을 수행하여 안개 상태에서도 선명한 이미지 제공

```python
def enhance_low_light(image):
    lab = cv2.cvtColor(image, cv2.COLOR_BGR2LAB)
    l, a, b = cv2.split(lab)
    clahe = cv2.createCLAHE(clipLimit=3.0, tileGridSize=(8,8))
    cl = clahe.apply(l)
    limg = cv2.merge((cl, a, b))
    enhanced_img = cv2.cvtColor(limg, cv2.COLOR_LAB2BGR)
    return enhanced_img
```


<div align="center">
<a href="#japanese">⬇️ 日本語バージョンへ移動 (Go to Japanese Version) ⬇️</a>
</div>

</div>

---

<div id="japanese">

### 🇯🇵 Japanese Version




<div align="center">
<a href="#Team">⬇️ Go to Team Version) ⬇️</a>
</div>

</div>

---

<div id="Team">

### Team

# CTRL SEA CTRL VISION

## 1. 프로젝트 소개
> ### **AI 기반 선박 제어실 보조 On-Device 시스템**

### 주요 기능
- **안개 너머 객체 탐지 및 이상 감지**  
- **선원 안전 확보**  
- **자동 항해 일지 작성 및 브리핑**

**개발 기간**: 2025.09.26 ~ 2025.10.22  
**개발 환경**: Jetson Nano / Raspberry Pi 5 / Python / MQTT  
**발표 자료 다운로드**: [[Ctrl + Click Here]](https://drive.google.com/drive/folders/1VzminDn5eenhiwE3JjTkIos7xjNJQT3j?usp=sharing)

## 2. 안개 제거 Dehazing

> ### **이미지 향상(Image Enhancement) 및 복원(Image Restoration)을 통한 시야 확보**

<img src="docs/resources/screenshot/01_Dehazing.png" alt="01_Dehazing.png" width="800"/>
<img src="docs/resources/screenshot/02_Dehazing.png" alt="02_Dehazing.png" width="800"/>
<img src="docs/resources/screenshot/03_Dehazing.png" alt="03_Dehazing.png" width="800"/>
<img src="docs/resources/video_gif/01_Dehazing.gif" alt="01_Dehazing.gif" width="800"/>

## 3. 이상 감지 Anomaly Detection

### 🛰 이상 감지 학습 방식
<img src="docs/resources/screenshot/04_AD.png" alt="04_AD.png" width="800"/>
<img src="docs/resources/screenshot/05_AD.png" alt="05_AD.png" width="800"/>
<img src="docs/resources/video_gif/02_AD_No_Dehazing.gif" alt="02_AD_No_Dehazing.gif" width="800"/>
<img src="docs/resources/video_gif/03_AD_Dehazing.gif" alt="03_AD_Dehazing.gif" width="800"/>

## 4. 낙상 감지 Fall Detection

<img src="docs/resources/screenshot/06_PE.png" alt="06_PE.png" width="800"/>
<img src="https://github.com/user-attachments/assets/ac1ceadf-53a7-4eb9-8f55-9cbd8d159dfe" width="800"/>  
<img src="https://github.com/user-attachments/assets/58486cd9-d9b5-46f6-bcaf-c36f92431969" width="800"/>  
<img src="docs/resources/video_gif/04_PE1.gif" alt="04_PE1.gif" width="800"/>
<img src="docs/resources/video_gif/05_PE2.gif" alt="05_PE2.gif" width="800"/>
 


## 5. 상황실 Ctrl Room

### 🛰 MQTT 통신 구조

<img src="docs/resources/screenshot/07_Server.png" alt="07_Server.png" width="800"/>
<img src="docs/resources/screenshot/08_Server.png" alt="08_Server.png" width="800"/>
<img src="docs/resources/video_gif/06_Server_SystemLog.gif" alt="06_Server_SystemLog.gif" height="480"/>
<img src="docs/resources/video_gif/07_Server_Logbook.gif" alt="07_Server_Logbook.gif" height="480"/>

## 6. 팀원 소개
| 이름 | 담당 |
|------|------|
| **문두르** | PM |
| **류균봉** | Image Enhancement / Dehazing |
| **나지훈** | Server / MQTT / GUI / LLM / STT / TTS |
| **김찬미** | Pose Estimation / Fall Detection |
| **이환중** | Object Detection / Anomaly Detection |
