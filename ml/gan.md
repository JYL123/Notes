[Generative Adversial Network (GAN)](https://arxiv.org/pdf/1406.2661.pdf) is a generative model using adversial approach. This model can be used to replicate content, such as cat/dog images. The adversial approach is inspired by the game theory, where two models, a generator and a critic, are competing with each other while making each other stronger at the same time.

The two models in `GAN` are generator and discriminator. The overview of the `GAN` is as below:
![overview](https://github.com/JYL123/Notes/blob/master/gan_overview.png)

Both the generator and the discriminator are neural networks. The generator output is connected directly to the discriminator input. Through backpropagation, the discriminator's classification provides a signal that the generator uses to update its weights.

### The Discriminator

The discriminator in a GAN is simply a classifier. It tries to distinguish real data from the data created by the generator. It could use any network architecture appropriate to the type of data it's classifying.

During discriminator training:
1. The discriminator classifies both real data and fake data from the generator.
2. The discriminator loss penalizes the discriminator for misclassifying a real instance as fake or a fake instance as real.
3. The discriminator updates its weights through backpropagation from the discriminator loss through the discriminator network.

### The Generator

The generator part of a GAN learns to create fake data by incorporating feedback from the discriminator. It learns to make the discriminator classify its output as real.

We train the generator with the following procedure:
1. Sample random noise.
2. Produce generator output from sampled random noise.
3. Get discriminator "Real" or "Fake" classification for generator output.
4. Calculate loss from discriminator classification.
5. Backpropagate through both the discriminator and generator to obtain gradients.
6. Use gradients to change only the generator weights.

### Two Complications

Because a GAN contains two separately trained networks, its training algorithm must address two complications:

* GANs must juggle two different kinds of training (generator and discriminator).
  
  GAN training proceeds in alternating periods:
  1. The discriminator trains for one or more epochs.
  2. The generator trains for one or more epochs.
  3. Repeat steps 1 and 2 to continue to train the generator and discriminator networks.
  
 We keep the generator constant during the discriminator training phase. Similarly, we keep the discriminator constant during the generator training phase. 
 
* GAN convergence is hard to identify.
  
  As the generator improves with training, the discriminator performance gets worse because the discriminator can't easily tell the difference between real and       fake. If the generator succeeds perfectly, then the discriminator has a 50% accuracy. In effect, the discriminator flips a coin to make its prediction.

  This progression poses a problem for convergence of the GAN as a whole: the discriminator feedback gets less meaningful over time. If the GAN continues training     past the point when the discriminator is giving completely random feedback, then the generator starts to train on junk feedback, and its own quality may collapse.

Reference:
* https://developers.google.com/machine-learning/gan/discriminator
* https://lilianweng.github.io/lil-log/2017/08/20/from-GAN-to-WGAN.html
* https://www.kaggle.com/jesucristo/gan-introduction?scriptVersionId=16563028



