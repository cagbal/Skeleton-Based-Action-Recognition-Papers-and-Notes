# Skeleton-based Action Recognition Papers and Small Notes About Them
I am keeping these notes for my research at Fraunhofer IPA. For each paper, I am planning to give link, accuracy on ntu rgbd dataset and some small notes. 

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
| Accuracy: |               0.891              |               0.865              |
|   Link:   | https://arxiv.org/abs/1811.04237 | https://arxiv.org/abs/1804.06055 |

### Papers:
**1. SKELETON-BASED ACTION RECOGNITION WITH CONVOLUTIONAL NEURAL
NETWORKS**

Link: https://arxiv.org/abs/1704.07595

Code:

Accuracy on Cross Subject NTU-RGBD: **0.832**

Notes:
- They introduced **Skeleton Transformer** which is a linear layer and creates a linear combination of the existing joints. 
- The idea is that the ordering of the joints may not be optimal, this linear layer may create a better ordering.
- How many joints at the end of the Skeleton Transformer? This information is not clear. 
- From my experience, it is working fine for 2D CNN based methods.
- Two stream. Uses both poisition and velocity of the joints. Fusion by concatenation. 


------------



**2. Co-occurrence Feature Learning from Skeleton Data for Action Recognition and
Detection with Hierarchical Aggregation**

Link: https://arxiv.org/abs/1804.06055

Code: https://github.com/huguyuehuhu/HCN-pytorch (Re-implementation PyTorch Accuracy is %1.5 lower than original)

Accuracy on Cross Subject NTU-RGBD: **0.865**

Notes:
- My understanding is that they use joints as channels and this helps using the information from different joints at the same time.
- At some point, they change the joint dimensions and the spatial dimension(x,y,z). Then, convolve it again. So, each joint becomes a channel. To better understand the concept: "If each joint of a skeleton is treated as  a  channel,  then  the  convolution  layer  can  learn  the  co-occurrences from all joints easily" says author in the introduction.
- Impressive accuracy. 
- Two stream network. Fusion by concatenation. 
- They apply the CNN to each person then fuse the information by using max. operation. 
- Extremely low number of parameters. It has around **800K parameters**. 
- They use 2d dropout with 0.5 probability. 


------------



**3. Skeleton-Based Action Recognition with Synchronous Local and Non-local Spatio-temporal Learning and Frequency Attention**

Link: https://arxiv.org/abs/1811.04237

Code: 

Accuracy on Cross Subject NTU-RGBD: **0.891**

Notes:
- So many ideas in the paper. Non-local, local data exlotation, reformed softmax and frequency domain analysis. 
- I want to focus on the frequency domain analysis on this paper. The idea is using frequency domain along with time domain. 
- The "necessary" frequency components are selected or attended by using a FC based network. This information is later added to the time information by using IFFT.  
- Amazing accuracy. Outperformed everything with large margin. 
- For such a big margin, I would expect a code. 


------------

**4. Interpretable 3D Human Action Analysis with Temporal Convolutional
Networks**

Link: https://arxiv.org/abs/1704.04516

Code: https://github.com/TaeSoo-Kim/TCNActionRecognition

Accuracy on Cross Subject NTU-RGBD: **0.743**

Notes:
- Low accuracy. Old paper.(2017)
- Single stream network using Joint Positions
- Resnet based 
- 1D Convolution through temporal domain. All spatial domain is considered at once meaning that the spatial size of kernel is the same as spatial dimension of the input (number of joints x 3 (xyz))
- The contribution is in interpretable action recognition. They show which motion effects a particular action.  

------------

**5. Ensemble One-Dimensional Convolution Neural Networks for Skeleton-Based Action Recognition**

Link: https://arxiv.org/abs/1801.02475 (but no pdf!)

Code: https://github.com/Qingyang-Xu/Ensem-NN

Accuracy on Cross Subject NTU-RGBD: **0.851**

Notes:
- Using ensembles of 4 different subnets - body part net, base net, attention net etc. 
- Introducing a channel wised attention net which is a FC+Activation+FC+Softmax
- Two stream 1D CNN. The idea is coming from Interpretable 3D Human Action Analysis with Temporal Convolutional Networks
- All the subnets are trained independently. I think this is a drawback.  
- Why would they extract the features of each body part? I don't understand. There are 5 different base-nets. The number of parameter should be enourmous.
- In general, this paper is a nice reference to ensemble applied to skeleton-based action recoginition.
- High accuracy. 

------------

**Other GITHUB Repos for Skeleton-based Action Recognition Papers**
- https://github.com/XiaoCode-er/Skeleton-Based-Action-Recognition-Papers

------------

#### Acknowledgement 
This work(Github REPO) has received funding from the European Unions Horizon  2020  research  and  innovation  programme  under  the Marie  Skodowska-Curie  grant  agreement  No  721619  for  the SOCRATES project. 

