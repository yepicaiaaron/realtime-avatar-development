# Real-Time Avatar Development

A dedicated space for tracking real-time avatar development, custom implementations, and testing models with Aaron's face.

## Overview
This repository is used for:
- 🧪 **Implementations**: Deployable code and configurations for real-time avatar models (FasterLivePortrait, Ditto, MuseTalk, etc.)
- 👤 **Custom Models**: Fine-tunes and custom implementations specifically using Aaron's face.
- ⚙️ **Pipelines**: WebRTC/Pipecat streaming setups for these avatars.

## Current Focus
We are currently focusing on integrating **FasterLivePortrait**, **Ditto**, and **MuseTalk** with **Pipecat** to achieve sub-second real-time streaming latency for conversational agents.

### Core Technologies
1. **FasterLivePortrait (TensorRT)**: Our primary driver for full facial animation due to its extreme efficiency and high frame rates.
2. **Ditto**: Exploring Ant Group's native online streaming pipeline for low-latency inference.
3. **MuseTalk**: Used for dynamic, high-quality lip-syncing over static or looping base videos of Aaron.
4. **Pipecat Framework**: Handling WebRTC transport, audio sync, Voice Activity Detection (VAD), and LLM orchestration to bypass custom streaming infrastructure.

### Development Roadmap
- [ ] Build a custom Pipecat `Action` wrapper around the FasterLivePortrait inference loop.
- [ ] Optimize TensorRT/ONNX models specifically for Aaron's base face videos.
- [ ] Stream raw `VisionImageRawFrame` data directly into the Pipecat transport.
- [ ] Deploy containerized instances using Docker Swarm / Cloud Run.