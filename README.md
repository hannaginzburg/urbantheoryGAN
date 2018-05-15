﻿# urban_theory_GAN
#### Kai Matheson & Hanna Ginzburg, Vassar College
##### This work was completed as part of an independent study on machine learning.


<p align="center">
<img src="https://github.com/hannaginzburg/urbantheoryGAN/blob/master/giphy.gif">
</p>


This project aims to reclassify the American city and challenge existing urban sector models. The motivation behind the project is the conception that existing theoretical models of U.S. cities are too general to be accurate. Furthermore, the assumptions crucial to laying the groundwork for some of these models may be spurious; for example, demand behavior might not actually manifest as it appears in the concentric ring theory (that wealthier, working consumers cluster towards a city center and lower-paid consumers cluster around the outside of a metropolitan area).

We attempt to train a generative adversarial neural network (GAN) with pictures of maps of socioeconomic distributions within cities -- using the top 25% most densely populated core-based statistical areas (CBSA), of which all are metropolitan statistical areas (MSA), and data on median household income by census tract collected by the 2010 U.S. Census. Generative adversarial networks are implemented by a system of two neural networks contesting with each other; one network generates candidates and the other evaluates them. Typically, the generative network learns to map from a latent space to create images that resemble a particular data distribution of interest, while the discriminative network discriminates between instances from the true data distribution and candidates produced by the generator. The generative network's training objective is to increase the error rate of the discriminative network (i.e., "fool" the discriminator network into believing the generated outputs have come from the true data distribution). 

In this case, we generate images of “fake” city maps that are representative “enough” of the original dataset to deceive the discriminator. In simpler terms, the network uses existing maps of MSAs to create representative outputs of what the socioeconomic distribution of real urban areas looks like in the United States. We use the Keras library implemented in Python to train this GAN. Keras is a high-level neural networks API, written in Python, with the back-end of TensorFlow, and easily deployable across a greater range of platforms than any other deep learning framework. It was developed with a focus on enabling fast experimentation, and is backed by key companies like Google and Microsoft.  

Without the help of machine learning, it would be difficult for humans to generalize from existing maps. The most salient value this GAN provides is its ability to view existing maps from many more angles than a simple pair of human eyes (i.e. to sample from the sample space of existing maps, rather than relying on human memory and limited visual processing). This allows the network to create representative MSA “outputs” that are significantly more accurate than any human artist or social scientist.

In choosing how to map a city or metropolitan area, we considered various designations made by the U.S. Census. Metropolitan divisions are made up of pieces of metropolitan statistical areas, while other units such as micropolitan statistical areas or urban areas appear to be too large and encompass smaller towns. MSAs are the units of measurement most often used in urban economics papers, further validating their importance. We avoid very rural areas by just using the top 25% in population size of CBSAs. Population size should be uncorrelated to the structure of a city, so we can assume there is no bias here. 

In GIS, we justify our data clustering methods into “jenks” (via the natural breaks optimization method, which seeks to reduce the variance within clusters and maximize the variance between clusters) by pointing to outputs from the Census Bureau as a guide (https://www.census.gov/library/visualizations/2015/acs/2010-2014-acs-hh-income.html). This is closest we could get to “convention” in the practice of clustering household income brackets within MSAs. We furthermore justify our resizing of images in the dataset as 256x256 pixels as per convention outlined in OpenAI, by experts like Ian Goodfellow (inventor of generative neural networks) ( https://blog.openai.com/generative-models/).

We encountered some technical difficulties while implementing this project; the full number of parameters we had to run in order to generate 256x256 images with color ended up being over 4.5 million. Therefore, we decided to reduce the size of the images to 28x28 pixels and transform them to grayscale. The overall output from this simplified GAN shows relatively random distributions of color concentration, showing that there may not be a cohesive theory pertaining to the actual arrangement of U.S. cities by household income. We would need to run our model with more epochs (trials of the GAN) and a higher number of pixels to say something more conclusive about the viability of traditional, theoretical models of cities in the U.S. However, we believe these results are a good place to start.

All code used in building the neural network is credited to Mattia Spinelli from his Medium article (https://medium.com/@mattiaspinelli/simple-generative-adversarial-network-gans-with-keras-1fe578e44a87) and his corresponding repository (https://github.com/daymos/simple_keras_GAN).

To run the code, first download the repository. Then upload the iPython notebook into Google Colaboratory. When you run the command that begins with "uploaded = ", you will need to upload both the "256x256maps.zip" file and the "requirements.txt" file. "256x256maps.zip" is the dataset, while the other zip files are examples of output from running a certain pixel size image on however many epochs. It will output a zip file of sample images from every 10 epochs (signified by "save_interval=10" in the code, but adjustable to your preference). If you are not using Google Colab to run the code, some of the lines at the beginning and end for data processing should be removed. You may also have to delete the exclamation point in front of the pip command-- this syntax is what is used in Google Colab. 
