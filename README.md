# operating-room-assistance-

# Evaluating Edge & Cloud Computing in the Operating Room

This experiment explores the tradeoff between Edge and Cloud computing for real-time assitance in the operating room.
It should take 2-3 hours to run this experiement.

You can run this experiemnt on the [Chameleon](https://chameleoncloud.org/) testbed. To run this experiment you should already have an account on Chameleon, be part of a project, and have configured keys om CHI@Edge, CHI@UC, and KVM@TACC.

## Background

### My Application 

Real Time AI assitance plays a significant role in various industries, including customer service, healthcare, finance, and more. These systems use artificial intelligence and other processing techniques to provide real-time support and assistance to users. In this specfic experiment we will be using AI to see how fast a prediction can be made for a human surgeon in an operating room, OR. With time as the objective, it is crucial for us to examine where the compution of a prediction are made either in a edge device or in the cloud.

### Edge vs Cloud

In edge computing, data is processed locally on edge devices or servers. With the compuations being done locally it can reduce latency and network bandwidth and improve security. In our edge scenario, images from our chosen dataset would be processed on the edge device that includes the machine learning model and then it would display the prediction. Given that it is a smaller device, the Inference Time, the time it takes to make prediction, can vary based on the load given to the device.

Whereas cloud computing, the computations are done remotely, so the images on the edge device would be sent to the cloud that has the machine learning model then sent back with prediction. When sending information over a network (in our case LAN, local area network), it is called Network Transfer time. Network Transfers can take longer depending on the amount of data and newtowk bandwidth present. Although the network transfer time can take long, the inference time can be smaller since the cloud is a bigger device that can handle larger loads of data.

Due to the cloud being a larger and more powerful device it can have smaller inference times, but it's network transfers are a big contribution to how fast the prediction can be displayed. While on the other hand edge devices have little to no newtwork transfers, but okay inference times. With these tradeeoffs we must test which computation location wwould be optimal for real time assitance in the OR. Late predictions aren't useful predictions.

### Methodology

For this experiment, we will be using the [SARAS-MESAD Multi-domain Endoscopic Surgeon Action Detection](https://saras-mesad.grand-challenge.org/) dataset.

In order to obtain the models provided, I used this dataset to train a machine on [Teachable Machines](https://teachablemachine.withgoogle.com/) with 21 classes. These classes will be the predictions the model can make when provided with an image. In order to make this experiment specfic to a hospital we used a local area network. One deemed as bad ethernet and the other as good ethernet to represent cases were there's more or less bandwidth in a network in order to measure network transfer times in both edge and cloud computing.

The devices used to make the predictions are Coral Dev Board with CPU, Coral Dev Board with TPU, Raspberry Pi 4 with CPU, GPU with LAN, GPU with high quality LAN, GPU with optimizations and LAN, and lastly GPU with optimations and high quality LAN. THe first three are our edge scenarios and the last four are our cloud scenarios.

## Results

![image](https://github.com/nanakordie4/operating-room-assistance-/assets/141275613/72f2efca-b47a-42f7-8913-8c766810e2a5)


## Run my experiment

### Set up resources at CHI@Edge
first least for raspi4
set up server
insteall ml
### Measure inference time at CHI@Edge
how to copy models to chi@edge provide test images etc
add folder, name it edge, in folder put basic tflite model edgetpu, text.txt, test images
### Set up resources at CHI@UC
first lease for rtx6000gpu
set up server
install machine learning
### Measure inference time at CHI@UC
how to copy models to chi@edge provide test images etc
add folder, name it edge, in folder put h5 model, text.txt, test images
### Set up resources at KVM@TACC
set up stuff
### Measure network transfer times at KVM@TACC
set it up how it is on my computer

## Notes

### References
copy refrences from poster

### Acknowledgements
I’d like to acknowledge support of NYU TANDON, K12 STEM outreach center, The Pinkterton Foundation, and my mentors at the New York State Center for Advanced Technology in Telecommunications: Chandra Shekhar Pandey and Fatih Berkay Sarpkaya

















