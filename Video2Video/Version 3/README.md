# Video2Video Style Transfer Version 3

## Navigation
- [Overview](https://github.com/DaWelli/DIGCRE-project/blob/main/Video2Video/README.md)

## Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Workflow Overview](#workflow-overview)
- [Node Explanations](#node-explanations)
- [Output](#output)

## Introduction
This is the third version of the Video2Video Style Transfer Project, showcasing a functional workflow for applying artistic styles to video input. This workflow is basically the same as Version 2, but with a more "refined" prompt and new checkpoints.

## Prerequisites
To run this iteration successfully, ensure the following ComfyUI extensions are installed:

1. VideoHelperSuite: For loading and combining video frames.

2. ControlNet Extension: To load and apply advanced ControlNet models.
3. AnimateDiff Loader: For integrating animation-specific AI models.

## Workflow Overview
![Version3_workflow](https://github.com/user-attachments/assets/e88783d3-cd47-4ae9-9a26-10a805da61f4)


# Node Explanations

## 1. Load Video (VideoHelperSuite)

**Purpose**: Uploads the video file for processing.

**Parameters**:
- `media_batch`: Specifies the video to be processed.
- `frame_skip`: Defines how many frames to skip.
- `select_every_nth`: Extracts every nth frame from the video.

---

## 2. Upscale Image

**Purpose**: Enhances the resolution of the extracted video frames.

**Parameters**:
- `width`: Output width, set to 1024.
- `height`: Output height, set to 1024.
- `upscale_method`: Specifies the upscaling method, set to nearest-exact.

---

## 3. VAE Encode & Decode

**Purpose**:
- **VAE Encode**: Converts video frames into latent representations for processing.
- **VAE Decode**: Converts latent representations back into images after processing.

---

## 4. Load Checkpoint

**Purpose**: Loads the pre-trained model for further artistic transformations.

**Model**: `SD1.5-AbyssOrangeMix2`.

---

## 5. Load VAE

**Purpose**: Loads the VAE model used for encoding and decoding frames.

**Model**: `SD2.1-768-EMA-pruned`.

---

## 6. Load LORA

**Purpose**: Loads the LORA model to enhance specific features or styles.

**Model**: `sdxl_lcm_lora_safetensors`.

**Parameters**:
- `strength_model`: Set to 1.0.
- `strength_clip`: Set to 1.0.

---

## 7. CLIP Text Encode (Prompt)

**Purpose**: Defines the artistic style using natural language prompts.

**Prompts**:
- **Positive Prompt**: "masterpiece, best quality, An anime-style depiction of three characters in a lush, vibrant grassy field with tall tropical trees in the background. The characters are crouched together, showing a mix of awe and joy. The first character is a middle-aged man with short brown hair, wearing a rugged denim jacket and a red scarf, looking intently forward. The second is a cheerful woman with short blonde hair, dressed in a soft orange shirt, hugging her knees. The third is an older man with a white beard, wearing a white outfit and holding a wooden cane, smiling gently. The scene includes two red and gray off-road vehicles parked behind them. The art style features bright, vivid colors, soft shading, expressive facial details, and a cinematic anime feel. The atmosphere is adventurous and slightly nostalgic, with attention to the lush greenery and a clear sky"
- **Negative Prompt**: "nsfw, nude, nudity, bad quality, worst quality, lowres, multiple limbs, multiple fingers,Realistic textures, blurry details, overly dark shadows, muted colors, hyper-realism, distorted anatomy, extra limbs, text, logos, watermark, 3D rendering, photorealism, surreal art, monochrome, unnatural lighting, low resolution, pixelated details, cluttered composition, noisy backgrounds"

---

## 8. Advanced ControlNet OpenPose Model

**Purpose**: Uses the OpenPose ControlNet model for skeletal guidance and poses.

**Model**: `control_v11p_sd15_openpose`.

**Parameters**:
- `strength`: Set to 0.75.
- `start_percent`: Set to 0.0.
- `end_percent`: Set to 0.796.

---

## 9. ControlNet Depth Model

**Purpose**: Uses a depth estimation model for further transformations.

**Model**: `control_v11p_sd15_depth`.

**Parameters**:
- `strength`: Set to 0.6.
- `start_percent`: Set to 0.0.
- `end_percent`: Set to 0.756.

---

## 10. ControlNet LineArt Model

**Purpose**: Uses the LineArt ControlNet model for line art guidance.

**Model**: `control_v11p_sd15_lineart`.

**Parameters**:
- `strength`: Set to 0.5.
- `start_percent`: Set to 0.0.
- `end_percent`: Set to 0.75.

---

## 11. AnimateDiff Loader

**Purpose**: Loads the model used for animation-specific processing and frame interpolation.

---

## 12. KSampler

**Purpose**: Processes the latent frames to apply the specified style.

**Parameters**:
- `steps`: Set to 21.
- `scheduler`: Noise scheduling method, set to karras.

---

## 13. Video Combine (VideoHelperSuite)

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

https://github.com/DaWelli/DIGCRE-project/blob/main/Video2Video/Version%203/Version3_output.mp4


