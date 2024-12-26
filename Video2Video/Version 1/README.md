# Video2Video Style Transfer Version 1

## Navigation
- [Overview](https://github.com/DaWelli/DIGCRE-project/blob/main/Video2Video/README.md)

## Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Workflow Overview](#workflow-overview)
- [Node Explanations](#node-explanations)

## Introduction
This is the initial version of the Video2Video Style Transfer Project, showcasing a functional workflow for applying artistic styles to video input.

## Prerequisites
To run this iteration successfully, ensure the following ComfyUI extensions are installed:

1. VideoHelperSuite: For loading and combining video frames.
2. ControlNet Extension: To load and apply advanced ControlNet models.
3. AnimateDiff Loader: For integrating animation-specific AI models.

## Workflow Overview
![Version1_workflow](https://github.com/user-attachments/assets/3db53a4d-b7c3-46d3-b046-61f1afaf3389)




## Node Explanations

### 1. Load Video (VideoHelperSuite)

**Purpose**: Uploads the video file for processing.

**Parameters**:
- `media_batch`: Specifies the video to be processed.
- `frame_skip`: Defines how many frames to skip.
- `extract_every`: Sets the interval for extracting frames from the video.

### 2. Upscale Image

**Purpose**: Enhances the resolution of the extracted video frames.

**Parameters**:
- `width`: Output width, set to 1024.
- `height`: Output height, set to 720.
- `upscale_method`: Specifies the upscaling method, set to nearest-exact.

### 3. VAE Encode & Decode

**Purpose**:
- **VAE Encode**: Converts video frames into latent representations for processing.
- **VAE Decode**: Converts latent representations back into images after processing.

### 4. Load Advanced ControlNet Model

**Purpose**: Loads the ControlNet model used to guide artistic transformations.

**Model**: `config_v1p_sd15_lineart_ph`

### 5. Apply Advanced ControlNet

**Purpose**: Integrates the ControlNet model into the workflow and applies its effects to the video frames.

**Parameters**:
- `strength`: Controls how strongly the style is applied, set to 0.5.
- `start_percent`: Sets the starting point for the style, set to 0.0.
- `end_percent`: Sets the ending point for the style, set to 1.0.

### 6. CLIP Text Encode (Prompt)

**Purpose**: Generates artistic style effects using natural language prompts.

**Prompts**:
- **Positive Prompt**: "masterpiece, best quality, old man crouching down next to 2 people, a man and a woman, landscape, red jeep in background, scenery, close up, oil painting, water color, cyberpunk, dystopian, anime, neon lights"
- **Negative Prompt**: "bad quality, worst quality, nsfw, nude, lowres"

### 7. KSampler

**Purpose**: Processes the latent frames to apply the style specified by the prompts.

**Parameters**:
- `steps`: Number of processing steps, set to 21.
- `scheduler`: Noise scheduling method, set to karras.

### 8. AnimateDiff Loader

**Purpose**: Loads the model used for animation-specific processing and frame interpolation.

### 9. Video Combine (VideoHelperSuite)

**Purpose**: Combines the processed frames back into a video.

**Parameters**:
- `frame_rate`: Sets the output video frame rate, set to 30.
- `format`: Specifies the output video format, set to .mp4.

---

### Output

- **Input Video**: A regular video file provided by the user.
- **Output Video**: A stylized video resembling anime or other artistic styles.
- **Format**: .mp4, processed at 30 FPS (like my original clip).
