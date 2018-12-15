## Welcome to the Cognitive Services

In this tutorial I am  going to integrate two of the cognitive services that I have implemented through Azure Machine Learning  course. First, I will create a Custom Vision Service (Fruit classifier project) to train a model for predicting and identifying objects without writing any code. Second, I will write some code in Web bot App template to create a Car Brand Classifier project. Subsequently, I will send image of a cars over the bot channel and the bot app will respond back with predictions its receives from custom vision service. The system will integrate a chat bot service  with the custom vision service that will automatically respond to the users depending on what they are asking for. Finally, these services can be connected to other channels such as Microsoft Teams or Skype Messenger.

***

### 1. Custom Vision Service
In this project I will use my existing Azure pass. First, I create a custom vision service using Azure subscription. My location is still going to be set to south central US and I keep using my existing research group as you see in the following pictures. The service will be created and deployed just in few minutes. 


![create_new_custom_vision_services_on_azure_](https://user-images.githubusercontent.com/26039303/49919411-c5b80d80-fea6-11e8-8c4b-4a6ea671b8b4.png)

![choose_predictions_pricing_tier](https://user-images.githubusercontent.com/26039303/49919545-3e1ece80-fea7-11e8-9c22-f742e4ae2fff.png)

Every call to Custom Vision Training API requires a subscription key. This key needs to be either passed through a query string parameter or specified in the request header. We can find the keys in the API resource 'Overview' or 'Keys' from the left menu. We can simply visit  the Custom Vision website where we can create a project (without using any code), upload picture of objects to be identified, organize them in groupe by taging them. 

![customvisiondeployed](https://user-images.githubusercontent.com/26039303/49920683-5a246f00-feab-11e8-88b2-0ffe30b880ad.png)


The following view will display our Fruit Classifier project. I have created four class of fruit by assigning them to a tag.


![fruit_classifier](https://user-images.githubusercontent.com/26039303/49921498-f3ed1b80-fead-11e8-826c-945bea3afbc0.png)


Then, we can run a test to observe if the desired object is identified correctly. The prediction will show probability of the most scored tags in descending order. In performance window we can adjust the threshold slider to get best precision and recall values.


![identifiedapple](https://user-images.githubusercontent.com/26039303/49925169-67942600-feb8-11e8-8763-01e08d84c8ae.png)


![performance](https://user-images.githubusercontent.com/26039303/49925307-c78acc80-feb8-11e8-9d15-7e13f3b56540.png)

By clicking on setting icon in the upper right corner we will find ProjectId, Training Key, Training Endpoin, Prediction Key and Prediction Endpoint. In the dollowing sections we are going to write some codes and use the above mentioned information to create a project, send a request (by bot app) to be compared with our trained model.


![setting](https://user-images.githubusercontent.com/26039303/49938842-5ad4f980-fedb-11e8-9704-c59ca82a43a9.png)


In the performance page we can have information about image URL, Production key and content type which we will use in the next section.


![imageurl](https://user-images.githubusercontent.com/26039303/49941676-78a65c80-fee3-11e8-8506-2bc528bd50f6.png)

### 2. Web App Bot
I created a bot service app in Azure portal and I named this to be LPA bot service. Further, I select the subscription type, resource groupe, location and prising tier. I used my Azure pass and choosed a free prising tier which allows me to have 10000 premium messages. 


![create_web_app_bot](https://user-images.githubusercontent.com/26039303/49929591-205f6280-fec3-11e8-923b-1262b2a76cb5.png)


There is also an option to choose between  different SDK version and programming languages. I choosed to go for C# template. It is the basic template but it carries the files and code necessary to implement this project. Now let's go ahead and navigate over to the built tab where we start coding our bot. However, we can download the source code and develop the bot locally, using preferred Development Environment. There is possibility to add intelligence to the bot with services such as: Luis, QnAMaker, and Dispatch. 


![webbotappformcreation](https://user-images.githubusercontent.com/26039303/49929791-99f75080-fec3-11e8-85ed-d87204483b13.png)


In this project we are going to write some codes. We can simply make quick changes to bot code online, run build.cmd in the editor console, and see the changes instantly. The online code editor gives us ability to download the source code. As we selected C# template than we're going to have a visual studio solution. This soloution can be implemented with continous development / integeration to push all changes back to a repository.

![build_online_code_editor](https://user-images.githubusercontent.com/26039303/49929610-2f461500-fec3-11e8-8ab3-a4f5a7501965.png)


Let's go ahead and open the on line code editor. Then, we navigate to EchoDialog.cs. Here we observe the main functionalities and we are going to focus on "Task StartAsyncon" and "Task MessageReceivedAsync" which also called task async node. It will use a counter and keep track of all message been sent and displaying them. 
 
 ![echodialog](https://user-images.githubusercontent.com/26039303/49935567-a2568800-fed1-11e8-8d0b-d559fd13f02d.png)
 
 
 ![counter](https://user-images.githubusercontent.com/26039303/49952167-b8793e00-fefb-11e8-944f-5e69fb767d4d.png)
 
 
I have added following line of code to our template. I have defined a method to identify the brands and pass the image Url as a string.
Than we have to specify the request Url, header with prediction key and body. After finishing the code we run the build.cmd and waiting few seconds to install the packaged.
 
 ![code1](https://user-images.githubusercontent.com/26039303/49937019-ce740800-fed5-11e8-8558-db9507da757f.png)


![runbuildcmd](https://user-images.githubusercontent.com/26039303/49992335-0b96d380-ff84-11e8-9cb8-55d660305f08.png)


![build](https://user-images.githubusercontent.com/26039303/49992349-194c5900-ff84-11e8-9099-1377ead25803.png)


Now we go back to our test channel and send a request (sending an url) to custom vision service and get prediction of car brand. After few seconds We can see the result in the chat bot. As you see in the picture below, we get the prediction in json format. Since, I am familiar with this kind of information hence it is easy to read and understand the content. But we can not send this type of information to the user so we have to extract just the brand type and predict probability. 


![bmw](https://user-images.githubusercontent.com/26039303/49995259-e908b880-ff8b-11e8-9be9-a1e814c2586d.png)


We want to get the jason file deserialized and get the actual data. We just need to extract the first brand type and its prediction probability and then  display it to user. We copy the jason code we recieved from the service and we are going to generate a class out of this. To do so we navigate to http://jsonutils.com/ and paste the code here.


![jsonfile](https://user-images.githubusercontent.com/26039303/50034998-198a3a00-0000-11e9-9075-818892cdf5ad.png)


We copy the code generated here and paste it to our code in EchoDialog.cs file in Web Bot App in Azure Portal and we build it again. We test the service by send a image url in the test channel and we observe that the out put is different and more userfriendly.


![newcode](https://user-images.githubusercontent.com/26039303/50035909-180f4080-0005-11e9-9ab3-0d1dddf33b76.png)


![brandformated](https://user-images.githubusercontent.com/26039303/50035846-a9ca7e00-0004-11e9-9645-a928ed63dce5.png) 
 


Further, We navigate to Custom vision website (prediction page) and view the result.


![bmw2](https://user-images.githubusercontent.com/26039303/49996050-384fe880-ff8e-11e8-86b4-75c08baa43ee.png)


We can also test the expriment in Custom Vision website driectly.

![prediction_picture](https://user-images.githubusercontent.com/26039303/49995270-f2922080-ff8b-11e8-953e-c5b41d7d0d6a.png)


### 3. Connecting the Bot to a Facebook Messenger Channel

The most interesting thing here is that these bot servers can be connected to many different types of channels such as Skype, Teams and Facebook Messenger. We are going to connect to the last mentioned option.


![facebookchannel](https://user-images.githubusercontent.com/26039303/50036405-0760c980-0009-11e9-81cc-fb361b428223.png)


![configure_facebook](https://user-images.githubusercontent.com/26039303/50036351-991c0700-0008-11e9-93da-5ccb54fff324.png)









