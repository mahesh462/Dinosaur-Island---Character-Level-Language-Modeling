# Dinosaur-Island---Character-Level-Language-Modeling
Build a character level language model to generate new names of dinosaurs. The algorithm will learn the different name patterns, and randomly generate new names. 

## Overview of the model
The model will have the following structure:
- Initialize parameters
- Run the optimization loop.
  - Forward propagation to compute the loss function.
  -  Backward propagation to compute the gradients with respect to the loss function.
  - Clip the gradients to avoid exploding gradients.
  - Using the gradients, update your parameters with the gradient descent update rule.
- Return the learned parameters
<p align = 'center'>
  <img src = '/images/rnn.png'>
</p>

- At each time-step, the RNN tries to predict what is the next character given the previous characters.
- The dataset  X=(x<sup>⟨1⟩</sup>,x<sup>⟨2⟩</sup>,...,x<sup>⟨Tx⟩</sup>)  is a list of characters in the training set.
- Y=(y<sup>⟨1⟩</sup>,y<sup>⟨2⟩</sup>,...,y<sup>⟨Tx⟩</sup>)  is the same list of characters but shifted one character forward.
- At every time-step  t, y<sup>⟨t⟩</sup>=x<sup>⟨t+1⟩</sup> . The prediction at time  t  is the same as the input at time  t+1 .
## Building blocks of the model
Two important blocks are:
1. Gradient clipping: to avoid exploding gradients.
2. Sampling: a technique used to generate characters.

## Clipping the gradients in the optimization loop
In this section we will implement the clip function that you will call inside of your optimization loop.
### Exploding gradients
- When gradients are very large, they're called "exploding gradients."
- Exploding gradients make the training process more difficult, because the updates may be so large that they "overshoot" the optimal values during back propagation.

Before updating the parameters, you will perform gradient clipping to make sure that your gradients are not "exploding."

### Gradient Clipping
- There are different ways to clip gradients.
- We will use a simple element-wise clipping procedure, in which every element of the gradient vector is clipped to lie between some range [-N, N].
- For example, if the N=10
  - The range is [-10, 10]
  - If any component of the gradient vector is greater than 10, it is set to 10.
  - If any component of the gradient vector is less than -10, it is set to -10.
  - If any components are between -10 and 10, they keep their original values.

<p align = 'center'>
  <img src = '/images/clip.png'>
</p>

# Sampling
Once the model is trained, we would like to generate new text (characters). The process of generation is explained in the picture below:

<p align = 'center'>
  <img src = '/images/dinos3.png'>
</p>

Stochastic gradient descent(with clipped gradients) will be used.

We will go through the training examples one at a time, so the optimization algorithm will be stochastic gradient descent.

## Training the model
- Given the dataset of dinosaur names, we use each line of the dataset (one name) as one training example.
- Every 2000 steps of stochastic gradient descent, sample several randomly chosen names to see how the algorithm is doing.

The below pictures shows the output we get after training:
<p align = 'center'>
  <img src = 'Screenshot (133).png'>
</p>


<p align = 'center'>
  <img src = 'Screenshot (134).png'>
</p>


.....

.....

.....


<p align = 'center'>
  <img src = 'Screenshot (135).png'>
</p>



<p align = 'center'>
  <img src = 'Screenshot (136).png'>
</p>

We can see that the algorithm has started to generate plausible dinosaur names towards the end of the training. At first, it was generating random characters, but towards the end we could see dinosaur names with cool endings.
