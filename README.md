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

