## FCN+RL: A Fully Convolutional Network followed by Refinement Layers to Offline Handwritten Signature Segmentation
This model is an approach to locate and extract the pixels of handwritten signatures on identification documents, without any prior information on the location of the signatures.

### Informations and credit
To learn more about this approach, go to the paper for this project [HERE](https://arxiv.org/abs/2005.14229). When using this material, we ask that you quote the authors of this project correctly.

## Dependencies:

- Python 3.6
- numpy 1.17.4
- keras 2.3.1
- tensorflow-gpu 1.14.0 or tensorflow 1.14.0
- opencv-contrib-python 4.1.2.30

### Preliminary settings.
Divide your dataset/images into two directories: `./train` and `./validation`. 

Configure your global settings in the ```utils/global_config.py``` file.

### Training stages

#### *Stage 1*
Train the layers of the encoder-decoder model with the following command at your prompt:
```
python train_encoder_decoder_model.py "-mencoder_decoder_model" "--train-folder=<path_local_diretorio_de_treino>/" "--validation-folder=<path_local_diretorio_de_validacao>/" "--gpu=1" "--bs=12" "--train-steps=10" "--valid-steps=10" "--no-aug" "--train-samples=800" "--valid-samples=200" "--lr=0.0001"
```
After completing the training of the first stage, your model will be saved in the directory you defined, here we define the directory ```./model_path_hdf```. The file saved in this directory will be invoked for the training of the second stage.

#### *Stage 2*
Train the layers of the FCN+RL (RL) model with the following command at your prompt:
```
python train_fcnrl_model.py "-mrefinement_layer_model" "--train-folder=<path_local_diretorio_de_treino>/" "--validation-folder=<path_local_diretorio_de_validacao>/" "--gpu=1" "--bs=12" "--train-steps=10" "--valid-steps=10" "--no-aug" "--train-samples=800" "--valid-samples=200" "--lr=0.0001"
```

#### Comments:
The code is not updated for TensorFlow version 2.x. You can find migration information or code compatibility with Tensorflow 2.x [HERE](https://www.tensorflow.org/guide/migrate).
