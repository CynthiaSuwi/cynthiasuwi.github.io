---
layout: post
title:  "Google Summer of Code: Work Submission"
date:   2018-08-08
excerpt: "And thus, final code submission and evaluations has opened. Now my task is to finally submit my work."
project: true
tag:
- GSoC
comments: true
---

# Google Summer of Code: Work Submission

Hello, all. 🙂

And thus, GSoC is about to end. I've been finishing up the coding on my project and working with my mentors. Tuesday, August 14th 16:00 UTC is Final Evaluation deadline.

![](https://github.com/CynthiaSuwi/cynthiasuwi.github.io/blob/master/_posts/img/final_evaluation.png?raw=true)

My project on “[Automatic Speech Recognition for Speech-to-Text on Chinese](https://summerofcode.withgoogle.com/projects/#5284664500027392)” was developed under [Red Hen Lab](http://www.redhenlab.org/). In this project, a Speech-to-Text conversion engine on Chinese is established, resulting in a working application.

During 12 weeks, I developed my project on [GitHub://ASR-for-Chinese-Pipeline](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline). If you like, you can go through the project' [README](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/README.md). Here, I summarized the work done by me(ordered by timeline).

*Please note that this is just a summary of what I did during this summer. If you like, you can read my weekly blogs [here](https://cynthiasuwi.github.io/posts/) for better understanding.*

## 1. Help Prepare the Language Model for Red Hen Lab

We fixed all the bugs and successfully downloaded the [70GB model for Mandarin](http://cloud.dlnel.org/filepub/?uuid=245d02bb-cd01-4ebe-b079-b97be864ec37) using [wget](https://cynthiasuwi.github.io//GSoC-Week2/) on CWRU HPC on May 22nd.

## 2. PaddlePaddle Docker appliance on the CWRU HPC
I gave a try for [Docker appliance](https://cynthiasuwi.github.io//GSoC-Week3/) following the steps Prof. Peter did before. I had an idea that the image itself has no problem. And what we need to do is to modify $HOME path inside the image. It turned out that my idea is right. As a result, we can finally run DeepSpeech2 on CWRU HPC. This is the very first step and establish a foundation for future works.

## 3. DeepSpeech2 Paper Review
Our Chinese language model based on [Baidu’s Deep Speech 2 paper](Baidu’s Deep Speech 2 paper), with [PaddlePaddle platform](https://github.com/PaddlePaddle/Paddle). Since we will directly use the [released Mandarin LM Large](http://cloud.dlnel.org/filepub/?uuid=245d02bb-cd01-4ebe-b079-b97be864ec37) as our language model, it is important for us to fully understand its operation principle.

## 4. Code Walkthrough
I [walked throgh the whole codes](https://cynthiasuwi.github.io//GSoC-Week6&7/) to understand its logic and operation in [DeepSpeech2](https://github.com/PaddlePaddle/DeepSpeech). It helps me a lot to make modification for fitting Red Hen Lab CWRU HPC server.

## 5. Create a Singularity Recipe for DeepSpeech2 Model
I created a [Singularity Recipe](https://github.com/RedHenLab/singularity_containers/blob/master/Singularity.DeepSpeech2_shuwei) for our DeepSpeech2 model so that we don't need to trouble unsetting $HOME each time we enter the singularity image. What's more, we can also modify the environment with higher flexibility.

## 6. Run Aishell on CWRU HPC server
**I make a big breakthrough and successfully run [the whole workflow in DeepSpeech2 on CWRU server](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline#running-code-at-cwru-hpc). I think it an important milestone for evaluation. I am also so proud that I fixed all the bugs the team previously faced, including memory problem, CUDA problem, environment problem, UTF-8 Chinese problem, language model problem, batch size problem and so on!**

The main scripts involved in Code-Running on CWRU HPC:
1. [Details in run_data.sh](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/examples/aishell/run_data.sh):
    - Codes in run_data.sh can mainly be divided into 3 parts:
      - [Generate Manifest](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline#1-generate-manifest): [data/aishell/aishell.py](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/data/aishell/aishell.py)
      - [Compute Mean & Stddev for Normalizer](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline#2-compute-mean--stddev-for-normalizer): [tools/compute_mean_std.py](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/tools/compute_mean_std.py)
      - [Build Vocabulary](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline#3-build-vocabulary): [tools/build_vocab.py](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/tools/build_vocab.py)

2. [Details in run_infer_golden.sh](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/examples/aishell/run_infer_golden.sh):
    - Codes in run_data.sh can mainly be divided into 2 parts:
      - Download well-trained model: [models/aishell/download_model.sh](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/models/aishell/download_model.sh)
      - Infer:[infer.py](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/infer.py)
      
3. [Details in run_test_golden.sh](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/examples/aishell/run_test_golden.sh):
    - The most important part in codes is evaluation:
      - Evaluation:[test.py](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline/blob/master/test.py)

## 7. Establish an ASR system based on PaddlePaddle and Kaldi
Different from direct prediction of word distribution using deep learning end-to-end model in DeepSpeech, the example in this blog is closer to the traditional ASR process. I tried to use phoneme as the modeling unit, focusing on the training of the acoustic model in ASR,using Kaldi to extract the features of the audio data and the label alignment, and integrate the decoder of the Kaldi to complete the decoding.I finished [a complete example using Aishell dataset](https://github.com/CynthiaSuwi/ASR-for-Chinese-Pipeline#asr-system-based-on-paddlepaddle-and-kaldi) on my local PC. I hope I am able to make it fit the CWRU HPC server in the future days.

# Conclusion
I am thankful to my primary mentors - Prof. Mark Turner and Prof. Francis Steen, for all the support they provided. They always supported me when I faced some issues/bugs in my code. Also, I would like to thank Michael Pacchioli sir, for all the help he provided on Red Hen Lab’s Slack channel. I will also thank PaddlePaddle’s Deep Speech’s developers. Lastly, I would like to thank Prof. Robert Ochshorn,  Prof. Peter Uhrig, and all other Red Hen Lab members for their support.

And most importantly, I express my gratitude to the people behind Google Summer of Code. I had a very enjoyable experience working in GSoC 2018. I hope I keep contributing.
![](http://markturner.org/RedHenNoBackgroundWebsiteSmall.png)
