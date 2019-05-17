# Skeleton-based Action Recognition Papers and Small Notes About Them
I am keeping these notes for my research at Fraunhofer IPA. For each paper, I am planning to give a link, accuracy on the NTU-RGBD dataset and some small notes. 

## Contribution 
Feel free to contribute. No general rule. Just keep the format for each paper as below. 

##### Template:
    **Name of the paper**
    Link: 
    Code:
    Accuracy on Cross Subject NTU-RGBD: **XX%**
    Notes:
    - Bullet point 1
    - Bullet point 2

#### Current Top 2 for NTU-RGBD Cross Subject Split: (Only using Skeleton data, not RGBD)
|           |               Top 1              |               Top 2              |
|:---------:|:--------------------------------:|:--------------------------------:|
| Accuracy: |               0.894              |               0.891              |
|   Link:   | https://arxiv.org/abs/1804.07453 | https://arxiv.org/abs/1811.04237 |

### Papers:
**1. SKELETON-BASED ACTION RECOGNITION WITH CONVOLUTIONAL NEURAL
NETWORKS**

Link: https://arxiv.org/abs/1704.07595

Code:

Accuracy on Cross Subject NTU-RGBD: **0.832**

Notes:
- They introduced **Skeleton Transformer** which is a linear layer and creates a linear combination of the existing joints. 
- The idea is that the ordering of the joints may not be optimal; this linear layer may create a better ordering.
- How many joints at the end of the Skeleton Transformer? This information is not clear. 
- From my experience, it is working fine for 2D CNN based methods.
- Two streams. Uses both position and velocity of the joints. Fusion by concatenation. 


------------



**2. Co-occurrence Feature Learning from Skeleton Data for Action Recognition and
Detection with Hierarchical Aggregation**

Link: https://arxiv.org/abs/1804.06055

Code: https://github.com/huguyuehuhu/HCN-pytorch (Re-implementation PyTorch Accuracy is %1.5 lower than original)

Accuracy on Cross Subject NTU-RGBD: **0.865**

Notes:
- My understanding is that they use joints as channels and this helps using the information from different joints at the same time.
- At some point, they change the joint dimensions and the spatial dimension(x,y,z). Then, convolve it again. So, each joint becomes a channel. To better understand the concept: "If each joint of a skeleton is treated as a channel, then the convolution layer can learn the co-occurrences from all joints easily" says author in the introduction.
- Impressive accuracy. 
- Two stream network. Fusion by concatenation. 
- They apply the CNN to each person then fuse the information by using max. operation. 
- Extremely low number of parameters. It has around **800K parameters**. 
- They use dropout with 0.5 probability. 


------------



**3. Skeleton-Based Action Recognition with Synchronous Local and Non-local Spatio-temporal Learning and Frequency Attention**

Link: https://arxiv.org/abs/1811.04237

Code: 

Accuracy on Cross Subject NTU-RGBD: **0.891**

Notes:
- So many ideas in the paper. Non-local, local data exploitation, reformed softmax and frequency domain analysis. 
- I want to focus on the frequency domain analysis in this paper. The idea is using frequency domain along with time domain. 
- The "necessary" frequency components are selected or attended by using an FC based network. This information is later added to the time information by using IFFT.  
- Amazing accuracy. Outperformed everything with a large margin. 
- For such a significant margin, I would expect a code. 


------------

**4. Interpretable 3D Human Action Analysis with Temporal Convolutional
Networks**

Link: https://arxiv.org/abs/1704.04516

Code: https://github.com/TaeSoo-Kim/TCNActionRecognition

Accuracy on Cross Subject NTU-RGBD: **0.743**

Notes:
- Low accuracy. Old paper. (2017)
- Single stream network using Joint Positions
- Resnet based 
- 1D Convolution through the temporal domain. All spatial domain is considered at once meaning that the spatial size of the kernel is the same as the spatial dimension of the input (number of joints x 3 (XYZ))
- The contribution is in interpretable action recognition. They show which motion effects a particular action.  

------------

**5. Ensemble One-Dimensional Convolution Neural Networks for Skeleton-Based Action Recognition**

Link: https://arxiv.org/abs/1801.02475 (but no pdf!)

Code: https://github.com/Qingyang-Xu/Ensem-NN

Accuracy on Cross Subject NTU-RGBD: **0.851**

Notes:
- Using ensembles of 4 different subnets - body part net, base net, attention net, etc. 
- Introducing a channel wised attention net which is an FC+Activation+FC+Softmax
- Two stream 1D CNN. The idea is coming from Interpretable 3D Human Action Analysis with Temporal Convolutional Networks
- All the subnets are trained independently. I think this is a drawback.  
- Why would they extract the features of each body part? I don't understand. There are 5 different base-nets. The number of the parameter should be enormous.
- In general, this paper is a nice reference to ensemble applied to skeleton-based action recognition.
- High accuracy. 

------------

**6. Hard Sample Mining and Learning for Skeleton-Based Human Action Recognition and Identification**

Link: https://ieeexplore.ieee.org/abstract/document/8588326

Code: 

Accuracy on Cross Subject NTU-RGBD: **0.866**

Notes:
- Using Global and Local features. Global features are the classical spatio-temporal matrix. However, local features are highly hand engineered relative Hand positions. 
- A good example of hand engineered features; however, I think it violates the end-to-end learning because we explicitly state that Hand features are essential.(Just my opinion, no offense!)
- High accuracy. 
- Two-stage network: Temporal and Spatial processing. Temporal domain network is heavily using LSTM which is not suitable for computation time. 
- They introduce hard sample mining by selecting low-performance actions. Complicated training procedure to avoid overfitting.
- Human identification part is irrelevant to me.  

------------

**7. View Adaptive Neural Networks for High-Performance Skeleton-based Human Action Recognition**

Link: https://arxiv.org/abs/1804.07453

Code: 

Accuracy on Cross Subject NTU-RGBD: **0.894**

Notes:
- Impressive accuracy 
- No code
- The idea is cool. They transform the skeletons with a small network so that they all will be aligned. This, inevitably, reduces the error caused by view variations. 
- The parameter number is huge, around 10-20 million for state-of-the-art results. There is a good analysis of parameter number vs. accuracy in the paper.
- There are two networks which are RNN and CNN. They fuse the output of them at the end.
 
------------

**8. Actional-Structural Graph Convolutional Networks forSkeleton-based Action Recognition**

Link: https://arxiv.org/pdf/1904.12659.pdf 

Code: https://github.com/limaosen0/AS-GCN

Accuracy on Cross Subject NTU-RGBD: **86.1%**

Notes:
- Graph-based algorithm. Their contribution: How to link the nodes. Two ideas: Actional links and structural links 
- Actional Links are links which can link two arbitrary skeleton points. They are produced by a module which is an encoder-decoder network. After the encoder, they get the A-Links, and then these A links are fed into a Decoder network to predict the next possible skeleton pose constrained by the A-Links. 
- Structural Links are links which bond the neighboring nodes. The point here is increasing the receptive field of the graph convolution kernel. So many math tricks there :) 
- GRU is presented in the actional links module so the network MAY be slow.  
- Code is available, which is super cool, but the documentation is poor. Probably, they will "release" it soon. 
- Complicated paper, so not so easy to read. 
- All in all, definitely a good paper; however, I have some questions in mind like ok, the initial links are super important for sure, but a good convolutional network should be able to bond or create spatial relations in the higher layers, even though their initial links are bad. This is like, each pixel of an image is connected to its 8-neighbors; however, the network can give a response to a, let's say, dog consisting of 200 pixels. **If someone understands and explains me in a pull request or issue, I will add it here and delete this comment.** 

------------

**Other GITHUB Repos for Skeleton-based Action Recognition Papers**
- https://github.com/XiaoCode-er/Skeleton-Based-Action-Recognition-Papers

------------

#### Acknowledgement 
This work(Github REPO) has received funding from the European Unions Horizon  2020 research and innovation programme under the Marie  Sklodowska-Curie grant agreement No  721619 for the SOCRATES project. 

