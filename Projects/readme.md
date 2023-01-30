# Training The Model

## Installing the dependencies

`conda create -n cifar10`
`pip install tensorflow tensorflow-gpu opencv-python os matplotlib seaborn`
`jupyter notebook`

![74c6601faf3834730fe8abc044970379.png](../_resources/74c6601faf3834730fe8abc044970379.png)

> Cifar10 is a dataset of 50,000 32x32 color training images and 10,000 test images, labeled over 10 categories. See more info at the
> [CIFAR homepage](https://www.cs.toronto.edu/~kriz/cifar.html)

Turns out that the images are already splitted

> The classes of the datasets are
> `classes = ["airplane","automobile","bird","cat","deer","dog","frog","horse","ship","truck"]`
> ![05cf3c2c430648afea69bad37561f945.png](../_resources/05cf3c2c430648afea69bad37561f945.png)

## Plotting the image

Image can be plotted with `matplotlib` library
![bac87205bdc8d568555a8ad506000d6a.png](../_resources/bac87205bdc8d568555a8ad506000d6a.png)
The weird part is the image looks like Japanese video 😂😂😂

## Pre-processing the data

1.  Normalizing The Image's Arra
2.  Reshapping the y to fit into the model

# Architecture

***The most important part of the project is*** **CNN Model**

- The efficiency is tested with three different models

# Model 0

- This is the first model which has

1.  Convolutional Layer with 16 filters of size (3,3)
2.  MaxPooling
3.  Convolution Layer with 32 filters of (3,3) size with stride = 1
4.  MaxPooling
5.  Flatten
6.  Fully Connected Layer with neurons =256
7.  Final Output Layer with sigmoid activation

![5fffe48b65271f1a888100120e703121.png](../_resources/5fffe48b65271f1a888100120e703121.png)
`model.add(Conv2D(16, (3,3), 1, activation='relu', input_shape=(32,32,3)))`

- $$
    \lfloor \frac{n-f+2p}{s} +1\rfloor
    
    $$
    
- Here n = 32 ,f =3 ,p =0 ,s=1
- $$
    \lfloor \frac{32-3}{1} +1\rfloor
    
    $$
    
- 30 is the width of the output layer of the first convolutional layer
- `activation = 'relu'` is the rectified linear unit which
- $$
    f(x) = max(0,x)
    
    $$
    
- ![80cc70ae7c590668dd8e1f4806b7dcdd.png](../_resources/80cc70ae7c590668dd8e1f4806b7dcdd.png)
- **Parameters**
- First parameter =

$$
((3*3*3)+1)*16 = 448

$$

![05f62c6e7206ff63052a510878870956.png](../_resources/05f62c6e7206ff63052a510878870956.png)

- For **maxpooling**
- $$
    \lfloor \frac{254}{2}\rfloor =127
    
    $$
    
- There wont be parameter for the max pooling.

## For second conv2D

`model.add(Conv2D(32,(3,3),1,activation='relu'))`
means that **32** 3*3 filters of RGB(3) channels have stride =1

- $$
    \lfloor \frac{n-f+2p}{s} +1\rfloor
    
    $$
    
- Here n = 127 ,f =3 ,p =0 ,s=1
- $$
    \lfloor \frac{127-3}{1} +1\rfloor
    
    $$
    
- 125 is the width and height of its output layer
- The chanels would be 32
- Hence, the output shape =(None,125,125,32)
    **Parameters**

$$
((f_{H}*f_{W}*n^{[C-1]})+1)*n^{[C]} 

$$

$$
((3*3*16)+1)*32=4640

$$

### For max pooling

- $$
    \lfloor \frac{125}{2}\rfloor =62
    
    $$
    

## For third conv2D

`model.add(Conv2D(64,(3,3),1,activation='relu'))`
means that **64** 3*3 filters of RGB(3) channels have stride =1

- $$
    \lfloor \frac{n-f+2p}{s} +1\rfloor
    
    $$
    
- Here n = 62 ,f =3 ,p =0 ,s=1
- $$
    \lfloor \frac{62-3}{1} +1\rfloor
    
    $$
    
- 60 is the width and height of its output layer
- The chanels would be 64
- Hence, the output shape =(None,60,60,64)
    **Parameters**

$$
((f_{H}*f_{W}*n^{[C-1]})+1)*n^{[C]} 

$$

$$
((3*3*32)+1)*64=18496

$$

`dense_17`

$$
Parameters = 256*256+256*1 = 65792

$$

`dense_18`

$$
Parameters = 256*10+10*1 = 2570

$$

`model.compile('adam',loss='sparse_categorical_crossentropy',metrics=['accuracy'])`
**Adaptive Moment Estimation Algorithm** optmiizer is used with loss = sparse\_categorical\_entropy
![c304030b501123a10230684a7be47ae7.png](../_resources/c304030b501123a10230684a7be47ae7.png)

***model 1 and model 2 have same architecture but they differ on the architecture only***

# Model 1

![4a8736de7ca874e05d195071b337e1c5.png](../_resources/4a8736de7ca874e05d195071b337e1c5.png)

# Model 2

![24ae853676ed70d2649b40ed702ec668.png](../_resources/24ae853676ed70d2649b40ed702ec668.png)

```model_name.add(Conv2D(8,
    model_name.add(MaxPooling2D())
    model_name.add(Conv2D(16,(3,3),1,activation='relu'))
    model_name.add(MaxPooling2D())
    model_name.add(Conv2D(32,(3,3),1,activation='relu'))
    model_name.add(MaxPooling2D())
    model_name.add(Flatten())
    model_name.add(Dense(3000,activation='relu'))
    model_name.add(Dense(1000,activation='relu'))
    model_name.add(Dense(10,activation='softmax'))
```

Model is saved and loaded to/from the disk

```
model.save(os.path.join('models','model.h5'))
model = load_model(os.path.join('models','model.h5'))**strong text**
```

![f928a42d89c759a08ea44e23cf254f4e.png](../_resources/f928a42d89c759a08ea44e23cf254f4e.png)
***GitHub allows upto 100 MB files so the h5 files cant be included but please let me know if you need this**

# Testing the result 😊😊

| Parameter | Model 0 | Model 1 | Model 2 |
| --- | --- | --- | --- |
| Accuracy After 10th | 0.7955 | 0.7925 | 0.5813 |
| Loss After 10th epoch | 0.5730 | 0.5719 | 1.1919 |
| Parameters | 91,946 | 3,404,042 | 3,404,042 |

# Randomly testing with test-images
![bacfcac286de7b3b26dd23b3a3dd1b98.png](../_resources/bacfcac286de7b3b26dd23b3a3dd1b98.png)
![0b126a1a06f001ff2cfcf09e9d8382e9.png](../_resources/0b126a1a06f001ff2cfcf09e9d8382e9.png)
![fc1a835566eb999e308ca9d9160a83f1.png](../_resources/fc1a835566eb999e308ca9d9160a83f1.png)
## Graph of accuracy and loss 
![ddd5f433c8725d7f9962084242e78fbf.png](../_resources/ddd5f433c8725d7f9962084242e78fbf.png)
Graph For accuracy
![8b5180891d4fbd6a75c9fc2e1b1688be.png](../_resources/8b5180891d4fbd6a75c9fc2e1b1688be.png)
## Confusion Matrix
![1980dc695c90646184f7d1a3789b36ad.png](../_resources/1980dc695c90646184f7d1a3789b36ad.png)
![10ea11d649a74106096397bf9f00b638.png](../_resources/10ea11d649a74106096397bf9f00b638.png)
![7fc332b395636b9b00f236f9e5645cb2.png](../_resources/7fc332b395636b9b00f236f9e5645cb2.png)
My favourite part is testing with new images typically
![14f4384d9e00baecb64a62fcdd19cf5e.png](../_resources/14f4384d9e00baecb64a62fcdd19cf5e.png)
![5223127ef41f69e426c382de47ae14e8.png](../_resources/5223127ef41f69e426c382de47ae14e8.png)
![ec631a8b68f210ab7925f7a3540732b1.png](../_resources/ec631a8b68f210ab7925f7a3540732b1.png)
![9fe421c466dda0d2f8771c00ce0d25c7.png](../_resources/9fe421c466dda0d2f8771c00ce0d25c7.png)
The model does have error
***Fun Thing I did was even though there is not class for a human I wanted to know how it will classify my image*** 

🥁🥁🥁 
![9ce12eef8f9304045a65988f72cb4afb.png](../_resources/9ce12eef8f9304045a65988f72cb4afb.png)
TURNS OUT I'M A TRUCK🚚🚚
