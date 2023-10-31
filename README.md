## DEEPFAKE
DEEPFAKE project funded by Meta Research

# Introduction
This project has been created for research purposes only. Anyone intending to replicate the scientific discoveries are expected to also follow the ethical guidelines stated in the github repositories that we use a submodules. 

The aim of this project is to demonstrate how to generate realistic videos of specified people (deepfakes) and research the credibility of the deepfakes. The owners of the data that we applied our methods to gave consent to do so. However, we will refrain from allowing public access to the data. Anyone interested in seeing the actual data can contact us. Otherwise, one can still use our method on their own data.

# Requirements for deepfake

Using our method, one has to have access to the following ressources:

An image of a person to imitate (source), and a video of a person to drive the motion and speech of the source (driver) are required. Both are required to have a resolution of 256x256 and the face needs to occupy most of the frame. This data is used to animate the source into a video.

One needs 20 minutes or more speech data of the person depicted in the source to be succesful. This data is used to train the voice-to-voice model


# Face animation

The GAN based model, Latent-Image-Animator (LIA), was used to animate the source. We used the "vox.pt" model weights that is used when LIA needs to animate the motion of the face in a closeup portrait of the source.

Paper : https://arxiv.org/abs/2203.09043

Upload `LIA-colab.ipynb` in colab to reproduce the image animation that is used in the DEEPFAKE sample. 

Remember to download the data and follow the instructions in the notebook. The data relevant for the image animation is located in the `data/vid/` directory in the Open Science repository. When running the notebook, the resulting vide will be located in `DEEPFAKE/LIA/res/vox/`.

After generation of the animation, we use prolific to synchronize the animated video, with the original video.

# Voice cloning

To replicate the voice of the person depicted in the source, we trained a model on the voice data using the repository So-Vits-Svc-fork. We followed the repository's instructions on how to set up the conda environment, and how to train a finetuned model. We split the voice data into 7 seconds long `wav` files, and trained the voice model. You can use the following linux command to divide the file into smaller voice segments:

```
ffmpeg -i somefile.mp3 -f segment -segment_time 7 -c copy out%d.wav
```

The data is also located in the `data/voice/` directory in the Open Science repository. 

We altered only batch-size and epochs, but this ultimately depends on the compute resources available. We used a batch-size of 20 and trained for 15 hours, with 3833 epochs, going through 107 samples.

Repository : https://github.com/hcds-itu/so-vits-svc-fork.git


