## Welcome to the Cognitive Services

In this tutorial I am  going to integrate two of the cognitive services that I have implemented through Azure Machine Learning  course. First, I will create a Custom Vision Service to train a model for identifying objects. Second, I will integrate  a chat bot service  with the custom vision service that will automatically respond to our users depending on what they are asking for. Finally, these services can be connected to other channels such as Microsoft Teams or Skype Messenger.

***

### 1. Custom Vision Service
We create new custom vision service using Azure subscription. My location is still going to be set to south central US. Im going to keep using my existing research group as you see in the following pictures. The service will be created and deployed just in few minutes. 


![create_new_custom_vision_services_on_azure_](https://user-images.githubusercontent.com/26039303/49919411-c5b80d80-fea6-11e8-8c4b-4a6ea671b8b4.png)

![choose_predictions_pricing_tier](https://user-images.githubusercontent.com/26039303/49919545-3e1ece80-fea7-11e8-9c22-f742e4ae2fff.png)

Every call to Custom Vision Training API requires a subscription key. This key needs to be either passed through a query string parameter or specified in the request header. We can find the keys in the API resource 'Overview' or 'Keys' from the left menu. We can simply visit  the Custom Vision website where we can create a project (without using any code), upload picture of objects to be identified, organize them in groupe by taging them. The following view will display our Fruit Classifier project. 

![customvisiondeployed](https://user-images.githubusercontent.com/26039303/49920683-5a246f00-feab-11e8-88b2-0ffe30b880ad.png)



![fruit_classifier](https://user-images.githubusercontent.com/26039303/49921498-f3ed1b80-fead-11e8-826c-945bea3afbc0.png)


Then, we can run a test to observe if the desired object is identified correctly. The prediction will show probability of the most scored tags in descending order. In performance window we can adjust the threshold slider to get best precision and recall values.


![identifiedapple](https://user-images.githubusercontent.com/26039303/49925169-67942600-feb8-11e8-8763-01e08d84c8ae.png)


![performance](https://user-images.githubusercontent.com/26039303/49925307-c78acc80-feb8-11e8-9d15-7e13f3b56540.png)
