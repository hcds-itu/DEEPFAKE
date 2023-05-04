## DEEPFAKE
DEEPFAKE project funded by Meta Research

# Introduction
This project has been created for research purposes only. The ethical guidelines of the submodules have been followed, which is also expected of anyone intending to replicate the scientific discoveries. 

The aim of this project is to generate realistic videos of specified people that never existed ie. convincing deepfakes. The resulting deepfakes of this project were generated with consent of the data giving parts, and they have been shown to participants of a scientific survey. These participants were informed about the origin of the results and their fabrication.

# Requirements for deepfake

A person to imitate (source), and a video of a person to drive the motion and speech of the source (driver) are required.
To animate the source according to the motion of the driver, it is possible to use a pretrained image animation model, which requires a closeup portrait of the source.
To transform the driver's voice to the source's voice, one would need to train a voice-voice model. This would require approximately 20 minutes or more speech data of the source to be succesful.


# Face animation

For the face animation, Latent-Image-Animator (LIA) was used. LIA is a GAN based model with the aim of animating motion in a target image from a motion donor (video). We used the "vox.pt" model that animates speech in a closeup portrait of the source. We used a still image of the source, and zoomed in on the face. Likewise, the video of the driver must also be close to the face. The resolution of both the source and the driver must be 256 x 256 pixels. We would pass these a arguments to LIA.

Paper : https://arxiv.org/abs/2203.09043

Colab for reproducing results : https://colab.research.google.com/drive/1lrze_pIUh3dqEKawunXN5NXGzbFpp1KS?usp=sharing

Later, we used prolific to put the resulting, animated video of the source, and put it into place of the still image, where the zoom had happened.

# Voice cloning

For voice transformation, we used the repositroy So-Vits-Svc-fork. We followed the repository's instructions on how to set up the conda environment, and how to train a finetuned model. We sampled approximately 20 minutes of speech of the source, split it into 7 seconds long wav files, and trained the voice model. We altered only batch-size and epochs, but this ultimately depends on the compute resources available. We used a batch-size of 20 and trained for (x) hours, with (y) epochs, going through (z) samples.

Github : https://github.com/hcds-itu/so-vits-svc-fork.git

follow installation of fork -> prepare data by downloading video -> divide into snippets of approx 7s (ffmpeg -i somefile.mp3 -f segment -segment_time 7 -c copy out%d.wav)


# Other paths

There are many paths to go to imitate a source visually. Besides image animation, different face swap models were considered. Although the quality of the results are realistic, the results look like a fusion of the source and driver rather than one or the other. 
Finetuned text to video diffusion models based on stable-diffusion were also considered. The results however were not realistic.

