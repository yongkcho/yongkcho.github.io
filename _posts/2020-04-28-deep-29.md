---
title: "[Deep learning]CNN (3) Filter for Edge Detection"
date: 2020-04-28
toc: true
toc_sticky: true
header:
  teaser: 
use_math: true
categories: python udacity study deeplearning ai nural network
---

*이 포스팅은 Udacity의 Bertelsmann Technology Scholarship을 정리한 자료입니다.*  

# Lesson 3 Filter, Edge Detection 만들기 

<br>

## 1) 라이브러리 및 이미지 로드 


```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

import cv2 #pip install opencv-python을 통해 설치합니다. 
import numpy as np

%matplotlib inline

# image파일 읽어오기
image = mpimg.imread('curved_lane.jpg')

plt.imshow(image)
```


![png](https://drive.google.com/uc?id=1d4ArkPJLaemThDuODQobWFALQwzvt7R8)


## 2) 이미지를 grayscale로 변환하기


```python
# filter를 위해 grayscale로 바꾸기
gray = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)

plt.imshow(gray, cmap='gray')
```


![png](https://drive.google.com/uc?id=1LBpAZc6OpEJJdvcOgJ-SCD7HldxlNJKl)



```python
# Sobel operator을 만들어 custom kernel 만들기

# Sobel y operator로 3x3 행렬 사용
sobel_y = np.array([[ -1, -2, -1], 
                   [ 0, 0, 0], 
                   [ 1, 2, 1]])

# Sobel x operator로 3x3 행렬 사용
sobel_x = np.array([[ -1, 0, 1], 
                   [ -2, 0, 2], 
                   [ -1, 0, 1]])

# filter2D를 사용해 이미지 필터링 (inputs : grayscale image, bit-depth, kernel)  
filtered_image = cv2.filter2D(gray, -1, sobel_y)

# filter2D를 사용해 이미지 필터링 (inputs : grayscale image, bit-depth, kernel)  
filtered_image_2 = cv2.filter2D(gray, -1, sobel_x)

plt.figure(figsize = (15,15)) 
plt.imshow(filtered_image, cmap='gray')
plt.title("sobel y")
plt.show()
```


![png](https://drive.google.com/uc?id=1CwvBXwRc53sfMJFkMWH92H6s0gYPUtPE)



```python
plt.figure(figsize = (15,15))
plt.imshow(filtered_image_2, cmap='gray')
plt.title("sobel x")
plt.show()
```


![png](https://drive.google.com/uc?id=1MNbHZ5GbNWnQsXNb2e82RG0z7DjNsOKA)



```python
# 값을 낮춰서 blur 필터를 만들어보기 
blur_filter = np.array([[ 0.05, 0.2, 0.05], 
                        [ 0.2, 0.2, 0.2], 
                        [ 0.05, 0.2, 0.05]])

# filter2D를 사용해 이미지 필터링 (inputs : grayscale image, bit-depth, kernel)  
filtered_image_blur = cv2.filter2D(gray, -1, blur_filter)

plt.figure(figsize = (15,15))
plt.imshow(filtered_image_blur, cmap='gray')
plt.title("blur")
plt.show()
```


![png](https://drive.google.com/uc?id=1clDv21Oc2T93bRJsko3d5VODwTg9z6Sz)



```python
# edge dectection을 위한 필터 만들어보기 
edge_detection = np.array([[ 0.0, -1, 0], 
                        [ -1, 4, -1], 
                        [ 0, -1, 0]])

# filter2D를 사용해 이미지 필터링 (inputs : grayscale image, bit-depth, kernel) 
filtered_image_edges = cv2.filter2D(filtered_image_blur, -1, edge_detection)

plt.figure(figsize = (15,15))
plt.imshow(filtered_image_edges, cmap='gray')
plt.title("edge detection")
plt.show()
```


![png](https://drive.google.com/uc?id=1zyMSIx7uIhRygdd3q_1-AJFsaAz5ZsYs)



```python
# 5x5 필터를 사용해 edge dectection해보기 
image_2 = mpimg.imread('curved_lane.jpg')

# Convert to grayscale for filtering
gray_2 = cv2.cvtColor(image_2, cv2.COLOR_RGB2GRAY)

plt.imshow(gray_2, cmap='gray')
plt.show()

edge_detection_2 = [[0,0,-2.5,0,0],
                    [0,0,-1,0,0],
                    [-2.5,-1,12,-1,-2.5],
                    [0,0,-1,0,0],
                    [0,0,-2.5,0,0]]
edge_detection_2 = np.array(edge_detection_2)

# Filter the image using filter2D, which has inputs: (grayscale image, bit-depth, kernel)  
filtered_image_edges_2 = cv2.filter2D(gray_2, -1, edge_detection_2)

plt.figure(figsize = (15,15))
plt.imshow(filtered_image_edges_2, cmap='gray')
plt.show()
```


![png](https://drive.google.com/uc?id=1whEnXKXjt6GycRb9t2G9Z4LZOUEiorDF)



![png](https://drive.google.com/uc?id=1vuSYwuA2aJ7XO41Z0dUX3OH1hos579zR)

