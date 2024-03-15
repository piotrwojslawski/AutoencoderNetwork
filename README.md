# AutoencoderNetwork IIITM Face

The IIITM Face Emotion Dataset consists of 1928 images from 107 individuals, with a gender distribution of 87 males and 20 females. These images are categorized into three distinct vertical orientations: front, up, and down. The objective of this project is to employ an autoencoder network for dimensionality reduction.

## Autoencoder Network

I developed an autoencoder for feature extraction and dimensionality reduction of facial expression images. Initially, the picture size was 1000x800x3. After passing through the encoder network, the size was reduced to 125x100x32, resulting in a six-fold reduction in input size. This transformation was essential due to the large size of the images.

### Components:

#### a. Image Generator

To handle large image sizes efficiently, the `image_generator` function generates batches of images and labels for training. Images are loaded and processed in batches, ensuring data variety by shuffling in each epoch. The images are normalized and converted into an array suitable for neural network input, while labels are extracted from file names. This generator facilitates continuous data flow for model training without loading all images into memory simultaneously.

#### b. Encoder and Decoder Architecture

The autoencoder comprises two main components: the encoder and the decoder.

- **Encoder**: Compresses the input image into a lower-dimensional latent space. It consists of three convolutional layers, each followed by batch normalization and max pooling. The number of filters in these layers progressively reduces the data dimensions: 128, 64, and 32, respectively.
  
- **Decoder**: Reconstructs the original image from the encoded representation. It mirrors the encoder with three deconvolutional (Conv2DTranspose) layers and batch normalization. The data is gradually upscaled, increasing the number of filters from 32 back to 128. The final output matches the original input dimensions.

#### c. Model Compilation and Architecture

The model is compiled using the Adam optimizer, with the learning rate adjusted based on the batch size. Mean squared error serves as the loss function, suitable for reconstruction tasks in autoencoders.

#### d. Training the Model

The training process utilizes the image generator to feed data into the model. The number of training steps per epoch is determined by the total number of images and the batch size. Callbacks are employed for model checkpointing (saving the model with the lowest loss), early stopping (to prevent overfitting), and learning rate reduction (based on performance). The model undergoes training for 100 epochs, with the steps per epoch defined by the dataset size and batch size.

#### e. Results

Post-training, it is observed that using only six times less data, images can be effectively reconstructed. The original image is depicted on the right, while the image reconstructed using reduced data is displayed on the left.
![image](https://github.com/piotrwojslawski/AutoencoderNetwork/assets/55345644/7d66aede-d8e9-4704-b388-d42201ec9239)
![image](https://github.com/piotrwojslawski/AutoencoderNetwork/assets/55345644/18c34779-294c-4aa5-b94d-52cd08af50b0)

