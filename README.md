## DEEPFAKE
DEEPFAKE project funded by Meta Research

# Introduction
This project has been created for research purposes only. Consent of the data giving parts must be given.

This github repo contains an image animation repository and a voice to voice cloning repository. The aim is to generate hyper-realistic, videos of people, which fabricates speeches of specified people that never existed ie. convincing deepfakes. The resulting deepfakes have been shown to participants of a scientific survey. The participants were informed about the origin of the results and their fabrication.

# Requirements for deepfake

A person to imitate (source), and a video of a person to drive the motion and speech of the source in a generated video (driver) are required.
To animate the source according to the motion of the driver, it is possible to use a pretrained image animation model, which requires a closeup portrait of the source.
To transform the driver's voice to the source's voice, one would need to train a voice-voice model. This would require approximately 20 minutes or more speech data of the source to be succesful.


# Face animation

For the face animation, Latent-Image-Animator (LIA) was used. LIA is a GAN based model with the aim of animating motion in a target image from a motion donor (video). We used an image of the source, did a zoom and changed the quality to 256 x 256 pixels. Equally, we would do a zoom and change the quality of the driver to 256 x 256 pixels. We would pass these a arguments to LIA.

Paper : https://arxiv.org/abs/2203.09043

Colab for reproducing results : https://colab.research.google.com/drive/1lrze_pIUh3dqEKawunXN5NXGzbFpp1KS?usp=sharing

(Afterwards, we used prolific to put the animated face video into place of the original video)

# Voice cloning

For voice transformation, we used the open source model So-Vits-Svc-fork. We followed the repository's instructions on how to set up the conda environment, and how to train a finetuned model. We sampled approximately 20 minutes of speech of the source, split it into 7 seconds long wav files, and trained the voice model. We altered only batch-size and epochs, but this ultimately depends on the compute resources available. We used a batch-size of 20 and trained for (x) hours, with (y) epochs, going through (z) samples.

Github : https://github.com/hcds-itu/so-vits-svc-fork.git

follow installation of fork -> prepare data by downloading video -> divide into snippets of approx 7s (ffmpeg -i somefile.mp3 -f segment -segment_time 7 -c copy out%d.wav)


# Other paths:

There are many paths to go to imitate a source visually. Besides image animation, different face swap models were considered. Although the quality of the results are realistic, the results look more like a fusion of the source and driver rather than one or the other. 
Finetuned text to video diffusion models based on stable-diffusion were also considered. The results however were not realistic.

