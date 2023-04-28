## DEEPFAKE
DEEPFAKE project funded by Meta Research

# Introduction
This project has been created for research purposes only. The samples have been shown to participants of a scientific survey. They were informed about the origin of the samples and their fabrication.

The aim of this repository is to generate hyper-realistic, videos of people, which fabricates speeches of specified people that never existed.

A person to imitate (source), and a video of a person to drive the motion and speech of the source in a generated video (driver) are required.
To animate the source according to the motion of the driver, it is possible to use a pretrained image animation model, which requires a closeup portrait of the source.
To recreate the voice of the source using the speech from the driver, one would need to train a voice-voice model. This would require approximately 20 minutes or more speech data of the source.

# Background:
There are many paths to go to imitate a source visually. Besides image animation, different face swap models were considered. Although the quality of the results are realistic, the results look more like a fusion of the source and driver rather than one or the other. 
Finetuned text to video diffusion models based on stable-diffusion were also considered. The results however were not realistic.


# Method

For the face animation, we used Latent-Image-Animator (LIA). LIA is a GAN based model with the aim of animating motion in a target image from a motion donor (video). We used an image of the source and do a zoom and change in quality to 256 x 256 pixels. Equally, we would do a zoom and change the quality of the driver to 256 x 256 pixels. We would pass these a arguments to LIA.

Paper : https://arxiv.org/abs/2203.09043
Colab for producing results : https://colab.research.google.com/drive/1lrze_pIUh3dqEKawunXN5NXGzbFpp1KS?usp=sharing

For voice recreation, we used the public, open source model So-Vits-Svc-fork. We sampled approximately 20 minutes of speech of the source, split it into 7 seconds long wav files, and trained the voice model.

Github : https://github.com/hcds-itu/so-vits-svc-fork.git
follow installation of fork -> prepare data by downloading video -> divide into snippets of approx 6s (ffmpeg -i somefile.mp3 -f segment -segment_time 6 -c copy out%d.wav)

