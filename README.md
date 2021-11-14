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

### III) Project management

Because we are a team of three members, we found that making one member responsible for one model can be a good idea. Like this, we can avoid some code understanding problems. Moreover, because we will be responsible for one architecture and we will have to explain it to the team in the future, a such split will give us a deeper understanding of what we did during this project. Although we are each responsible for one part of the project, that doesn't mean that we don't help each other and that we will just make our piece of code and give it to others.

For the next weeks, Pyae will be responsible for the ADD-LSTM architecture, Anupam to BiDANN framework-based model, and Harold to the DGCNN model. This is our understanding of the project for the moment and the way we will process it. 

You can find the code advancement of each member in the folder Code, and the associated folder. And you can find the documentation in the folder Documentation. 

### IV) Week4

To be clearer in our advancement, we decided to split the update part between each member

#### a) Pyae
On data preprocesssing and working on github lstm code.
also reviewing paper A LSTM based deep learning network for recognizing emotions using wireless brainwave driven system

#### b) Anupam
I am still working on data preprocesing . I have already divided my datasets for left,right for one sample and with all electrodes which is needed for different cases. i  divided my data to 9s windows or 9 step for the data processing. Now i need to work for whole datasets. For the model, i prepared the lstm feature extractor and classifier model. I also reviewing the paper " Domain-Adversarial Training of Neural Networks" paper which is in the later part after lstm. I started to build a model for GRL but not completed.
I planned to complete the data processing part and lstm with GRL and Discriminator in the next week and test my model.

#### c) Harold

This week I implemented my first DGCNN model. I will explain in more detail what steps I followed during the interview on the 15th of November, and according to what will be said during this interview I will update the GitHub properly. However, the results got are not good, and I am trying to fix all errors I possibly made during the implementation. 

Indeed, in the beginning, I obtained a constant loss and a constant accuracy for both training and test set during the training when I used even numbers of Chebyshev coefficients. When I used odd numbers of Chebyshev coefficients, I obtained an unstable loss for both training and test set and also a non-sense accuracy. It appeared that this instability came from the fact that I didn't normalize the extracted EEG signals. The origin of the constant loss was due to the fact the Chebyshev approximation obtained was a matrix with only negative coefficients, so when this matrix was evaluated by the ReLU function we got a null matrix and so a null gradient, and this for all signals. The origin of the instability was due to the non-normalization of the data. By normalizing the data, the Chebyshev approximation on the signal is no longer composed only of negative coefficients, and the Chebyshev approximation is far more stable. The other problem faced was the only use of the ReLU function as activate functions in the model. Especially, with le linear layer, I noticed that the same phenomenon of ReLU output with only zeros coefficients occurred between the two linear layers. To counter this problem I chose to use tanh function as activating function for the moment. Also, this week I also saw that there was a pytorch dedicated library called [pytorch-geometric](https://pytorch-geometric.readthedocs.io/en/latest/). In this library all the graph functions I use are already implemented. Nevertheless, since I got difficulties to import it and I already implemented almost every useful functions, I didn't spend more time to try import it. Nevertheless, once the implementation ready, I am planning to compare my results with the one from this library. To finish, there is one big issue I faced and I don't really fixed or have a clear answer, I hope you can help me. When I run my code, sometimes Python crashe. There is no error message, just the windows pop up with the message Python stops working please wait until we find a solution and after that the only solution is stop the program. So, I have to restart the kernel and I get the same message error. My search on the web may suppose that my pytorch program use the total amount of RAM available on my computer when I run the code. Or, the CPU of my computer cannot handle the calculation. I think that the second hypothesis is not the good one. Indeed, when I run other
deep learning python script like a CNN script even if my CPU use is 100%, I don't have this problem. So, I think it is a RAM problem, 
but do you know how can I fix it? Is there any tricks to do it? 

Now I'm still having a non understandable training of the model. Even if it's non understandable yet, it makes more sense (at least for myself). For the upcoming week, I am will work on understand what's wrong and try to fix it. 

*I update the code on the repository*
