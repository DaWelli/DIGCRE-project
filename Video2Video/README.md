# Video2Video Style Transfer Project

This project implements video2video style transfer using a node-based workflow. The following steps and nodes explain the methodology and structure of the project.

## Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Workflow Overview](#workflow-overview)
- [Node Explanations](#node-explanations)
- [Output](#output)

## Introduction
The video2video style transfer generates a stylized video by processing an original video with advanced AI models. Techniques such as text2image modeling, upscaling, and ControlNet are utilized.

## Prerequisites
1. GPU with CUDA support for efficient processing
2. Input video to upload (MP4 or similar formats)
3. Required extensions (specific to the nodes used):
   - **ControlNet Extension**: For nodes related to advanced control.
   - **AnimateDiff Extension**: For temporal consistency and animation.
   - **Upscaler Extension**: For image scaling.
   - **VideoHelperSuite Extension**: For video handling (loading and combining frames).

## Workflow Overview
The workflow consists of several nodes that are connected step-by-step to process the input video and produce a stylized output video.
![V1](https://github.com/user-attachments/assets/adb2bef3-62cf-4d72-9893-8d214007e88b)

## Node Explanations

### 1. **Load Video (Upload)**
- **Description:** This node uploads the original video.
- **Extension Required:** VideoHelperSuite.
- **Settings:**
  - `video`: Choose the input video.
  - `frame_count`: Number of frames to process.
  - `force_size`: Optional resizing of the video.
  - `select_every_nth`: Option to process every nth frame.

### 2. **Upscale Image**
- **Description:** Upscales each video frame to a higher resolution.
- **Extension Required:** Upscaler Extension.
- **Settings:**
  - `upscale_method`: `nearest-exact` for precise scaling.
  - `width` and `height`: Target resolution (e.g., 1080x720).

### 3. **VAE Encode / Decode**
- **Description:** Converts images into latent representations (Encode) and back into pixel images (Decode) after processing.
- **Extension Required:** Diffusers Library.
- **Input:** Frames from the uploaded video.


### 4. **Load Checkpoint**
- **Description:** Loads the pre-trained model (e.g., Stable Diffusion).
- **Extension Required:** Core Stable Diffusion Framework.
- **Settings:**
  - `ckpt_name`: Name of the checkpoint file (e.g., `v1-5-pruned.safetensors`).

### 5. **CLIP Text Encode (Prompt)**
- **Description:** Defines the text prompt that describes the style and content of the video.
- **Extension Required:** Core Stable Diffusion Framework.
- **Positive Prompts:**
  - Example: "masterpiece, best quality, old man crouching down next to 2 people, ...".
- **Negative Prompts:**
  - Example: "bad quality, worst quality, nsfw, nude, ...".

### 6. **Load Advanced ControlNet Model**
- **Description:** Loads the ControlNet model to allow fine control over the generated content.
- **Extension Required:** ControlNet Extension.
- **Settings:**
  - `control_v11p_sd15_lineart.pth`: Model for lineart rendering.

### 7. **Apply Advanced ControlNet**
- **Description:** Applies the ControlNet model with the selected settings.
- **Extension Required:** ControlNet Extension.
- **Settings:**
  - `strength`: 0.5 for balanced style changes.
  - `start_percent` and `end_percent`: Controls application over video sections.

### 8. **KSampler**
- **Description:** Generates latent representations and transforms them based on the prompt.
- **Extension Required:** Diffusers Library.
- **Settings:**
  - `steps`: Number of diffusion steps (e.g., 21).
  - `cfg`: Classification guidance (e.g., 7.0).
  - `scheduler_name`: Diffusion algorithm (e.g., `ddpmpp_2m`).

### 9. **Video Combine**
- **Description:** Combines the generated frames into a video.
- **Extension Required:** VideoHelperSuite.
- **Settings:**
  - `frame_rate`: Frame rate of the output video (e.g., 30 FPS).
  - `format`: Video format (e.g., `video/h264-mp4`).
  - `save_output`: Saves the output video.

### 10. **AnimateDiff Loader**
- **Description:** Ensures temporal coherence using motion LORAs and layer effects.
- **Extension Required:** AnimateDiff Extension.
- **Settings:**
  - `model_name`: Model for temporal animations (e.g., `temporaldiff-v1-animatediff`).
  - `beta_schedule`: Schedule for weighting (e.g., `sqrt_linear`).

## Output
The final stylized video is saved as an MP4 file and made available in the target directory.

---

## Contact
If you have questions or encounter issues, feel free to contact me via [GitHub Issues](#).

Good luck with your video-to-video style transfer project!

