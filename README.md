# Image Captioning 

**Image Captioning** 

In this project, we designed a system for captioning images with the help of recurrent and convolutional networks.

## **Data Collection**

 In this project, we are going to use flickr8k data, which you can download from [here](https://www.kaggle.com/adityajn105/flickr8k), or directly use the Kegel notebook so that we can put captions on the images. 

This dataset contains 8000 images, each of which has five captions. After receiving the file, we tried to get a general intuition from the data and then stored our data in the dictionary based on the image ID and caption.

## **Caption Data Cleaning**

To work with text data, we must first pre-process the data. This pre-processing can have specific types depending on the application. Here are just some simple pre-processing done.

* We changed all the words in the captions to lowercase form.

* We removed punctuations and words that contain numbers and tried to avoid monosyllabic words. (This can be done using the string library.)

* It is better to save these captions in a file on the hard disk and load this file whenever necessary so that it does not occupy the system's cache memory.

The figures below show two of the images, along with five captions.

![](https://github.com/Fateme-Azizabadi/Image-Captioning/blob/main/Images/Example1.png)

![](https://github.com/Fateme-Azizabadi/Image-Captioning/blob/main/Images/Example2.png)


## **Creating a Dictionary of Unique Words**

* Having a dictionary when it comes to working with text is necessary. The dictionary consists of a collection of unique words in captions.

* We tried to extract all the unique words in the captions in this section. Next, we discarded the words extracted less than ten times in the captions.

* The original vocabulary size is 6751. We form a dictionary of unique words. Then we identify the words repeated less than ten times and delete them. The size of the dictionary is reduced to 1350.

## **Building Training Data**

* We read train images and their id from the file 'Flickr_8k.trainImages.txt'. Then we save all train and test images in the train-img and test-img list.

* Next, we add two tokens, 'startseq' and 'endseq', to specify the beginning and the end.

## **Display of Images**

* In this section, we need to display images. So we try to work from a pre-learned network to do transfer learning. This can be done with any network trained with the imagenet dataset. 

* In this part, we use the Inceotionv3 model as a pre-trained network. To use this model, we need a pre-processing of the data to convert it to the appropriate network size, i.e., 299x299.

* Note that here our goal is not classification, and only a fixed vector length is considered. So, with the help of the encode function (which we implemented ourselves), we convert the training images into a d-dimensional representation.

* Similarly, we can also transfer the test images to the d dimension and then save them on the disk.

## **Creating Two Dictionaries**

We consider that we want to predict the captions word by word. Therefore, similarly, we also need to convert the words into a fixed vector representation. So we need two dictionaries (word2idx and idx2word dictionary). With this, we want to show the words in the dictionary with an integer number. Note that there are pre-made tokenizers available for different languages.

## **Data Generator**

In this section, we are trying to prepare our data using the data generator. Keep in mind that we are sending the data to the network as a mini-batch, so we increase all the captions to the largest desired length using the <pod> token.

We define a Data Generator. In this function, we first increase the captions to the largest length, i.e., 38, then we divide the data into two categories, x and y.

* Y: This category contains the output that is the target of LSTM and is the next word.
* X1: Includes images
* X2: All the words that come before the target function.

## **Mapping Words to Vector Space**

Now we want to display all the words in vector mode. We try to use a ready-made vector representation for vectors. We used GLOVE's pre-learned representation(Other representations can be used).

We implement embedding_matrix for all unique words. Keep in mind that freeze the embedding layer after using the pre-learned representation.

## **The network architecture**

The network architecture is shown in the figure below. 

![](https://github.com/Fateme-Azizabadi/Image-Captioning/blob/main/Images/Network.png)

## **Model training result**

![](https://github.com/Fateme-Azizabadi/Image-Captioning/blob/main/Images/Result.png)


## **Applying the model to the test images**


![](https://github.com/Fateme-Azizabadi/Image-Captioning/blob/main/Images/output1.png)

![](https://github.com/Fateme-Azizabadi/Image-Captioning/blob/main/Images/output2.png)




 
 
