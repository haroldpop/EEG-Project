# EEG-Project


## I) Introduction 

The scope of our project is emotion recognition based on EEG signals. Our purpose is to create a reliable deep learning model for this task. To achieve it first we will read the state of the art of this subject to analyze the best method and models existing nowadays. Then, we will implement some selected models to understand them more. Finally, we will see how we can mix the selected model to create our final model for emotion recognition. By mix, I mean that we intend to create a more reliable model based on the characteristics of the different models before. The ideal project deliverable is a model robust against the experiment subject and against the emotion we want to recognize. We are conscious that the project is a little bit too ambitious, but we would like to achieve it. 

To create this deliverable, we will begin by working on the SEED database provided by the Shangai Jiao Tong University. After implementing our first model trained on this dataset, we will work on another dataset such as DREAMER and DEAP. 


## II) State of the art

### 1) Human emotions

According to Eckman, there is 6 basic human emotions: *the joy, sadness, surprise, fear, anger and disgust*. Even if we don't know why there are classified as basics, the fact that this 6 emotions are the basic one, seems to be a general truth. One emotion is characterized by three dimensions: the dominance, the arousal and the valence. Often, the dominance is omitted and so the eomtion can also be characterized by two dimensions: the arousal and the valence. The arousal measures the degree of how exciting or apathetic an emotion is and the valence measures if the emotion is positive or negative (a [diagram](https://www.pinterest.com/pin/354588170647498721/) made by Russel illustrate this). Since the SEED database is a dataset in which we classify the human emotion based on three states (happy, neutral and sad) we will not go further. 

### 2) EEG features

SEED is a database in which EEG signals whee retrieved during 3 weeks experiment sessions. In each session, the subject of the experience watched 15 sequences extracted from 6 chinese movies. Each videos sequence is labelled as 0:sad, 1:neutral and 2:happy. 
A typical EEG emotion recognition method usually consists of two major parts: a discriminative part to extract EEG feature and an emotion classification part. Before making these two parts, a signal preprocessing part has to be made. Since, SEED databse is directly provided with preprocessed EEG and extracted feature EEG, we can focus ourself the emotion classification part. Extracted features of EEG signals of SEED database were extracted from the "five" brains frequency, $\delta$, $\theta$, $\alpha$, $\beta$, $\gamma$. Morevover, the exctracted feature got in SEED database are the following: the differential entropy, the power spectral density, the differential assymetry, the rational assymetry, and the differential caudality. These features was calculated with two methods the LDS (Linear Dynamic System) and the Moving average. 

### 3) Emotion classification algorithm

Generally, for emotion classification, even if classical machine learning classification algorithm got good results, deep neural network achieved better performance. Besides, deep neural network seems more robust to experiment and patient variation. For this reasons, we are giving more interests to deep neural network models. Among all deep neural networks, three successfully achieved almost equal accuracy performance (close to 90%) for a small standard deviation. These three architectures are Dynamical Graph Convolutional Neural Network (DGCNN), a neural network based on cerebral hemispheric asymmetry which used BiDANN framework and an improved LSTM network called ATDD-LSTM for Attention-based LSTM with Domain Discriminator. The neural network based on BiDANN framework use the preprocessed EEG signals to extract features which are optimized to minimize the loss of domain discriminators but maximize the loss of domain discriminators. This technique will lead to an adversial learning between classifier and domain discriminators to encourage emotion related but domain invariant data representation. The Dynamical Graph Convolutional Neural Network, is an extension of the traditional CNN by combining CNN with spectral theory. For emotion recognition, since the information is circulating through the brain 
