# Image2Image Style Transfer Project

Since I also wanted to test how well Image2Image would work for my project, I decided to give it a try.

### Navigation

- [Main](https://github.com/DaWelli/DIGCRE-project/blob/main/README.md)

## Introduction
The Image2Image style transfer generates a stylized video by processing an original video frame-by-frame using advanced AI models to alter each individual frame.

## Prerequisites
I strongly recommend that you install ComfyUI Manager, this extension allows you an easy way to install all custom nodes I have used. For my process, you'll also need FFmpeg to extract each frame from the clip.

## Workflow Overview

![Image2Image_workflow](https://github.com/user-attachments/assets/44601eef-550f-4199-984f-894b4876869b)

## Work Explanations

First, I'll extract each frame with FFmpeg. Then, I’ll feed every single frame into the pipeline and convert them. After the generation, I’ll put everything back together. I'll also need to extract the audio from the original clip and combine it with the output.

## Conclusion to Image2Image

I think I'll stick with Video2Video conversion. The process, although it takes longer, is much easier and smoother. I'm not really happy with the outputs due to the flickering and random style changes between the frames.
