**Project Name: Holy-Polly!**  
Text to speech conversion using Amazon Polly.    

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/Polly%20Architecture.jpg)  


**AWS Resources:**    

&nbsp;&nbsp;&nbsp;&nbsp;1. S3 Bucket: This stores table data and has event notifications enabled.  
&nbsp;&nbsp;&nbsp;&nbsp;2. Lambda Function: Acts as an Audio Processor for this project  
&nbsp;&nbsp;&nbsp;&nbsp;3. IAM policy for permission: Policy that allows read from the source bucket and write to the destination bucket. This policy &nbsp;&nbsp;&nbsp;&nbsp;must also include permission that allows text to speech conversion done by Amazon Polly.  
&nbsp;&nbsp;&nbsp;&nbsp;4. IAM Role: This role will be assumed by the Lambda function.  

  
**Walk-through Holy-Polly! Project**  
  
•	**Create two S3 Buckets**, one for uploading text file (merina-source-bucket) and another for saving audio file (merina-destination-bucket), disable public access.    

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/s3%20buckets.jpg)     

•	**Create Lambda Function** (holly-polly-lambda-function) which acts as an audio processor. Python is used to write this function.    

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/Create%20Function.jpg)    

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/Lambda%20Function%20Code%20Snippet.jpg)    

 
•	**Set up event notification** in the source S3 bucket to trigger the lambda function when any new upload (with .txt suffix) is made.   

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/1%20event%20notification.jpg)   

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/2%20event%20notification%20.jpg)  

![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/3%20event%20notification%20.jpg)  




•	**IAM Permission and Roles:**    

  &nbsp;&nbsp;&nbsp;&nbsp; o Creating an **IAM Policy** (s3-lambda-polly-policy) with Permissions on Amazon S3 and Amazon Polly. I used policy generator to generate this policy.    
  
  ![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/IAM%20Permission%201.jpg)    
  
  ![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/IAM%20policy.jpg) 
  
  

  &nbsp;&nbsp;&nbsp;&nbsp; o	Create an **IAM Role for Lambda function** (s3-lambda-polly-role) and attach s3-lambda-polly-policy and AWSLambdaBasicExecutionRole-ab9d54b9-a4e1-4153-94e5-88d779f61335 (this is created by default when triggered is added to Lambda or you may opt to choose from the AWS managed policies for the same)      
  
 ![image alt](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/IAM%20Role.jpg)     
 
 
•	**Test the system** by uploading .txt file to the source bucket and receive audio file in destination bucket.

 &nbsp;&nbsp;&nbsp;&nbsp;Source bucket uploaded text file
![Alt text](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/Uploaded%20text%20file.jpg)


 &nbsp;&nbsp;&nbsp;&nbsp;Destination bucket saves .mp3 file
![Alt text](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/saved%20Audio%20File%20.jpg)


•	**Make a good habit of monitoring through Amazon CloudWatch.**  
CloudWatch Log
![Alt text](https://github.com/merina-poudyal/Holy-Poly-/blob/master/Polly%20Images/CloudWatch%20Log.jpg)

