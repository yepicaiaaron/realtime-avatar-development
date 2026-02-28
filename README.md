# Real-Time Avatar Development

A dedicated space for tracking real-time avatar development, custom implementations, and testing models with Aaron's face.

## Overview
This repository is used for:
- 🧪 **Implementations**: Deployable code and configurations for real-time avatar models (FasterLivePortrait, MuseTalk, HeyGen, etc.)
- 👤 **Custom Models**: Fine-tunes and custom implementations specifically using Aaron's face.
- ⚙️ **Pipelines**: WebRTC/Pipecat streaming setups for these avatars.

## Current Focus
We are currently focusing on integrating **FasterLivePortrait**, **MuseTalk**, and **HeyGen LiveAvatar** with **Pipecat** to achieve sub-second real-time streaming latency for conversational agents.

### Core Technologies
1. **FasterLivePortrait (TensorRT)**: Our primary driver for full facial animation due to its extreme efficiency and high frame rates.
   - Repo: [warmshao/FasterLivePortrait](https://github.com/warmshao/FasterLivePortrait)
   - Supports ONNX/TensorRT for real-time inference
2. **MuseTalk 1.5**: Real-time high-quality lip-syncing (30fps+ on V100) with improved visual quality and training code now available.
   - Repo: [TMElyralab/MuseTalk](https://github.com/TMElyralab/MuseTalk)
   - Training code open-sourced (April 2025)
   - Enhanced clarity and identity consistency in v1.5
3. **HeyGen LiveAvatar**: Native Pipecat integration available for hosted real-time avatar streaming.
   - Pipecat service: `pipecat.services.heygen.video.HeyGenVideoService`
   - Example: [43a-heygen-video-service.py](https://github.com/pipecat-ai/pipecat/blob/main/examples/foundational/43a-heygen-video-service.py)
4. **Pipecat Framework (v0.0.103+)**: Handling WebRTC transport, audio sync, Voice Activity Detection (VAD), and LLM orchestration.
   - New: HeyGen LiveAvatar support
   - New: Deepgram SageMaker TTS support
   - Improved: Audio context management, STT keepalive mechanisms

### Recent Updates (February 2026)

#### Pipecat v0.0.103 (Released 2026-02-20)
- **HeyGen LiveAvatar Integration**: Native support for real-time interactive avatars via `HeyGenVideoService`
- **DeepgramSageMakerTTSService**: New service for Deepgram TTS on AWS SageMaker endpoints
- **Improved TTS Context Management**: Better handling of concurrent TTS requests with `reuse_context_id_within_turn`
- **STT Keepalive**: Prevents idle connection timeouts in ServiceSwitcher setups
- **UserIdleTimeoutUpdateFrame**: Dynamic user idle detection control

#### MuseTalk 1.5 (Released March 2025)
- Training code now open-sourced
- Two-stage training strategy with spatio-temporal sampling
- Improved visual quality and lip-sync accuracy
- GAN loss and sync loss integration

### Development Roadmap
- [x] Evaluate HeyGen LiveAvatar as hosted alternative (native Pipecat support available)
- [ ] Build a custom Pipecat `Action` wrapper around the FasterLivePortrait inference loop
- [ ] Optimize TensorRT/ONNX models specifically for Aaron's base face videos
- [ ] Stream raw `VisionImageRawFrame` data directly into the Pipecat transport
- [ ] Deploy containerized instances using Docker Swarm / Cloud Run
- [ ] Train custom MuseTalk model on Aaron's face dataset

## Quick Start - HeyGen LiveAvatar with Pipecat

```python
from pipecat.services.heygen.video import HeyGenVideoService
from pipecat.services.heygen.api_liveavatar import LiveAvatarNewSessionRequest
from pipecat.services.heygen.client import ServiceType

heygen = HeyGenVideoService(
    api_key=os.getenv("HEYGEN_LIVE_AVATAR_API_KEY"),
    service_type=ServiceType.LIVE_AVATAR,
    session=session,
    session_request=LiveAvatarNewSessionRequest(
        is_sandbox=True,
        avatar_id="dd73ea75-1218-4ef3-92ce-606d5f7fbc0a",  # Sandbox avatar
    ),
)
```

## References

- [Pipecat Documentation](https://docs.pipecat.ai)
- [FasterLivePortrait](https://github.com/warmshao/FasterLivePortrait)
- [MuseTalk](https://github.com/TMElyralab/MuseTalk)
- [LivePortrait (Original)](https://github.com/KlingAIResearch/LivePortrait)
- [HeyGen LiveAvatar Docs](https://docs.liveavatar.com/)