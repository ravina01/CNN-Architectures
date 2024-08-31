# CNN-Architectures
Implementation of different CNN architectures
---

CNN based approach vs classical CV based approach
- input -> Feature vector -> Filter/weights -> Feature maps
- larger the size of filter, smaller will be the feature maps.
- to control the size of feature map you can use -> padding.
- W - F + 2P / S + 1
- in CNN we do, multiple rounds of conv and Pool together.
- from same input, we get multiple feature maps, as the filter used has different values
- basically we use multiple filters, to get multiple feature maps.
- N filters will give - N feature maps -> pooling would downsample the feature maps.
- with each conv layer the depth of feature map will increase.
- depth refers to number of feature maps
- getting 256/ 512 feature map depth size is very common
- 3 FM -> 6 FM -> 3 FM gets multipled by 3 filters combined by element wise addition forms -> 1 FM
- such 6 pairs of 3 filters would give me -> 6 Feature maps
- that is I used 18 different Filters 3 x 6 to get 6 feature maps from 3, while each filter is 3 x 3 that is total number of parameters = 9 x 3 x 6 = 
- similary from 6 Fearure maps to 12 feature maps -> 6 x 12 Filters of size 3 x 3 = total trainable parameters would be = 6 x 12 x 9
- Number of FM will go on increasing and depth will be more.
- after this, complete flattened vector would given to the classifier.
- multiple filters give out texture, edges, reduces noise.
- extracts properties from image, - dots, corners, edges, texture etc.
- 

![image](https://github.com/user-attachments/assets/68619fa8-23c8-4df9-99e3-b114a1b1b2a6)

![image](https://github.com/user-attachments/assets/058fe908-5bcf-41ec-8dfc-75f116e6fc6c)

![image](https://github.com/user-attachments/assets/56dbc924-e9d0-47a9-bb91-c70badd3f58c)

![image](https://github.com/user-attachments/assets/ebcc7ff2-5515-404e-9101-dd530005e45a)

![image](https://github.com/user-attachments/assets/6648c84e-5a51-43ea-96d8-007135436d9e)

![image](https://github.com/user-attachments/assets/350442cc-7522-46ca-b20e-91452739191c)


- Here the confidence score would help us do the - classification.
- confidence score in my prediction

- ![image](https://github.com/user-attachments/assets/8817ba19-bd87-4271-a953-142b09bd674f)

- lets say we have 1000 classes and 10K images like ImageNet.
- to calculate probabilties/ conf score, we need softmax
- softmax the output would be always between 0 and 1
- softmax calculation -> 4 or 0 -> 98 percent prob -> 0.018 for 0 as shown below
- take exponential of both 4 and 0 and divide by sum of both the exponentials
- sum of all outputs would always be 1
- softmax gives probability score of the prediction.
- if values are closer, the conf score is also very close to each other, and we might not be able to predict/ classify properly
- when both inputs are equal the prob/ confidence score are equal
- even if your fully layer values are negative, you will still get the probability values/ conf score.
- even if values are negative your prediction values would be still positive and in between 0 - 1
- sign doesnt matter here, only the relative difference between these 2 matters.
- 

![image](https://github.com/user-attachments/assets/ace32299-4ac2-4936-9005-2fef1fe01843)
![image](https://github.com/user-attachments/assets/bc01621c-6fbb-4d4b-967a-c9fa49312446)

- hence, softmax is used at the end of Fully Connected layer. you will have confidence scores,
- with the help of softmax we can actually do - NMS

- Putting it all together ->

![image](https://github.com/user-attachments/assets/ebcfd55f-ad71-43b7-a9dc-54830ff1089d)

- Final Feature map is of dim = 6 x 3 with 512 depth = 18 x 512  = 9216 flattened output vector = applied FC and Softmax = would give us 1000 prediction probabilities.
- classification can be done using - conv + FC + softmax
- from big image we reduce size - to high dimensional maps -> we get 1000 vector with predictions/ conf score.
- softmax would be applied once at the end of all FC layers
- 
![image](https://github.com/user-attachments/assets/bb80bef6-973d-4498-a8ce-c8b88a572d64)


- 21 = 10 filters would give us = vector of 10 = 10 - with 4 filters would give us = vector of 4 = 4 with 2 filters would give us = vector of 2 = then we can apply softmax on the final level to get the predictions.

- Hence, instead of drastically dropping values from 9216 to 1000 we can add FC layers in beetween -> 
- Dropping directly from 9216 to 1000 dimensions could cause the model to lose a lot of important information too quickly. By adding intermediate FC layers, you allow the model to gradually reduce the dimensionality, which can help it learn more meaningful and abstract features at each stage.
- If you were to go directly from 9216 to 1000, the model might have too much capacity in a single layer, leading to overfitting. Adding intermediate layers with appropriate regularization (like dropout or weight decay) can help distribute the capacity and reduce overfitting.
- Deep networks (those with more layers) can learn more complex functions compared to shallow networks. By adding FC layers, you increase the depth of the network, potentially allowing it to learn more intricate and useful representations of the input data.

  
  
![image](https://github.com/user-attachments/assets/395c08b3-855f-4181-93d5-653b8845f1c2)



