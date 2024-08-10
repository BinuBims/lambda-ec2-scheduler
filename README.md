<h2>Schedule Your EC2 with Lambda and EventBridge</h2>

### ARCHITECTURE
<p align="center">
<img src="data/images/diagram.JPEG"  height="400" width="600" />
</p>

### AWS services and Tools
* EC2
* Lambda (Python)
* EventBridge

### Steps taken to implement this architecture
1. Create an EC2 instance.
2. Create an IAM policy and IAM role specifically for Lambda.
3. Write a Lambda function to stop the EC2 instance.
4. Write a Lambda function to start the EC2 instance.
5. Set up two separate events in EventBridge to trigger these Lambda functions.

## 1. Create an EC2 instance.
* Search for "EC2" in the search bar.
* Go to Instances > Launch instances.
* Name your EC2 instance.
* Select Ubuntu as your OS.
* Choose Proceed without a key pair (you do not need a key pair).
* Leave everything else as default.
* Click Launch instance.

## 2. Create an IAM policy and IAM role specifically for Lambda.
* Search for "IAM" in the AWS search bar.
* Select "Policies" from the left-hand menu.
* Click "Create policy".
* Switch from the "Visual" editor to the "JSON" editor.
* Replace the existing code with the provided JSON code below.
* Click "Next".
* Name your policy.
* Click "Create policy".
  
            {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "logs:CreateLogGroup",
                      "logs:CreateLogStream",
                      "logs:PutLogEvents"
                  ],
                  "Resource": "arn:aws:logs:*:*:*"
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "ec2:Start*",
                      "ec2:Stop*"
                  ],
                  "Resource": "*"
              }
          ]
      }



