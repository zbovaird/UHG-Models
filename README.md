
Designing/Testing deep learning models using Hyperbolic Graph Neural Network (HGNN). The GNN is chosen to model the architecture of the network, and is then trained in hyperbolic space to caputure the network heirarchy. 
The specific GNN used in GraphSage, as it allows the user to control the size of the neighborhood when it comes to message passing and aggregation of the feature vectors. 

All data was contextualized, normalized, formatted, and cleaned prior to importing into the models

The two models are:
Intrusion Detection
  - supervised learning with labeled data in a 70/15/15 split
  - Final testing accuracy was 98.64%

Anomoaly Detection in Network Traffic
  -uses modbus traffic, but works for any traffic type
  -unsupervised learning
  -traffic from attacking ip was lowered to 5% of the total traffic to better simulate normal environement under attack, but allow the model to still be trainable without too much fine-tuning
  -all IPs were obscured prior to training and assigned a unqiue 1 or 2 digit value to lower memory costs
  -model determined that IP 7 was the attacking IP, which correlated to the attacking IP from the documentation of the dataset


HGNN Approach
-The future of deep learning models will most likely gravitate to HGNN, but there will be 2 immediate issues that arise due to using the classicail approach of Hyperbolic Geometry (HG), which uses transcendantal functions (arccosh, arcsinh, etc). The two issues it creates are radically increased computation costs and distortion. In the classical approach to HG, it is difficult to train the model in hyperbolic space even with the data being formatted into tensors. The trick used is to project the data from hyperbolic space into the Euclidean tangent space using logmap function, let the model training do its linear operations, and then project back down hyperbolic space using expmap function. While the data is not distorted as tensors are invariant under coordinate-system transformations, the space is distorted as logmap and expmap are both non-linear functions. This leads to increased computation costs with the movement between the spaces, and the distortions in the generated embeddings. 

-Both models in this repo use a different approach to HG called Universal Hyperbolic Geometry (UGH) developed by Norman Wilderberger at the University of New South Wales. Its an algebraic approach using projective geometry. This allows not only the tensor data to maintain its invariance under coordinate-systems transformations, but the space to reatin its invariance as well. This causes a severe reduction in computation costs and eliminates the distortions. As there is no current PyTorch library for UHG, all the equations have been hardcoded in. 

  

# UHG
comparing Universal Hyperbolic Geometry models with both CPU and GPU

The file CIC-IDS-2017 is the cat of all files from the Canadian Institute for Cybersecurity Intrusion Detection (2017) Dataset; available on Kaggle

more UHG principles iff it benefits the model
