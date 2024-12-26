# Video2Video Style Transfer Version 4

## Navigation
- [Overview](https://github.com/DaWelli/DIGCRE-project/blob/main/Video2Video/README.md)

## Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Workflow Overview](#workflow-overview)
- [Node Explanations](#node-explanations)

## Introduction
This is the fourth version of the Video2Video Style Transfer Project, showcasing a functional workflow for applying artistic styles to video input. This workflow is basically the same as Version 2, but with a more "refined" prompt and new checkpoints.

## Prerequisites
To run this iteration successfully, ensure the following ComfyUI extensions are installed:

1. VideoHelperSuite: For loading and combining video frames.

2. ControlNet Extension: To load and apply advanced ControlNet models.
3. AnimateDiff Loader: For integrating animation-specific AI models.

## Workflow Overview
![Version4_workflow](https://github.com/user-attachments/assets/46907bcc-636e-49a9-b946-fb51c5a165e1)


# Node Explanations

## 1. Load Video (VideoHelperSuite)

**Purpose**: Uploads the input video for processing.

**Parameters**:
- `media_batch`: Video to process.
- `frame_skip`: Specifies how many frames to skip.
- `select_every_nth`: Selects every nth frame for processing.

---

## 2. Upscale Image

**Purpose**: Increases the resolution of extracted frames.

**Parameters**:
- `width`: 1024.
- `height`: 1024.
- `upscale_method`: `nearest-exact`.

---

## 3. VAE Encode & Decode

**Purpose**:
- **VAE Encode**: Converts frames into latent space representations.
- **VAE Decode**: Converts processed latent data back into images.

---

## 4. Load Checkpoint

**Purpose**: Loads a pre-trained model for stylizing the frames.

**Model**: `NUKEColormaxAnime`.

---

## 5. Load LORA Nodes (Multiple Models)

### **LORA 1**
- **Purpose**: Fine-tunes animation style with `more_details_safetensors`.
- **Strength**: `1.0`.

### **LORA 2**
- **Purpose**: Adds texture or shading with `Hotarucontrast`.
- **Strength**: `0.4`.

### **LORA 3**
- **Purpose**: Smooth rendering with `smoothpainting_safetensors`.
- **Strength**: `0.5`.

### **LORA 4**
- **Purpose**: Smooth rendering with `LCM Lora`.
- **Strength**: `1.0`.
---

## 6. CLIP Text Encode (Prompt)

**Purpose**: Defines the artistic style and scene composition.

**Prompts**:
- **Positive Prompt**: "masterpiece, best quality, An anime-style depiction of three characters in a lush, vibrant grassy field with tall tropical trees in the background. The characters are crouched together, showing a mix of awe and joy. The first character is a middle-aged man with short brown hair, wearing a rugged denim jacket and a red scarf, looking intently forward. The second is a cheerful woman with short blonde hair, dressed in a soft orange shirt, hugging her knees. The third is an older man with a white beard, wearing a white outfit and holding a wooden cane, smiling gently. The scene includes two red and gray off-road vehicles parked behind them. The art style features bright, vivid colors, soft shading, expressive facial details, and a cinematic anime feel. The atmosphere is adventurous and slightly nostalgic, with attention to the lush greenery and a clear sky"
- **Negative Prompt**: "nsfw, nude, nudity, bad quality, worst quality, lowres, multiple limbs, multiple fingers,Realistic textures, blurry details, overly dark shadows, muted colors, hyper-realism, distorted anatomy, extra limbs, text, logos, watermark, 3D rendering, photorealism, surreal art, monochrome, unnatural lighting, low resolution, pixelated details, cluttered composition, noisy backgrounds"

---

## 7. ControlNet Nodes

### **ControlNet OpenPose**
- **Model**: `control_v11p_sd15_openpose`.
- **Purpose**: Guides the skeletal poses of the characters.
- **Strength**: `0.75`.

### **ControlNet Depth**
- **Model**: `control_v11p_sd15_depth`.
- **Purpose**: Adds depth information for better scene structure.
- **Strength**: `0.6`.

### **ControlNet LineArt**
- **Model**: `control_v11p_sd15_lineart`.
- **Purpose**: Provides line art style guidance.
- **Strength**: `0.5`.

### **ControlNet LCM/Colors**
- **Model**: `SD12_adapter_color_safetensors`.
- **Purpose**: Refines color tones and lighting in the scene.
- **Parameters**:
  - `Strength`: 0.75.
  - `start_percent`: 0.0.
  - `end_percent`: 1.0.

---

## 8. AnimateDiff Loader & Models

**Purpose**: Handles animation-specific processing using motion interpolation.

- **Model**: `improved2DMotion_improvedSD2Diff`.
- **Motion Scale**: `100`.

---

## 9. KSampler

**Purpose**: Processes latent frames for the defined style and settings.

**Parameters**:
- `steps`: `21`.
- `scheduler`: Noise scheduling method set to `karras`.

---

## 10. Video Combine (VideoHelperSuite)

**Purpose**: Combines processed frames back into a final video.

**Parameters**:
- `frame_rate`: `30 FPS`.
- `format`: `mp4`.
- `save_output`: Enabled.

---

## Output

- **Input**: A standard video file.
- **Output**: A stylized animation with detailed poses, depth, colors, and line art.
- **Format**: `mp4`, at `30 FPS`.

