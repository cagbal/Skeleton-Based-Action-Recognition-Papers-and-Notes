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
Accuracy on Cross Subject NTU-RGBD: **0.832**
Notes:
- They introduced **Skeleton Transformer** which is a linear layer and creates a linear combination of the existing joints. 
- The idea is that the ordering of the joints may not be optimal, this linear layer may create a better ordering.
- How many joints at the end of the Skeleton Transformer? This information is not clear. 
- From my experience, it is working fine for 2D CNN based methods.
- Two stream. Uses both poisition and velocity of the joints. Fusion by concatenation. 

