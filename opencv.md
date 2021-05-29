## OpenCV

Import
```python
import cv2
```

Load Image
```python
# Grey scale
image = cv2.imread('path')

rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

Pixel values
```python
h = image.shape[0]
w = image.shape[1]

for y in range(0, h):
    for x in range(0, w):
        channel_1 = image[y, x, 0]
        channel_2 = image[y, x, 1]
        channel_3 = image[y, x, 2]
        
        print(channel_1, channel_2, channel_3)
```

Process video
```python
cap = cv2.VideoCapture('input.mp4')
fps = cap.get(cv2.CAP_PROP_FPS)
width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
resolution = (int(width), int(height))

codec = cv2.VideoWriter_fourcc(*'MP4V')
out = cv2.VideoWriter(root_dir + 'output.mp4', codec, fps, resolution)

while (cap.isOpened()):
    
    ret, frame = cap.read()
    if ret == True:
        out.write(frame)

    else:
        break

cap.release()
out.release()
```
