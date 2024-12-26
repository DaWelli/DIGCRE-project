# Video2Video Style Transfer Version 2

## Navigation
- [Overview](https://github.com/DaWelli/DIGCRE-project/blob/main/Video2Video/README.md)

## Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Workflow Overview](#workflow-overview)
- [Node Explanations](#node-explanations)
- [Output](#output)

## Introduction
This is the second version of the Video2Video Style Transfer Project, showcasing a functional workflow for applying artistic styles to video input.

## Prerequisites
To run this iteration successfully, ensure the following ComfyUI extensions are installed:

1. VideoHelperSuite: For loading and combining video frames.

2. ControlNet Extension: To load and apply advanced ControlNet models.
3. AnimateDiff Loader: For integrating animation-specific AI models.

## Workflow Overview
![Version2](https://github.com/user-attachments/assets/0afcfeb7-944d-4a72-a27f-e81d92ac484d)

# Node Explanations

## 1. Load Video (VideoHelperSuite)

**Purpose**: Uploads the video file for processing.

**Parameters**:
- `media_batch`: Specifies the video to be processed.
- `frame_skip`: Defines how many frames to skip.
- `extract_every_nth`: Extracts every nth frame from the video.

---

## 2. Upscale Image

**Purpose**: Enhances the resolution of the extracted video frames.

**Parameters**:
- `width`: Output width, set to 1024.
- `height`: Output height, set to 960.
- `upscale_method`: Specifies the upscaling method, set to nearest-exact.

---

## 3. VAE Encode & Decode

**Purpose**:
- **VAE Encode**: Converts video frames into latent representations for processing.
- **VAE Decode**: Converts latent representations back into images after processing.

---

## 4. Load Checkpoint

**Purpose**: Loads the pre-trained model for further artistic transformations.

**Model**: `v1.5-ground-stable-diffusion`.

---

## 5. Load VAE

**Purpose**: Loads the VAE model used for encoding and decoding frames.

**Model**: `vae-ft-mse-840000-ema-pruned`.

---

## 6. Load LORA

**Purpose**: Loads the LORA model to enhance specific features or styles.

**Model**: `sdxl_lrm_lora_safetensors`.

**Parameters**:
- `strength_model`: Set to 1.0.
- `strength_clip`: Set to 1.0.

---

## 7. CLIP Text Encode (Prompt)

**Purpose**: Defines the artistic style using natural language prompts.

**Prompts**:
- **Positive Prompt**: "Masterpiece, best quality, anime, cinematic..."
- **Negative Prompt**: "Bad quality, NSFW, low-res..."

---

## 8. Advanced ControlNet LineArt Model

**Purpose**: Loads and applies the ControlNet model for line art guidance.

**Model**: `control_v11p_sd15_lineart`.

**Parameters**:
- `strength`: Set to 0.3.
- `start_percent`: Set to 0.0.
- `end_percent`: Set to 0.79.

---

## 9. ControlNet Depth Model

**Purpose**: Uses a depth estimation model for further transformations.

**Model**: `control_v11p_sd15_depth`.

**Parameters**:
- `strength`: Set to 0.5.
- `start_percent`: Set to 0.0.
- `end_percent`: Set to 0.79.

---

## 10. AnimateDiff Loader

**Purpose**: Loads the model used for animation-specific processing and frame interpolation.

---

## 11. KSampler

**Purpose**: Processes the latent frames to apply the specified style.

**Parameters**:
- `steps`: Set to 21.
- `scheduler`: Noise scheduling method, set to karras.

---

## 12. Video Combine (VideoHelperSuite)

**Purpose**: Combines the processed frames back into a video.

**Parameters**:
- `frame_rate`: Set to 30.
- `format`: Specifies the output video format, set to .mp4.

---

## Output

- **Input Video**: A regular video file provided by the user.
- **Output Video**: A stylized video resembling anime or other artistic styles.
- **Format**: .mp4, processed at 30 FPS.





## Output






