## Welcome to the Cognitive Services

In this tutorial I am  going to integrate two of the cognitive services that I have implemented through Azure Machine Learning  course. First, I will create a Custom Vision Service (Fruit classifier project) to train a model for identifying objects without writing any code. Second, I will write some code in Web bot App to create the Car Brand Classifier project. The system will integrate  a chat bot service  with the custom vision service that will automatically respond to our users depending on what they are asking for. Finally, these services can be connected to other channels such as Microsoft Teams or Skype Messenger.

***

### 1. Custom Vision Service
In this project I will use my existing Azure pass. First, I create a custom vision service using Azure subscription. My location is still going to be set to south central US and I keep using my existing research group as you see in the following pictures. The service will be created and deployed just in few minutes. 


![create_new_custom_vision_services_on_azure_](https://user-images.githubusercontent.com/26039303/49919411-c5b80d80-fea6-11e8-8c4b-4a6ea671b8b4.png)

![choose_predictions_pricing_tier](https://user-images.githubusercontent.com/26039303/49919545-3e1ece80-fea7-11e8-9c22-f742e4ae2fff.png)

Every call to Custom Vision Training API requires a subscription key. This key needs to be either passed through a query string parameter or specified in the request header. We can find the keys in the API resource 'Overview' or 'Keys' from the left menu. We can simply visit  the Custom Vision website where we can create a project (without using any code), upload picture of objects to be identified, organize them in groupe by taging them. 

![customvisiondeployed](https://user-images.githubusercontent.com/26039303/49920683-5a246f00-feab-11e8-88b2-0ffe30b880ad.png)


The following view will display our Fruit Classifier project. I have created four class of fruit by assigning them a tag.


![fruit_classifier](https://user-images.githubusercontent.com/26039303/49921498-f3ed1b80-fead-11e8-826c-945bea3afbc0.png)


Then, we can run a test to observe if the desired object is identified correctly. The prediction will show probability of the most scored tags in descending order. In performance window we can adjust the threshold slider to get best precision and recall values.


![identifiedapple](https://user-images.githubusercontent.com/26039303/49925169-67942600-feb8-11e8-8763-01e08d84c8ae.png)


![performance](https://user-images.githubusercontent.com/26039303/49925307-c78acc80-feb8-11e8-9d15-7e13f3b56540.png)

By clicking on setting icon in the upper right corner we will find ProjectId, Training Key, Training Endpoin, Prediction Key and Prediction Endpoint. In the dollowing sections we are going to write some codes and use the above mentioned information to create a project, send a request (by bot app) to be compared with our trained model.


![setting](https://user-images.githubusercontent.com/26039303/49938842-5ad4f980-fedb-11e8-9704-c59ca82a43a9.png)

### 2. Web App Bot
I created a bot service app in Azure portal and I named this to be LPA bot service. Further, I select the subscription type, resource groupe, location and prising tier. I used my Azure pass and choosed a free prising tier which allows me to have 10000 premium messages. 


![create_web_app_bot](https://user-images.githubusercontent.com/26039303/49929591-205f6280-fec3-11e8-923b-1262b2a76cb5.png)


There is also an option to choose between  different SDK version and programming languages. I choosed to go for C# template. It is the basic template but it carries the files and code necessary to implement this project. Now let's go ahead and navigate over to the built tab where we start coding our bot. However, we can download the source code and develop the bot locally, using preferred Development Environment. There is possibility to add intelligence to the bot with services such as: Luis, QnAMaker, and Dispatch. 


![webbotappformcreation](https://user-images.githubusercontent.com/26039303/49929791-99f75080-fec3-11e8-85ed-d87204483b13.png)


In this project we are going to write some codes. We can simply make quick changes to bot code online, run build.cmd in the editor console, and see the changes instantly. The online code editor gives us ability to download the source code. As we selected C# template than we're going to have a visual studio solution. This soloution can be implemented with continous development / integeration to push all changes back to a repository.

![build_online_code_editor](https://user-images.githubusercontent.com/26039303/49929610-2f461500-fec3-11e8-8ab3-a4f5a7501965.png)


 Let's go ahead and open the on line code editor. Then, we navigate to EchoDialog.cs. Here we observe the main functionalities and we are going to focus "Task StartAsyncon" and "Task MessageReceivedAsync" which also called task async node. 
 
 ![echodialog](https://user-images.githubusercontent.com/26039303/49935567-a2568800-fed1-11e8-8d0b-d559fd13f02d.png)
 
 
 ![code1](https://user-images.githubusercontent.com/26039303/49937019-ce740800-fed5-11e8-8558-db9507da757f.png)











