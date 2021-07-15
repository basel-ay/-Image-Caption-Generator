# **Table of Contents**
1.Introduction

2.Approach to the problem statement

3.Data loading and Preprocessing

4.Glove Embedding

5.Model building

6.Model training

7.Greedy and Beam Search

8.Evaluation


# **Introduction**

Image caption Generator is a popular research area of Artificial Intelligence that deals with image understanding and a language description for that image. Generating well-formed sentences requires both syntactic and semantic understanding of the language. Being able to describe the content of an image using accurately formed sentences is a very challenging task, but it could also have a great impact, by helping visually impaired people better understand the content of images. 

This task is significantly harder in comparison to the image classification or object recognition tasks that have been well researched. 

The biggest challenge is most definitely being able to create a description that must capture not only the objects contained in an image, but also express how these objects relate to each other.

# **Approach to the problem statement**
We will tackle this problem using an Encoder-Decoder model. Here our encoder model will combine both the encoded form of the image and the encoded form of the text caption and feed to the decoder.

Our model will treat CNN as the ‘image model’ and the RNN/LSTM as the ‘language model’ to encode the text sequences of varying length. The vectors resulting from both the encodings are then merged and processed by a Dense layer to make a final prediction.

We will create a merge architecture in order to keep the image out of the RNN/LSTM and thus be able to train the part of the neural network that handles images and the part that handles language separately, using images and sentences from separate training sets. 

In our merge model, a different representation of the image can be combined with the final RNN state before each prediction.

![](https://cdn.analyticsvidhya.com/wp-content/uploads/2020/10/Screenshot-2020-10-20-at-7.36.38-PM-768x289.png)

The above diagram is a visual representation of our approach.

The merging of image features with text encodings to a later stage in the architecture is advantageous and can generate better quality captions with smaller layers than the traditional inject architecture (CNN as encoder and RNN as a decoder).

To encode our image features we will make use of transfer learning. There are a lot of models that we can use like VGG-16, InceptionV3, ResNet, etc.
We will make use of the inceptionV3 model which has the least number of training parameters in comparison to the others and also outperforms them.

To encode our text sequence we will map every word to a 200-dimensional vector. For this will use a pre-trained Glove model. This mapping will be done in a separate layer after the input layer called the embedding layer.

To generate the caption we will be using two popular methods which are Greedy Search and Beam Search. These methods will help us in picking the best words to accurately define the image.

I hope this gives you an idea of how we are approaching this problem statement.


**Let’s dive into the implementation and creation of an image caption generator!**

**Datasets and Notebook on Kaggle** : https://www.kaggle.com/basel99/image-caption-generator
