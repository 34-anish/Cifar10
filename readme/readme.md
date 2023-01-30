**readme![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.001.png)**

**Training The Model![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.001.png)**

**Installing the dependencies**

conda create -n cifar10![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.002.png)

pip install tensorflow tensorflow-gpu opencv-python os matplotlib seaborn jupyter notebook

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.003.jpeg)

Cifar10 is a dataset of 50,000 32x32 color training images and 10,000 test images, labeled over 10 categories. See more info at the![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.004.png)

CIFAR homepage

Turns out that the images are already splitted

The classes of the datasets are

classes =![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.005.png)



||["airplane","automobile","bird","cat","deer","dog","frog","horse","ship","tru||
| :- | - | :- |
|||![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.006.jpeg)||
||ck"]|||
||||
**Plotting the image**

Image can be plotted with matplotlib library![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.007.png)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.008.png)

**The weird part is the image looks like Japanese video** 😂😂😂

**Pre-processing the data**

1. Normalizing The Image's Arra
1. Reshapping the y to fit into the model

**Architecture![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.009.png)**

- Here n = 32 ,f =3 ,p =0 ,s=1

32 − 3

- + 1⌋ 1![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.010.png)

***The most important part of the project is*** **CNN Model**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.011.png) The efficiency is tested with three different models

**Model 0![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.012.png)**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.013.png) This is the first model which has

1. Convolutional Layer with 16 filters of size (3,3)
1. MaxPooling
1. Convolution Layer with 32 filters of (3,3) size with stride = 1
1. MaxPooling
1. Flatten
1. Fully Connected Layer with neurons =256
1. Final Output Layer with sigmoid activation

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.014.jpeg)

model.add(Conv2D(16, (3,3), 1, activation='relu', input\_shape=(32,32,3)))![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.015.png)

- 30 is the width of the output layer of the first convolutional layer
  - activation = 'relu' is the rectified linear unit which![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.016.png)
    - *f* (*x*) = *max*(0,*x*)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.017.png) ![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.018.jpeg)

**Parameters**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.019.png) First parameter = $$((3*3*3)+1)\*16 = 448$$

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.020.png)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.021.png) For **maxpooling**

254

- ⌋= 127 2![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.022.png)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.023.png) There wont be parameter for the max pooling.

**For second conv2D**

model.add(Conv2D(32,(3,3),1,activation='relu'))![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.024.png)

means that **32** 3\*3 filters of RGB(3) channels have stride =1

*n* − *f* + 2*p*

⌊~~ + 1⌋ ![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.025.png)*s*
- Here n = 127 ,f =3 ,p =0 ,s=1

127 − 3

- + 1⌋ 1![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.010.png)
- 125 is the width and height of its output layer
  - The chanels would be 32
    - Hence, the output shape =(None,125,125,32) **Parameters**

((*fH* ∗*fW* ∗*n*[*C*−1]) + 1) ∗*n*[*C*]

((3 ∗3 ∗16) + 1) ∗32 = 4640

**For max pooling**

125![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.026.png)

- ⌋= 62 2

**For third conv2D**

model.add(Conv2D(64,(3,3),1,activation='relu')) ![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.027.png)

means that **64** 3\*3 filters of RGB(3) channels have stride =1

*n* − *f* + 2*p*

- + 1⌋ ![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.028.png)*s*

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.029.png) Here n = 62 ,f =3 ,p =0 ,s=1

62 − 3![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.030.png)

- + 1⌋

1

- 60 is the width and height of its output layer
  - The chanels would be 64
    - Hence, the output shape =(None,60,60,64) **Parameters**

((*f* ∗*f* ∗*n*[*C*−1]) + 1) ∗*n*[*C*]

*H W*

((3 ∗3 ∗32) + 1) ∗64 = 18496

dense\_17![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.031.png)

*Parameters* = 256 ∗256 + 256 ∗1 = 65792

dense\_18![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.032.png)

*Parameters* = 256 ∗10 + 10 ∗1 = 2570                          model.compile('adam',loss='sparse\_categorical\_crossentropy',metrics=['accuracy'])![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.033.png)

**Adaptive Moment Estimation Algorithm** optmiizer is used with loss = sparse\_categorical\_entropy



![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.034.jpeg)

***model 1 and model 2 have same architecture but they differ on the architecture only***

**Model 1![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.009.png)**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.035.jpeg)

**Model 2![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.036.png)**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.037.jpeg)

`    `model\_name.add(MaxPooling2D()) ![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.038.png)

`    `model\_name.add(Conv2D(16,(3,3),1,activation='relu'))     model\_name.add(MaxPooling2D()) 

`    `model\_name.add(Conv2D(32,(3,3),1,activation='relu'))     model\_name.add(MaxPooling2D()) 

`    `model\_name.add(Flatten()) 

`    `model\_name.add(Dense(3000,activation='relu')) 

`    `model\_name.add(Dense(1000,activation='relu')) 

`    `model\_name.add(Dense(10,activation='softmax'))

Model is saved and loaded to/from the disk

model.save(os.path.join('models','model.h5'))

model = load\_model(os.path.join('models','model.h5'))\*\*strong text\*\*

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.039.png)

***GitHub allows upto 100 MB files so the h5 files cant be included but please let me know if you need this***

**Testing the result** 😊😊![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.040.png)

**Parameter Model 0 Model 1 Model 2 ![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.041.png)**Accuracy After 10th 0.7955 0.7925 0.5813 Loss After 10th epoch 0.5730 0.5719 1.1919 Parameters 91,946 3,404,042 3,404,042

**Randomly testing with test-images![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.042.png)**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.043.jpeg)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.044.jpeg)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.045.jpeg)

**Graph of accuracy and loss**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.046.png)

Graph For accuracy

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.047.png)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.048.png) Model 0 seems to be appropriate one

**Confusion Matrix**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.049.png)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.050.png)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.051.png)

**My favourite part is testing with new images typically**

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.052.jpeg)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.053.jpeg)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.054.jpeg)

![](Aspose.Words.e93a2642-f71a-4366-b568-da84d9c87bf9.055.jpeg)

**The model does have error**

***Fun Thing I did was even though there is not class for a human I wanted to know how it will classify my image***

🥁🥁🥁

TURNS OUT I'M A TRUCK🚚🚚
