## AWS Alexa Lambda Hello World
Simple Java example for an Amazon Web Services Alexa Skillset Lambda function. (Extracted from alexa starter kit samples)

### Building
```
mvn clean package
```
SpeechletRequestStreamHandler implementation will have to be updated with your alexa skill application id. (THIS IS NOT REQUIRED)
Finding application id:
-	Log in to the developer portal and navigate to the Alexa section by clicking Apps & Services and then clicking Alexa in the top navigation.
-	Find the skill in the list and click Edit.
-	Click Skill Information.
-	Note the Application ID displayed on the page.
(i.e. the alexa skill will have to be created before the lambda function unless we create one without this information)

### Deploying Lambda Function
-	build the uber package/jar 
-	Follow instruction for alexa skill from here: https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/deploying-a-sample-skill-to-aws-lambda
-	Follow instructions from http://docs.aws.amazon.com/AWSToolkitEclipse/latest/ug/lambda-tutorial.html (for basic setup only not AWS explorer)
-	Go to AWS Lambda Console and create a new function
-	Skip templates
-	Provide any name and description, choose java 1.8
-	upload jar
-	Handler will be the stream handler: helloworld.HelloWorldSpeechletRequestStreamHandler
- 	Role: lambda_basic_execution (you will need to select and allow when prompted)
-	Set Event Source : Alexa Skills Kit
-	Note: Lambda functions for Alexa skills must be hosted in the US East (N. Virginia) region. Currently, this is the only Lambda region the Alexa Skills Kit supports.

### Testing the lambda function
-	Click Test (or use Actions -> configure test events) 
-	if prompted to confirm the test data then do so. Copy from src/test/resources/request.json. It will look like (we have changed the myColor test data to just include name HelloWorldIntent (other values may be redundant):
	{
	  "session": {
	    "new": false,
	    "sessionId": "session1234",
	    "attributes": {},
	    "user": {
	      "userId": null
	    },
	    "application": {
	      "applicationId": "amzn1.echo-sdk-ams.app.[unique-value-here]"
	    }
	  },
	  "version": "1.0",
	  "request": {
	    "intent": {
	      "slots": {
	        "Color": {
	          "name": "Color",
	          "value": "blue"
	        }
	      },
	      "name": "HelloWorldIntent"
	    },
	    "type": "IntentRequest",
	    "requestId": "request5678"
	  }
	}
-	click save and test

### Configuring and testing the Alexa Skill
-	Follow instructions to create a new alexa skill using AWS lamda function: https://developer.amazon.com/public/community/post/TxDJWS16KUPVKO/New-Alexa-Skills-Kit-Template-Build-a-Trivia-Skill-in-under-an-Hour
-	Use the ARN of the lambda function created above
-	Ineraction model: Copy intent schema and utterances from the json files included (Custome slot types was also included from color palette example - THIS should not be needed: LIST_OF_COLORS	green | red | blue | orange | gold | silver | yellow | black | white)
-	testing - in service simulator, type: say hello. You should get a response in Lambda Response

#### Invoking from AWS CLI
-	./invoke.sh
-	This will get the output in outputfile.txt
-	http://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html
-	NOTE this exeutes the Lambda function only from cloud (and not the local copy)

### Publishing
-	Formally Releasing the current version. Save the version ($LATEST to Version 1 or ..). This is not necessary and by default alexa will use $LATEST

### Troubleshooting
-	Check Lambda Logs if the Alexa skill ends with Remote end point error (Lambda function -> Monitoring Tab -> View logs in CloudWatch)
-	If you get error: SpeechletRequestHandlerException: Could not validate SpeechletRequest (check https://forums.developer.amazon.com/questions/5619/speechletrequesthandlerexception-could-not-validat.html). In this sample, the application id has not been provided to avoid this.



### API Reference
-	https://developer.amazon.com/public/community/post/TxDJWS16KUPVKO/New-Alexa-Skills-Kit-Template-Build-a-Trivia-Skill-in-under-an-Hour
-	https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/deploying-a-sample-skill-to-aws-lambda#Preparing%20a%20Java%20Sample%20to%20Deploy%20in%20Lambda
-	https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/handling-requests-sent-by-alexa
-	https://developer.amazon.com/public/solutions/alexa


