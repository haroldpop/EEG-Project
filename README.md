# EEG-Project


## I) Introduction 

The scope of our project is emotion recognition based on EEG signals. Our purpose is to create a reliable deep learning model for this task. To achieve it first we will read the state of the art of this subject to analyze the best method and models existing nowadays. Then, we will implement some selected models to understand them more. Finally, we will see how we can mix the selected model to create our final model for emotion recognition. By mix, I mean that we intend to create a more reliable model based on the characteristics of the different models before. The ideal project deliverable is a model robust against the experiment subject and against the emotion we want to recognize. We are conscious that the project is a little bit too ambitious, but we would like to achieve it. 

To create this deliverable, we will begin by working on the SEED database provided by the Shangai Jiao Tong University. After implementing our first model trained on this dataset, we will work on another dataset such as DREAMER and DEAP. 

## II) State of the art
 
### 1) Human emotions

According to Eckman, there are 6 basic human emotions: * joy, sadness, surprise, fear, anger, and disgust*. Even if we don't know why there are classified as basics, the fact that these 6 emotions are the basic one, seems to be a general truth. One emotion is characterized by three dimensions: dominance, arousal, and valence. Often, the dominance is omitted and so the emotion can also be characterized by two dimensions: arousal and valence. The arousal measures the degree of how exciting or apathetic an emotion is and the valence measures if the emotion is positive or negative (a [diagram](https://www.pinterest.com/pin/354588170647498721/) made by Russel illustrate this). Since the SEED database is a dataset in which we classify human emotion based on three states (happy, neutral, and sad) we will not go further. 

### 2) EEG features

SEED is a database in which EEG signals whee retrieved during 3 weeks experiment sessions. In each session, the subject of the experience watched 15 sequences extracted from 6 Chinese movies. Each videos sequence is labeled as 0:sad, 1:neutral, and 2:happy. 
A typical EEG emotion recognition method usually consists of two major parts: a discriminative part to extract EEG features and an emotion classification part. Before making these two parts, a signal preprocessing part has to be made. Since the SEED database is directly provided with preprocessed EEG and extracted feature EEG, we can focus ourself the emotion classification part. Extracted features of EEG signals of SEED database were extracted from the "five" brains frequency, $\delta$, $\theta$, $\alpha$, $\beta$, $\gamma$. Moreover, the extracted feature got in the SEED database are the following: the differential entropy, the power spectral density, the differential asymmetry, the rational asymmetry, and the differential caudality. These features were calculated with two methods the LDS (Linear Dynamic System) and the Moving average. 

### 3) Emotion classification algorithm

Generally, for emotion classification, even if classical machine learning classification algorithms got good results,  deep neural networks achieved better performance. Besides, deep neural networks seem more robust to experiment and patient variation. For this reason, we are giving more interest to deep neural network models. Among all deep neural networks, three successfully achieved almost equal accuracy performance (close to 90%) for a small standard deviation. These three architectures are Dynamical Graph Convolutional Neural Network (DGCNN), a neural network based on cerebral hemispheric asymmetry which used BiDANN framework, and an improved LSTM network called ATDD-LSTM for Attention-based LSTM with Domain Discriminator. 
The neural network based on the BiDANN framework uses the preprocessed EEG signals to extract features that are optimized to minimize the loss of domain discriminators but maximize the loss of domain discriminators. This technique will lead to adversarial learning between classifier and domain discriminators to encourage emotion-related but domain invariant data representation. 
The Dynamical Graph Convolutional Neural Network is an extension of the traditional CNN by combining CNN with spectral theory. Since information is circulating through the brain a classic CNN cannot be trained to classify emotion, indeed such networks learn from local features. That's why a graph approach was proposed. The term dynamical in DGCNN means that the graph will learn from the intrinsic data of the graph. The DGCNN can provide an effective way to describe the relationship between different nodes of the graph, which could provide a way to explore the relationship between the EEG channels. 
Nevertheless, the DGCNN can only learn the linear relationship between channels which characterizes the strength of connections between two channels. 
The ATDD-LSTM neural network is a neural network model which contrary to DGCNN can characterize non-linear relations among two channels of an EEG. This model is like an improved version of LSTM (Long Short Term Memory) for emotion recognition. Even if the three cited models are independent of each other, we can see that from the ATDD-LSTM and DGCNN we can learn useful information about the relationship between different channels of the EEG. These two models are trained with the extracted features given with the dataset, these features are general features of EEG signals. But, we can imagine that if we learn these two algorithms with better features like probably with the one given by the neural network based on the BiDANN framework we could achieve better performance and a better understanding of the data. 

### III) Notebook Guide

All scripts can be found in the script folder in the specified model implemented. Below is the instructions of each member on which notebook you should pay attention.

#### a) Attention-based LSTM

#### b) BiDANN-Framework

#### c) DGCNN

In the notebook GraphConvNetworkChebyshevParameters, you can find how I create the GCNN model and how I varied different parameters to understand the impact of them and find the best one. 
In the notebook SynthesisScript, you can find the definition of every model I implemented and how I looped across all the datasets to create a table of results. (Unfortunately, when I ran this notebook on my computer Python crashed. To be able, to create the table of results I ran 4 different notebooks for each model and I hoped that Python will not crashed, python crashed for one with the use of the norm mod Laplacian. This 4 notebooks are the other one in the folder.)


