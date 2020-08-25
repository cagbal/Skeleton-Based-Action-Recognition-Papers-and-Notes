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
| Accuracy: |               0.899              |               0.894              |
|   Link:   | [Link](http://openaccess.thecvf.com/content_CVPR_2019/papers/Shi_Skeleton-Based_Action_Recognition_With_Directed_Graph_Neural_Networks_CVPR_2019_paper.pdf) | [Link](https://arxiv.org/abs/1804.07453) |

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

Code: https://github.com/microsoft/View-Adaptive-Neural-Networks-for-Skeleton-based-Human-Action-Recognition

Accuracy on Cross Subject NTU-RGBD: **0.894**

Notes:
- Impressive accuracy 
- The idea is cool. They transform the skeletons with a small network so that they all will be aligned. This, inevitably, reduces the error caused by view variations. 
- The parameter number is huge, around 10-20 million for state-of-the-art results. There is a good analysis of parameter number vs. accuracy in the paper.
- There are two networks which are RNN and CNN. They fuse the output of them at the end.
 
------------

**8. Actional-Structural Graph Convolutional Networks forSkeleton-based Action Recognition**

Link: https://arxiv.org/pdf/1904.12659.pdf 

Code: https://github.com/limaosen0/AS-GCN

Accuracy on Cross Subject NTU-RGBD: **0.861**

Notes:
- Graph-based algorithm. Their contribution: How to link the nodes. Two ideas: Actional links and structural links 
- Actional Links are links which can link two arbitrary skeleton points. They are produced by a module which is an encoder-decoder network. After the encoder, they get the A-Links, and then these A links are fed into a Decoder network to predict the next possible skeleton pose constrained by the A-Links. 
- Structural Links are links which bond the neighboring nodes. The point here is increasing the receptive field of the graph convolution kernel. So many math tricks there :) 
- GRU is presented in the actional links module so the network MAY be slow.  
- Code is available, which is super cool, but the documentation is poor. Probably, they will "release" it soon. 
- Complicated paper, so not so easy to read. 
- All in all, definitely a good paper; however, I have some questions in mind like ok, the initial links are super important for sure, but a good convolutional network should be able to bond or create spatial relations in the higher layers, even though their initial links are bad. This is like, each pixel of an image is connected to its 8-neighbors; however, the network can give a response to a, let's say, dog consisting of 200 pixels. **If someone understands and explains me in a pull request or issue, I will add it here and delete this comment.** 

------------




**9. Skeleton-Based Action Recognition with Directed Graph Neural Networks**

Link: http://openaccess.thecvf.com/content_CVPR_2019/papers/Shi_Skeleton-Based_Action_Recognition_With_Directed_Graph_Neural_Networks_CVPR_2019_paper.pdf

Code:

Accuracy on Cross Subject NTU-RGBD: **0.899**

Notes:
- Another Graph-based algorithm. It uses a novel Directed Acyclic Graph (DAG) approach. Their reason is that the bone and joints were treated separately and the information extracted was not taking in the dependencies between the two. 
- Their contribution: How to model the dependencies between the bones and the joints. 2-stream fusion of the bone and joint information to perform action recognition. Learn the topology of the graph rather than feed the input skeletal graph.
-DAG approach: Treat bones as edges and joints as vertices. Let the centre of gravity of the skeleton be the root node and for any edge, treat the source vertex to be the one closer to the centre of gravity. 
-Directed Graph Neural Network: It takes in the graph as input and outputs the graph with updated attributes of edge and vertex respectively. The information is extracted from the motion information from the skeleton joints to the bones.
- Adaptive graph that inputs a graph with fixed topology and evolves with time.
- 1D temporal convolutions to extract temporal information.

------------

**10. Make Skeleton-based Action Recognition ModelSmaller, Faster and Better**

Link: https://arxiv.org/abs/1907.09658

Code: https://github.com/fandulu/DD-Net

Accuracy on Cross Subject NTU-RGBD: **Not tested on NTU-RGBD**

Notes:
- It is a really light network. Only 150K-500K params. You don't even need to do knowledge distillation to deploy this algorithm to an edge device.
- They have three streams. One for the distance matrix of the joints. One for the temporal difference with one stride. One for the temporal difference with two strides. I think the idea is amazing. I am also facing this issue every day. Some of the actions are performed slowly, and some of them are really fast. This varying strides would capture both slow and fast motions. My concern here is, though, why 1 and 2 strides. What happens if I add a stream for three strides and one more for four strides. How can I decide? 
- Evaluation part is not so good. NTU-RGBD is like a standard here. However, they test it on different datasets.
- Code is published. So, if anyone can test it on NTU-RGBD and open an Issue or PR, I would appreciate it.

------------

**11. Deep Independently Recurrent Neural Network (IndRNN)**

Link: https://arxiv.org/abs/1910.06251

Code: https://github.com/Sunnydreamrain/IndRNN_pytorch

Accuracy on Cross Subject NTU-RGBD: **0.867**

Notes:
- Independently recurrent neural network (IndRNN), a new type of RNN that can construct deep RNNs and process long sequences.  
- Very simple.  

------------

**12. Two-Stream Adaptive Graph Convolutional Networks for Skeleton-Based Action Recognition**

Link: http://openaccess.thecvf.com/content_CVPR_2019/papers/Shi_Two-Stream_Adaptive_Graph_Convolutional_Networks_for_Skeleton-Based_Action_Recognition_CVPR_2019_paper.pdf

Code: https://github.com/lshiwjx/2s-AGCN

Accuracy on Cross Subject NTU-RGBD: **0.885**

Notes:
- Another Graph-based convolutional network approach. It combines information from two streams: joint and bone stream. It is one of the first approaches to take into account, second-order information like bone-stream that takes into account the direction and angle between the bones to model the action.
- It builds upon ST-GCN model but the topology of the graph is not fixed. It is adaptively changing depending upon the action sample in an end-to-end manner. This helps in increasing the robustness of the model to new actions. 

------------


**Other Github Repos for Skeleton-based Action Recognition Papers**
- https://github.com/XiaoCode-er/Skeleton-Based-Action-Recognition-Papers
- https://github.com/niais/Awesome-Skeleton-based-Action-Recognition

------------

**Websites for Skeleton-based Action Recognition Papers**
- https://paperswithcode.com/task/skeleton-based-action-recognition (Nice benchmarks, link to codes and papers, well organized)
- https://skeleton.iiit.ac.in/dashboard (an interactive dashboard showing detailed performance plots of top-performing models on NTU-120, and including new action datasets(skeletics-152, skeleton-mimetics) and pre-trained models)

------------
#### Acknowledgement 
This work(Github REPO) has received funding from the European Unions Horizon  2020 research and innovation programme under the Marie  Sklodowska-Curie grant agreement No  721619 for the SOCRATES project. 

