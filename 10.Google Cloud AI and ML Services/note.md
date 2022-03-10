### Overview of Google Cloud AI and ML Services
- AI Building Blocks provide AI through simple REST calls  

- Cloud AutoML enables training models on custom datasets    

- AI Platform provides end-to-end ML pipelines both on-premises and cloud  
  + customers can use AI platform to perform machine learning techniques all the way from training the models tutoring the models to deploying the models.  

- AI Hub is a Google hosted repository to discover, share, and deploy ML models  

- Google Cloud Platform offers comprehensive set of ML & AI services for beginners and advanced AI engineers
  + It is a collection of artifacts and various resources that can be shared by teams or even the public domain.  

### 1. AI Building Blocks(check the PDF)
- **SIGHT**  
  + Vision: Derive insights from images in the cloud or at the edge.
      = perform object detection or image classification by simply uploading the image or sending the image to the API.

  + Video: Enable powerful content discovery and engaging video experiences.  

- **CONSVERSATION**
  + Dialogflow: Build virtual agent and other conversational experience.    

  + Cloud Text-to-Speech API: Convert text to human-like speech using WaveNet voice.    

  + Cloud Speech-to-Text API: Convert speech to text automatically with outstanding accuracy.  

- **LANGUAGE**
  + Translation: Dynamically detect and translate between languages.

  + Natural Language: Reveal the structure and meaning of text through machine learning.    
    = extract intents and actions from the plain clear text that is actually sent to the API.  

- **STRUCTURED DATA**
  + AutoML Tables: Automatically build and deploy state-of-the-art machine learning models on structured data.  

  + Recommendations AI: Deliver highly personalized product recommendations at scale.  

  + Cloud Inference API: Quickly run large-scale correlations over typed time-series datasets.  

### 2. AutoML(https://cloud.google.com/automl/docs?hl=en)
The building blocks provide APIs that you can invoke by sending data, but there is one data point at a time. What if you want to train a custom model but do not want to write complex code about neural networks or artificial neural networks? -> AutoML -> bring data and walk away with custom model.

- Cloud AutoML enables training high-quality models specific to a business problem  
- Custom machine learning models without writing code  
- Based on Google’s state-of-the-art machine learning algorithms  
- AutoML Services  
- Sight  
  + Vision  
  + Video Intelligence   
- Language  
  + Natural Language  
  + Translation  
- Structure Data  
  + Tabular data  


> when you send an image of a dog to the building block vision API, you get back a payload that says it is an animal and it is a dog. However, if you have a business problem where you need to identify a specific breed of the dog, cloud vision API, or the building block API doesn't directly support that, you need to train a custom model that can differentiate between one build of the dog versus the other.

> Assuming you have a large data set that is structured into a set of dogs based on the breed and their differences. You can take that data set and use Auto ML to create a custom model so when you send a dog image to the custom model trained through Auto ml, it not only recognizes that as a dog but it also tells you which breed it is because it has been on a data set that had multiple breeds.

### 3. AI Platform
Meant for advanced use cases such as to **build a ML Pipeline**. It targets data scientists and machine learning engineers who are actually creating custom machine learning models and leveraging the pipeline that is provided by machine learning platforms.

The next level to Auto ML, it exposing the infrastructure to manage the end-to-end lifecycle of machine learning models. it's an open and portable framework for developing machine learning models it runs on Prem as well as in the cloud.

- Covers the entire spectrum of machine learning pipelines  

- It is Built on Kubeflow, an open source ML project based on Kubernetes  

- Includes tools for data preparation, training, and inference  

> so Google AI platform includes tools for data preparation training and inference, is just like a data processing pipeline. An ML processing pipeline is a comprehensive set of stages combined into a pipeline and KobeFlow is a project that basically simplifies the process of creating these pipelines with multiple stages below.  

**Ingest data -> Prepare -> Preprocess -> Discover -> Develop -> Train -> Test & Analyze -> Deploy**

> customers running on-premises Kubernetes infrastructure can deploy AI platform on Prem, and it can be seamlessly extended to the cloud.
which means they can train on Prem but deploy it in the cloud or train in the cloud but deploy the models on Prem.

### 4. AI Hub
During the development of ml models and AI models, there are a lot of artifacts that get generated from datasets to fully trained machine learning models to Jupyter notebooks and artifacts that can be used for deployment and so on. hence, the AI hub acts as the single source of truth and it is the database for all those artifacts and entities generated during the development of machine learning models, and those artifacts can be shared in a collaborative fashion with the AI hub.

- Hosted repository of plug-and-play AI components    
- Makes it easy for data scientists and teams to collaborate   
- Contains private and public content  
- AI Hub includes  
  + Kubeflow Pipeline components   
  + Jupyter Notebooks  
  + TensorFlow modules  
  + VM Images  
  + Trained models  
  + ...  

### 5.Demo - Image Recognition with Cloud Vision API
We will upload an image and let cloud vision API come back with the annotation labels that explain what is actually inside the image.
```
# go to cloud.google.com/vision
# try to image file without writing code
# try to upload a mixed image
# check the results
```

### 6. Use Cases.
check the doc
