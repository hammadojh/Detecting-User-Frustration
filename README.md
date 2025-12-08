# Detecting User Frustration - Project Progress Tracker

## Overview
Research project on predicting user frustration in task-oriented dialogue systems, with focus on one-turn-ahead forecasting for human-robot interaction.

## Key Research Questions
- **RQ1**: Text-only frustration prediction accuracy
- **RQ2**: Multi-modal (text + vision) improvement
- **RQ3**: User-persona vector integration
- **RQ4**: Model efficiency for real-time deployment
- **RQ5**: Cross-domain transfer learning

## Progress


### Todo

- **Experiment E3**: Cross-domain robustness testing (transfer to DailyDialog/MELD)
- **Experiment E2**: Multi-modal fusion (text + vision) with User-VLM integration
- **Pepper Integration**: User-VLM vision encoder integration and ROS bridge setup
- **Wizard-of-Oz Pilot (E4)**: 30 live Pepper sessions with human-escalation measurement

### Completed

- ~~**Data Preprocessing**: EmoWOZ label shifting script implemented ([load_emowoz.py](https://github.com/hammadojh/predict_frustration))~~
- ~~**Model M1 (BERT-CLS)**: ✅ **Complete** - Macro-F1: **0.7156** (3.1x better than target), Latency: **10.07ms** ([report](https://github.com/hammadojh/predict_frustration/blob/main/reports/report_1_M1_BERT_CLS.md))~~
- ~~**Model M2 (RoBERTa-CLS)**: ✅ **Complete** - Implemented and evaluated ([report](https://github.com/hammadojh/predict_frustration/blob/main/reports/report_2_M2_RoBERTa_CLS.md))~~
- ~~**Model M3 (RoBERTa-GRU)**: ✅ **Complete** - Macro-F1: **0.7408**, Latency: **11.57ms** ([report](https://github.com/hammadojh/predict_frustration/blob/main/reports/report_3_M3_RoBERTa_GRU.md))~~
- ~~**Model M4 (DialoGPT)**: ✅ Implemented (notebook available)~~
- ~~**Training Pipeline**: Loss functions, optimizers, hyperparameter tuning implemented~~
- ~~**User Features**: Feature engineering implemented (Phase 2: feature extractors, Phase 3: ablation studies)~~
- ~~**Experiments Phase 1**: Baseline models implemented and evaluated~~
- ~~**Experiments Phase 2**: Feature-based models with comprehensive feature extraction~~
- ~~**Experiments Phase 3**: Advanced models with ablation studies and feature selection~~
- ~~**Experiment E1 (Text-only)**: ✅ Completed - All text-only models (M1-M4) evaluated on EmoWOZ~~



## Project Files

### 📄 [Frustration Prediction in Task-Oriented Dialogs.txt](resources/Frustration%20Prediction%20in%20Task-Oriented%20Dialogs.txt)
**Main research proposal** - Comprehensive proposal covering background, related work, research questions, and proposed method.

### 📄 [Proposal One-Turn-Ahead Frustration Forecasting](resources/Proposal%20One-Turn-Ahead%20Frustration%20Forecasting%20for%20Task-Oriented%20Human-Robot%20Dialogue.md)
**Detailed HRI proposal** - 8-week timeline with experiments, expected contributions, and risks/mitigation.

### 📄 [Joint project HRI -- Internal](resources/Joint%20projexct%20HRI%20--%20Internal%20.md)
**Collaboration notes** - Joint project with Dr. Chetouani focusing on advanced user modeling.

### 📄 [User Frustration.md](resources/User%20Frustration.md)
**Research notes** - Reading list, keywords, and relevant paper links.

## References
- [HARMONI Project](https://github.com/hamedR96/HARMONI/tree/english-app)
- [Frustration Detection Repo](https://github.com/hammadojh/frustration_detection)
- [Predict Frustration Repo](https://github.com/hammadojh/predict_frustration) 

