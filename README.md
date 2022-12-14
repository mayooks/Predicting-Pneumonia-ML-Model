# Predicting-Pneumonia-ML-Model
## Project Team Members: Kudzanai, Emmanuela, Noshaad, Maxwell and Chisimnulia
## Introduction
Pneumonia is a disease, usually caused by an infection, that affects the lungs and it is usually diagnosed by physicians using radiological imaging to determine the infectious agent that causes the disease. 15% of child deaths were caused by Pneumonia in 2017 making it the leading cause of death in children under 5yrs old.
![image](https://user-images.githubusercontent.com/99673859/187027944-a97507ed-63f1-46a8-900d-815d75f6de8f.png)

Again you can see that the death rate from pneumonia is highest in  Africa and Asia. A clear difference between richer and poorer countries. 
![image](https://user-images.githubusercontent.com/99673859/187027977-6c94c1a7-74fb-4c79-b87a-2d68c4798358.png)

Below is an example of chest X rays, and the kind of chest X rays that our model is going to analyse. The first one is a normal chest X rays and the other three are  examples of chest x-rays with different types of Pneumonia. Differentiating X-rays with Pneumonia and X-rays without, could be difficult, as you can see by looking at image 1 and 4.
<img width="805" alt="Pneumonia x-ray" src="https://user-images.githubusercontent.com/85926823/187033122-ac193f92-c356-419c-acd5-71d63594edf8.png">

Armed with this information and knowing that pneumonia cannot easily be detected with the human eye, we set out to develop a convoluted neural network (CNN) model that  can analyse chest x-ray image and determine whether a person has pneumonia or not.

At the end of this presentation, we hope that our model will be used in the healthcare industry to improve detection of pneumonia and ultimately reduce mortality rate especially in under 5 children.

## Data Extraction, Transformation and Loading
Our data was sourced from <a href="https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia">kaggle</a>
 and it was loaded onto AWS into a bucket ready for extraction. We used Google Colab to connect to our AWS bucket. We used some essential models for image processing such as CV2 and PIL, and various modules to create  get_data function that processes AWS objects into a (224, 224, 1) Numpy array that is fed into the CNN. We faced many challeges such as image adjustments, we had to change our images from bytes to jpeg, we changed them to grayscale and saved them into arrays to be reduced in size. We also had some data imbalance issues which we resolved using class weights.
 



## Machine Learning
A sequential convoluted deep nueral network was used to build the model. Arriving to a nueral network model that could successfully produce a model that could predict weather the image being processed was from a person with pnuemonia or not was complicated by the fact that the data imbablance.  There was an inbalance between images that where from a person with pnuemonia and those that where from a person that had no pnuemonia. Images from a person with pnuemonia were classed as pnuemonia and given a label of 1 and there were 3875 of them in the training data set. Whilst those from a person with no pnuemonia were classed as zero and there were 1341. The difference between the two was due to the fact that it is difficult to gather X-ray images from a person with no pnuemonia. To increase the dataset size and variability datagen dataaugementation was used to adjust some images and increase the data volume. Class weights were also used use to normalise the datasets however this proved to make no difference in the grand scheme of things. As the best performing machine learning model (model_1) was produced when there was an even number of classes. This was produced when the number of both normal and pnuemonia images was  in the training data set was 1341. Making the total number of images in the training dataset for this model 2682. The validation data appeared to be overfitting

![image](https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Images/final_optimised_model_performance.png)


The confusion matrix of the validation data from model-1 can be seen in the image below. The recall and precision from this model was very good. Of the 310 people that had pnuemonia only 30 (approximately 10 %) were classed as having no pnuemonia (false negatives). On the other had only 30 of the images that were from people that had no pnuemonia were classed by the model as having come from the a person that had pnuemonia. This makes to percentage of false postives approximately 20%. This shows that model-1 is able to identify x-ray from people with pnuemonia with good confidence. The Hierarchical Data Format version 5 (HDF5) file and jupyter notebook of this model can be found on these links <a href="https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Notebooks/model-0_(HDF5)_file.h5">model-0 HDF5 file</a>
 and <a href="https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Notebooks/final_Pnuemonia_model_optimised_1.ipynb">model-1 jupyter notebook</a>
 respectively

![image](https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Images/model-1%20performance.png)


Model-1 is our best performing model. This was produced after performing trials in which the number of images from people with no pnuemonia and those with pnuemonia was 1341 and 3875 respectively. Even though class weights were used to normalise the data. The model from the first trail wrongly predicted 22% of the positive (pnuemonia) instances in the validation data and 28% of the negative instances(no pnuemonia). The confusion matrix for this model is shown below and the jupter notebook for this model can be found here <a href="https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Notebooks/First_trial_notebook.ipynb">first trial notebook</a>


![image](https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Images/first_trial_model_performance.png)

Using kerastuner RandomSearch library it was possible to indentify parameters that improved on the first trial run by finding the best fit model based nueral network model that was used in the trial run and reducing the batch size from 32 to 16. This is model-0. The Hierarchical Data Format version 5 (HDF5) file and jupyter notebook of this model can be found here <a href="https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Notebooks/model-1_(HDF5)_file.h5">model-0 HDF5-file</a>
 and <a href="https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Notebooks/model-0_jupyter_notebook.ipynb">mode-0 jupyter notebook</a> respectively. The confusion matrix and classification report for this model is shown below. The model wrongly predicts 9% of the postive values and 20% of the negative values.  


![image](https://github.com/mayooks/Predicting-Pneumonia-ML-Model/blob/main/Images/model-0%20classification%20report.png)


