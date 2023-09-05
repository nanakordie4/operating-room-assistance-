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

After conducting the experiments, we were able to conclude that GPU and TPU can both be fast for inferences, but for cloud computing you also need to consider the network delay. On the left side of the graph we have our edge devices and on the other cloud. Although GPU takes a tad bit longer due to the newtwork transfer time, the blue color , its inference time, the cyan color, is quite similar to the best edge device used. If we ignore network transfer time, edge is definitely better for real time assitance. The only con is it is the more expensive option. Every area a compuattion is needed to be done an edge device would have to be placed there whereas with cloud we would only need one GPU device for all the computations. Both options are great, but it truly depends on what a hospital is willing to spend. 


## Run my experiment

### Set up resources at CHI@Edge

Let's start off with our Raspberry Pi 4 experiment!

In order to complete this experiment you must have a lease for a Raspberry Pi 4. By accessing [GUI for CHI@Edge](https://chi.edge.chameleoncloud.org/project/container/containers), there you can obtain a lease for a Raspberry Pi 4. Once you are sure you have a lease, you can run the [Edge- CPU experiment](https://github.com/teaching-on-testbeds/edge-cpu-inference/) on a Chameleon Jupyter environment. 

Using the provided model_quant_updated.tflite , our machine learning model, and the label.txt file upload them to the image_model folder within the Jupyter environement. Also include the all test images provided into that same folder. The experiement should run pretty smoothly! Be sure to run each cell one at a time and fill in the required information. When prompted to fill the lease ID and project ID, the specfic number on the top left handside of CHI@Edge, refer back to the [GUI for CHI@Edge](https://chi.edge.chameleoncloud.org/project/container/containers)

### Measure inference time at CHI@Edge

When finding out the inference time for a particular model it's important the path used in the code is correct. If a file, folder, and or model is spelled incorrectly the experiement won't work. When you reach line 36 it should mirror something similar to this:

result = container.execute(my_container.uuid, 'python /root/image_model/model.py --model model_200_quant_updated.tflite --label labels.txt --image 1.jpg ')
print(result['output'])

Repeat line 36 for all ten test images. Be sure to change the image name or you will be testing the same image multiple times. Once you excute all the test for the basic edge device you can restart the experiment this time using the other model called model_quant_updated_edgetpu.tflite for the faster edge device. Make sure to record all 20 inference times! 


### Set up resources at CHI@UC
Now for our GPU experiment!

In order to complete this experiment you need another lease but for a RTX6000 GPU. Similarly you can access it at [GUI for CHI@UC](https://chi.uc.chameleoncloud.org/project/leases/), there you can obtain a lease for a RTX6000 GPU. Once you are sure you have a lease, you can run the [Cloud- GPU experiment](https://github.com/teaching-on-testbeds/cloud-gpu-inference) on a Chameleon Jupyter environment. 

Using the provided model.h5 , the specfic machine learningmodel for GPU  and the label.txt file again upload them to the image_model folder within the Jupyter environement. Also include the all test images provided into that same folder. The experiement should run pretty smoothly! Be sure to run each cell one at a time and fill in the required information. When prompted to fill the lease ID and project ID, the specfic number on the top left handside of CHI@UC, refer back to the [GUI for CHI@UC](https://github.com/teaching-on-testbeds/cloud-gpu-inference)

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

















