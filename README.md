## Welcome to the Cognitive Services

In this tutorial I am  going to integrate two of the cognitive services that I have created through Azure Machine Learning  course. First, I will create a Custom Vision Service that train a model for identifying objects. Second, I will integrate  a chat bot service  with the custom vision service that will automatically respond to our users depending on what they are asking. Finally, these services can be connected to other channels such as Microsoft Teams or Skype Messenger.

***

### 1. Custom Vision Service
We create new custom vision service using Azure subscription. My location is still going to be set to south central US. Im going to keep using my existing research group as you see in the following pictures. The service will be created and deployed just in few minutes. 


![create_new_custom_vision_services_on_azure_](https://user-images.githubusercontent.com/26039303/49919411-c5b80d80-fea6-11e8-8c4b-4a6ea671b8b4.png)

![choose_predictions_pricing_tier](https://user-images.githubusercontent.com/26039303/49919545-3e1ece80-fea7-11e8-9c22-f742e4ae2fff.png)

Every call to Custom Vision Training API requires a subscription key. This key needs to be either passed through a query string parameter or specified in the request header. We can find the keys in the API resource 'Overview' or 'Keys' from the left menu. We can simply visit  the Custom Vision website where we can create a project(without using any code), upload picture of object to be identified, organize them in groupe by taging them. The following view will display our Fruit Classifier project.


![customvisiondeployed](https://user-images.githubusercontent.com/26039303/49920683-5a246f00-feab-11e8-88b2-0ffe30b880ad.png)


![customvision_website](https://user-images.githubusercontent.com/26039303/49920689-65779a80-feab-11e8-95c9-6a2a1ca6096d.png)


![fruit_classifier](https://user-images.githubusercontent.com/26039303/49921498-f3ed1b80-fead-11e8-826c-945bea3afbc0.png)
