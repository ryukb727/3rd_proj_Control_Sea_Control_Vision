| [Korean 🇰🇷](#korean) | [Japanese 🇯🇵](#japanese) | [Team](#Team) |
| :---: | :---: | :---: |

</div>

---

<div id="korean">

### 🇰🇷 Korean Version

# 🌊 AI 기반 선박 제어실 보조 On-Device 시스템
## 🏆 **인텔 엣지 AI 실무 프로젝트 경진대회 최우수상 수상**

<img src="docs/resources/video_gif/01_Dehazing.gif" alt="01_Dehazing.gif" width="800"/>
<img src="docs/resources/video_gif/03_AD_Dehazing.gif" alt="03_AD_Dehazing.gif" width="800"/>
<img src="docs/resources/video_gif/04_PE1.gif" alt="04_PE1.gif" width="800"/>
<img src="docs/resources/video_gif/06_Server_SystemLog.gif" alt="06_Server_SystemLog.gif" height="480"/>

## 💡 1. 프로젝트 개요

본 프로젝트는 **AI 기반 컴퓨터 비전 기술**을 활용하여 해상 환경에서의 선박 항해 안전성과 효율 향상을 위한 **선박 제어실 보조 On-Device 시스템**입니다.
<br>
이 시스템은 **안개 속 객체를 실시간으로 탐지**하고, **이상을 감지**하며, **객체 추적, 자세 추정** 기술로 선체 안전과 선원 보호를 도모합니다. 또한, **LLM**을 활용하여 **자동 항해 일지 작성과 브리핑**을 제공합니다.
<br>
시스템의 핵심 기능으로는 **안개 제거**, **이상 감지**, **낙상 감지**, **자동 항해 일지 작성** 등이 포함됩니다.

### 📍 전체 시스템 구상도
![Image](https://github.com/user-attachments/assets/aa3c5641-43c6-497d-b5ac-7b89fd1d8878)

---

## 🛠️ 2. 기술 스택

![RaspberryPi](https://img.shields.io/badge/Hardware-RaspberryPi5-A22846?style=for-the-badge&logo=raspberrypi&logoColor=white)
![JetsonNano](https://img.shields.io/badge/Hardware-Jetson%20Nano-76B041?style=for-the-badge&logo=nvidia&logoColor=white)
![IMU Sensor](https://img.shields.io/badge/Hardware-IMU%20Sensor-FF9900?style=for-the-badge&logo=generic&logoColor=white)

![Python](https://img.shields.io/badge/Language-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenVINO](https://img.shields.io/badge/Framework-OpenVINO-0078D4?style=for-the-badge&logo=intel&logoColor=white)
![PyTorch](https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![YOLO](https://img.shields.io/badge/Model-YOLOv8-FF2B2B?style=for-the-badge&logo=github&logoColor=white)
![EfficientNet](https://img.shields.io/badge/EfficientNet-B3-FF6F00?style=for-the-badge&logo=google&logoColor=white)
![MoveNet](https://img.shields.io/badge/Model-MoveNet-03A9F4?style=for-the-badge&logo=google&logoColor=white)
![MQTT](https://img.shields.io/badge/Protocol-MQTT-00B5A1?style=for-the-badge&logo=cloudsmith&logoColor=white)
![OpenCV](https://img.shields.io/badge/Library-OpenCV-5C3A00?style=for-the-badge&logo=opencv&logoColor=white)
![MariaDB](https://img.shields.io/badge/Database-MariaDB-003B57?style=for-the-badge&logo=mariadb&logoColor=white)
![PyQt6](https://img.shields.io/badge/Framework-PyQt6-41C1C1?style=for-the-badge&logo=python&logoColor=white)

---

## 🎯 3. 핵심 기능

- **안개 제거 및 이상 감지**: 
   - **CLAHE 기법**과 **DCP(Dark Channel Prior)** 기법을 사용하여 안개를 제거
   - **YOLOX-S**와 **EfficientNet-B3** 모델을 활용해 **이상 객체 탐지** 및 **라벨링**을 실시간으로 수행

- **낙상 감지 및 경고 시스템**: 
   - **YOLOv8n** 모델로 **갑판 위 선원** 객체 탐지
   - **MoveNet Lightning** 모델로 **선원의 자세를 추정**, **fall down 상태**가 감지되면 서버로 **위험 알림** 전송
   - 특정 영역을 위험 구역으로 설정하고, 해당 구역에 사람이 있을 경우 **경고** 발송

- **자동 항해 일지 작성 및 브리핑**:
   - <strong>LLM (대형 언어 모델)</strong>을 활용
   - <strong>STT (음성 인식)</strong>와 <strong>TTS (음성 합성)</strong>로 선원 명령 처리와 **자동 항해 일지 작성** 및 **브리핑** 제공

- **실시간 데이터 처리**: 
   - 각 모듈에서 **MQTT**를 통해 데이터를 실시간으로 서버로 전송
   - **이상 감지**, **낙상 감지**, **위험 객체 감지** 등의 데이터 처리 및 저장
   - 실시간으로 처리된 데이터는 **모니터링 UI**를 통해 상황실에서 즉각 확인 가능 

---

## 📘 4. 기술 구현

### 1) **CLAHE (Contrast Limited Adaptive Histogram Equalization)** 기법
   - **목표**: 저조도 환경에서 이미지를 향상시켜 **선명한 시야** 확보
   - **기법**: 각 이미지 영역에 대해 **대비 향상**을 수행하여 안개 상태에서도 선명한 이미지 제공

### 2) **DCP (Dark Channel Prior)** 기법
   - **목표**: 이미지에서 **안개**를 제거하여 더욱 명확한 시야 제공
   - **기법**: 이미지의 **어두운 채널**을 사용해 안개 농도를 추정하고 이미지 복원

### 3) **YOLOX-S & EfficientNet-B3** 모델을 활용한 **이상 감지**
   - **목표**: 실시간으로 **이상 객체** 탐지
   - **기법**: **YOLOX-S** 모델을 사용하여 객체를 탐지하고, **EfficientNet-B3** 모델로 객체를 라벨링

### 4) **YOLOv8n 모델**을 활용한 **낙상 감지**
   - **목표**: 갑판 위 **선원 객체** 감지 및 **낙상** 상태 감지
   - **기법**: **YOLOv8n** 모델로 선원을 객체 탐지하고, **MoveNet Lightning**으로 자세를 추정하여 낙상 감지

### 5) **LLM**, **STT**, **TTS**를 활용한 **자동 항해 일지 작성 및 브리핑**
   - **목표**: **항해 일지** 자동 작성 및 **브리핑** 제공
   - **기법**: **STT**로 음성 인식, **TTS**로 실시간 브리핑 음성 제공, **LLM**으로 항해 일지 자동 작성

---

## 👨‍💻 5. 역할 및 기여

- **CLAHE 기법**을 사용하여 이미지 향상 → 저조도 환경에서 이상 감지 성능 향상
- **DCP** 기법으로 **안개 제거** → 해무로 인한 시야 저하를 개선하고, 선체 안전 확보, 이상 감지 성능 향상
- **부팀장**으로서 팀장 부재시 역할을 대행하며 프로젝트의 원활한 진행 지원

---

## 🐞 6. 트러블슈팅
### 1) **안개 제거 기법 (Dehazing) 모델 성능 문제**  
- 원인: 다양한 안개 제거 모델을 시도했으나 버전 호환, 속도 문제 등 **실시간 동영상 처리**에 부적합
- 해결: **DCP(Dark Channel Prior)** 기법을 채택해 **빠르고 효율적인** 안개 제거 구현
- 결과: **별도 학습 없이**, **안정적인 성능**으로 **실시간** 안개 제거 성능 확보

### 2) **해상 안개 데이터셋 확보 문제**  
- 원인: AI 학습과 성능 검증을 위해 **안개가 낀 해상 환경의 항해 데이터셋**이 필요했으나, 공개된 고품질 **데이터셋 부재**
- 해결: **일반 도로 환경**에서 촬영된 안개 제거 학습용 공개 데이터셋을 확보하여 대체 데이터로 사용
- 결과: 대체 데이터로 **AI 학습 데이터셋 문제를 해결**하고, DCP 알고리즘 검증에 활용
  
### 3) **낙상 감지 모델 성능 문제**  
- 원인: 최적화되지 않은 모델을 사용할 경우 **실시간 구동**에 어려움 발생
- 해결: **YOLOv8n**과 **MoveNet Lightning**을 최종 선택해 **실시간 구동 가능**한 성능 확보 
- 결과: **낙상 감지**의 평균 **FPS 20-25**, <strong>CPU 사용률 70%</strong>로 안정적인 성능 구현

### 4) **젯슨 나노 호환성 문제**  
- 원인: GPU 사용을 위해 선택한 **젯슨 나노**에서 **호환성 문제**가 발생하여 **이상 감지 모델**이 구동되지 않음 
- 해결: **CPU 구동**에는 성공했으나, 최종적으로 **PC**에서 구동하기로 결정
- 결과: **젯슨 나노 활용 목표**는 완전히 이루지 못했지만, 최종적으로 PC에서 **안정적인 성능으로 구동 성공**

---

## 📚 7. 배운 점

- **OpenCV**, **PyTorch**, **YOLO** 등 AI 관련 지식
- 다양한 **이미지 처리 기법**(CLAHE, DCP 등)을 활용하여 **저조도 및 안개 상태**에서도 시야를 확보하는 로직을 구현한 경험
- **MQTT**를 사용한 **실시간 데이터 전송** 및 **경고 발송 시스템** 구현을 보조하며 알게 된 새로운 통신 방식
- **STT**와 **TTS**를 활용한 **자동 항해 일지 작성 및 브리핑** 시스템을 통해 **음성 인식 및 합성**의 유용성을 실감
- 충분한 성능 확보를 위한 **실시간 시스템 최적화**의 중요성
---


<div align="center">
<a href="#japanese">⬇️ 日本語バージョンへ移動 (Go to Japanese Version) ⬇️</a>
</div>

</div>

---

<div id="japanese">

### 🇯🇵 Japanese Version

# 🌊 AIベースの船舶制御室補助On-Deviceシステム
## 🏆 **Intel Edge AI 実務プロジェクト コンペティション 最優秀賞 受賞**

<img src="docs/resources/video_gif/01_Dehazing.gif" alt="01_Dehazing.gif" width="800"/>
<img src="docs/resources/video_gif/03_AD_Dehazing.gif" alt="03_AD_Dehazing.gif" width="800"/>
<img src="docs/resources/video_gif/04_PE1.gif" alt="04_PE1.gif" width="800"/>
<img src="docs/resources/video_gif/06_Server_SystemLog.gif" alt="06_Server_SystemLog.gif" height="480"/>

## 💡 1. プロジェクト概要

本プロジェクトは、**AIベースのコンピュータービジョン技術**を活用し、海上環境における船舶の航行安全性と効率性の向上を目指した**船舶制御室補助On-Deviceシステム**です。  
このシステムは、**リアルタイムで霧の中のオブジェクトを検出**し、**異常検知**を実現します。さらに、**オブジェクト追跡、姿勢推定技術**を組み合わせることで、船体および乗員の安全確保を促進します。また、**LLM**を活用し、**自動航海日誌作成とブリーフィング機能**を提供します。  
システムの主要機能としては、**デハジング（霧画像補正）**、**異常検知**、**転倒検知**、**自動航海日誌作成**などが含まれます。

### 📍 システム全体構想図
![Image](https://github.com/user-attachments/assets/aa3c5641-43c6-497d-b5ac-7b89fd1d8878)

---

## 🛠️ 2. 技術スタック

![RaspberryPi](https://img.shields.io/badge/Hardware-RaspberryPi5-A22846?style=for-the-badge&logo=raspberrypi&logoColor=white)
![JetsonNano](https://img.shields.io/badge/Hardware-Jetson%20Nano-76B041?style=for-the-badge&logo=nvidia&logoColor=white)
![IMU Sensor](https://img.shields.io/badge/Hardware-IMU%20Sensor-FF9900?style=for-the-badge&logo=generic&logoColor=white)

![Python](https://img.shields.io/badge/Language-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenVINO](https://img.shields.io/badge/Framework-OpenVINO-0078D4?style=for-the-badge&logo=intel&logoColor=white)
![PyTorch](https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![YOLO](https://img.shields.io/badge/Model-YOLOv8-FF2B2B?style=for-the-badge&logo=github&logoColor=white)
![EfficientNet](https://img.shields.io/badge/EfficientNet-B3-FF6F00?style=for-the-badge&logo=google&logoColor=white)
![MoveNet](https://img.shields.io/badge/Model-MoveNet-03A9F4?style=for-the-badge&logo=google&logoColor=white)
![MQTT](https://img.shields.io/badge/Protocol-MQTT-00B5A1?style=for-the-badge&logo=cloudsmith&logoColor=white)
![OpenCV](https://img.shields.io/badge/Library-OpenCV-5C3A00?style=for-the-badge&logo=opencv&logoColor=white)
![MariaDB](https://img.shields.io/badge/Database-MariaDB-003B57?style=for-the-badge&logo=mariadb&logoColor=white)
![PyQt6](https://img.shields.io/badge/Framework-PyQt6-41C1C1?style=for-the-badge&logo=python&logoColor=white)

---

## 🎯 3. 主要機能

- **デハジングおよび異常検知**:  
   - **CLAHE手法**および<strong>DCP(Dark Channel Prior)</strong>手法を適用し、画像の霧を除去  
   - **YOLOX-S**および**EfficientNet-B3**モデルを使用し、**異常物体をリアルタイムで検出・識別**

- **転倒検知および警告システム**:  
   - **YOLOv8n**モデルで**デッキ上の乗員**を検知  
   - **MoveNet Lightning**モデルで**乗員の姿勢を推定**し、**転倒状態を検知**した場合、直ちにサーバーへ**危険警報**を送信 
   - 特定のエリアを危険ゾーンとして設定し、ゾーン内への乗員の立ち入りを検知した場合も**警告を発信**

- **自動航海日誌作成およびブリーフィング**:  
   - <strong>LLM (大規模言語モデル)</strong>を活用  
   - <strong>STT (音声認識)</strong>と<strong>TTS (音声合成)</strong>を使用し、乗員からの**音声指示の処理、自動航海日誌の作成、およびブリーフィングの提供**を実現

- **リアルタイムデータ処理**:  
   - 各モジュールから**MQTT**を通じてデータをリアルタイムでサーバーに送信  
   - **異常検知**、**転倒検知**、**危険物体検知**などのデータを処理・保存
   - リアルタイムで処理されたデータは**モニタリングUI**を通じてコントロールルームで即座に確認可能

---

## 📘 4. 技術実装

### 1) <strong>CLAHE (Contrast Limited Adaptive Histogram Equalization)</strong>手法
   - **目的**: 低照度環境下で画像を改善し、**鮮明な視界**を確保
   - **手法**: 各画像領域で**局所的なコントラストを強調**することで、低照度時の視認性を向上

### 2) <strong>DCP (Dark Channel Prior)</strong>手法
   - **目的**: 画像から**霧を除去**し、より明確な視界を提供
   - **手法**: 画像の<strong>ダークチャネル (暗い部分)</strong>を用いて霧の濃度を推定し、画像を復元

### 3) **YOLOX-S & EfficientNet-B3**モデルを活用した**異常検知**
   - **目的**: リアルタイムで**異常物体**を検出
   - **手法**: **YOLOX-S**で候補となる物体を検出し、その後**EfficientNet-B3**モデルで異常物体の種類を識別

### 4) **YOLOv8n**モデルを活用した**転倒検知**
   - **目的**: デッキ上の**乗員オブジェクト**を検出し、**転倒**状態を検出
   - **手法**: **YOLOv8n**モデルで乗員を検出し、**MoveNet Lightning**で姿勢を推定して転倒を検出

### 5) **LLM**, **STT**, **TTS**を活用した**自動航海日誌作成およびブリーフィング**
   - **目的**: **航海日誌**を自動で作成し、**ブリーフィング**を提供
   - **手法**: **STT**で音声認識、**TTS**でリアルタイムのブリーフィング音声を提供、**LLM**で航海日誌を自動作成

---

## 👨‍💻 5. 担当役割と貢献

- **CLAHE手法**を用いて画像を改善 → 低照度環境での異常検出性能向上
- **DCP**手法を活用し**霧を除去** → 霧による視界低下を改善し、船体安全を確保、異常検出性能を向上
- **副チームリーダー**として、チームリーダー不在時に役割を代行し、プロジェクトの円滑な進行をサポート

---

## 🐞 6. トラブルシューティング

### 1) **デハジング（霧画像補正手法）モデルの性能問題**  
- 原因: 様々な霧除去モデルを試したが、バージョンの互換性や速度の問題で**リアルタイム映像処理**に不適
- 解決策: <strong>DCP(Dark Channel Prior)</strong>手法を選択し、**迅速で効率的**な霧除去を実装  
- 結果: **学習不要の手法**でありながら、**安定した性能**かつ**リアルタイム**で霧の除去を実現

### 2) **海上霧データセットの確保問題**  
- 原因: AI学習と性能検証のための**霧のかかった海上環境の航行データセット**が必要だったが、公開されている高品質な**データセット不在**
- 解決策: **一般道路環境**で撮影された霧除去学習用の公開データセットを確保し、代替データとして利用  
- 結果: 代替データを用いることで**AI学習データセットの問題を解決**し、DCPアルゴリズムの検証に活用

### 3) **転倒検知モデルの性能問題**  
- 原因: 最適化されていないモデルを使用すると、**リアルタイム動作**に問題が発生  
- 解決策: **YOLOv8n**と**MoveNet Lightning**を最終的に選択し、**リアルタイム動作可能**な性能を確保  
- 結果: **転倒検知**の平均**FPS 20-25**、<strong>CPU使用率 70%</strong>で安定した性能を実現

### 4) **Jetson Nano互換性の問題**  
- 原因: GPU活用のための**Jetson Nano**で**互換性の問題**が発生し、**異常検知モデル**作動に問題発生
- 解決策: **CPUでの動作**には成功したが、最終的にモデルの動作環境をより高性能なPCに変更することを決定  
- 結果: **Jetson Nanoへの実装目標**は達成できなかったが、最終的に**PC**で安定した動作性能を確保

---

## 📚 7. 学んだこと

- **OpenCV**、**PyTorch**、**YOLO**などAIに関連する知識  
- 様々な**画像処理手法**(CLAHE、DCPなど)を活用し、**低照度や霧の状態**でも視界を確保するロジックを実装した経験
- **MQTT**を使用した**リアルタイムデータ転送**および**警告発信システム**の構築を補助したことで、新しい通信方式に関して理解  
- **STT**と**TTS**を活用した**自動航海日誌作成およびブリーフィング**システムを通じて、**音声認識および合成**の有用性を実感  
- 実行時の性能確保のための**リアルタイムシステム最適化**の重要性を学ぶ

---

<div align="center">
<a href="#korean">⬆️ 한국어 버전으로 돌아가기 (Go back to Korean Version) ⬆️</a>
</div>

</div>

---
---

<div align="center">
<a href="#Team">⬇️ Go to Team Version ⬇️</a>
</div>

</div>

---

<div id="Team">

### 🚢 Team

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
---

<div align="center">
<a href="#korean">⬆️ 한국어 버전으로 돌아가기 (Go back to Korean Version) ⬆️</a>
</div>

</div>

---
