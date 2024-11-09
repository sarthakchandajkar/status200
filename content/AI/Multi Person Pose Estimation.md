---
title: Multi Person Pose Estimation
aliases: 
draft: false
tags:
  - AI
author:
  - Sarthak Chandajkar
---
This blog is about the new model that **Google** has released called the ***Movenet*** model for multi person pose estimation.

This model is built on top of these 3 papers:
- MobileNetv2: [https://arxiv.org/pdf/1801.04381.pdf](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbkZ3TnRob0F2S0V6eFd4NWJjMEJuUUhkb2YyQXxBQ3Jtc0treVhKa0c2eFZxSEl1b19hemw5OWRwVjg3bGpsRGZtOUpqT3JiQ0Z4VWFzanlRSk9DRi13LXpsTGpFYUhmQkZvRWN3TnpXcERyZ2tEdFNoSkZuaWRObnBOSWxtLUcxd0hqUkpVZ2xUS21uRGxxMWtuNA&q=https%3A%2F%2Farxiv.org%2Fpdf%2F1801.04381.pdf&v=KC7nJtBHBqg) - backbone network
- Feature Pyramid Networks: [https://arxiv.org/pdf/1612.03144.pdf](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa1l5SngxZkZDSGM0ZkxVWURIcU9INEM4QV92UXxBQ3Jtc0tucmF2UExaVFJlY1c1bXNqNmp3eFRqaHUyMW1hcW9kSTQxNXlpQ3ZqZjl3RWdKZVRlcWVBUXd5T2pwU3ZDWVhheXQyMkppc2xnX1VEb1NRZDlfVGJSVE5zNWVrME5qUWZzR2wtSS1zeDZLeWdjTExzQQ&q=https%3A%2F%2Farxiv.org%2Fpdf%2F1612.03144.pdf&v=KC7nJtBHBqg) - feature extraction
- CenterNet: [https://arxiv.org/pdf/1904.07850.pdf](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbm9JS0pjeG5rMWhIMFltVFRoQVFYVWwwZTZ5QXxBQ3Jtc0tsWXlDc2NxSDZ5cV8wQ2VzbVc1am95RXlYSVJEak8xQzlvdjQyaTRpbGNrcWdCbmVRY185SHdjemFBRlZDaFViZlk0MlhjZUdROXotU2k2Z0dZMlcyVUU0LWVNdmRobWkxbm1UYzEyQkNMdGpFeXJjSQ&q=https%3A%2F%2Farxiv.org%2Fpdf%2F1904.07850.pdf&v=KC7nJtBHBqg) - prediction heads - the layer that outputs the key points.

## Steps for the project

1. Install Multi Person Movenet : [[Tensorflow]] and [[Tensorflow Hub]]
2. Make Detections using live video feed and webcam
3. Draw key points and edges

## How it works

1. Install Tensorflow and Tensorflow Hub
2. Load the model
3. Make detections from videos, camera and render.



