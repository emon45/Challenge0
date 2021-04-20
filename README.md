# Challenge0

import os
import glob
import cv2
import random
import numpy as np

imdir = '/Users/pp/*'   # add path of file here
ext = ['png', 'jpg', 'gif']

files = []
[files.extend(glob.glob(imdir + '*.' + e)) for e in ext]

images = [cv2.imread(file) for file in files]
abc= len(images)
print (abc)
num = 0
for img in images:

    def brightness(img, low, high):
        value = random.uniform(low, high)
        hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
        hsv = np.array(hsv, dtype=np.float64)
        hsv[:, :, 1] = hsv[:, :, 1] * value
        hsv[:, :, 1][hsv[:, :, 1] > 255] = 255
        hsv[:, :, 2] = hsv[:, :, 2] * value
        hsv[:, :, 2][hsv[:, :, 2] > 255] = 255
        hsv = np.array(hsv, dtype=np.uint8)
        img = cv2.cvtColor(hsv, cv2.COLOR_HSV2BGR)
        return img


    img = brightness(img, 0.5, 3)
    cv2.imshow('Result', img)


    cv2.imwrite(str(num) + 'photos.jpg', img) # changes of brightrness photos, you will get in the pycharm project window
    num += 1
    cv2.waitKey(0)
    cv2.destroyAllWindows()
