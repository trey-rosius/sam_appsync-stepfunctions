# Building a Step Functions Workflow With SAM ,Appsync and Python.

[https://github.com/trey-rosius/sam_stepfunctions](https://github.com/trey-rosius/sam_stepfunctions)

Hey there, welcome to the 3rd Scenario in “Building a Step Functions Workflow “

In the first part of this series, we built a step functions workflow for a simple apartment booking scenario using the AWS Step functions low code visual editor.

In the second part of this series, we built the same workflow using CDK as IaC, Appsync and python, while invoking the step functions execution from a Lambda function.

In this post, we’ll look at how to build the same workflow, using SAM as IaC, Appsync and python.

# Prerequisite

- Install AWS Cli ([https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html))
- Install AWS SAM CLI([https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html))
- AWS Account
- Any IDE of your choice. I use PyCharm
- Install python 3.8

### Assumption

In this post, we won’t be looking at SAM basics .So I’ll assume you’ve worked with  SAM before.

If i’m wrong, I apologize. Please level up with these articles

[https://phatrabbitapps.com/building-modern-serverless-apis-with-aws-dynamodb-lambda-and-api-gatewaypart-3](https://phatrabbitapps.com/building-modern-serverless-apis-with-aws-dynamodb-lambda-and-api-gatewaypart-3)

https://github.com/aws/aws-sam-cli-app-templates

## Problem Statement

What are we trying to solve ? 

So while building out a bigger system(Apartment Complex Management System) i came across an interesting problem. 

I’ll assume that, most of us have reserved or booked either an apartment or hotel or flight online.

For this scenario, let’s go with apartments. So when you reserve an apartment, here’s a breakdown in the most simplest form, of the series of steps that occur after that

- The apartment  is marked as reserved, probably with a status change.Let’s say the apartment status changes from **vacant** to reserved.
- This apartment is made unavailable for reserving by others, for a particular period of time.
- The client is required to make payment within that period of time
- If payment isn’t made within that time, the reservation is cancelled, and the apartment status changes back from reserved to **vacant .**
- If payment is made, then apartment status changes from reserved to occupied/paid

Building out this business logic using custom code is very possible, but inefficient. 

Why ?

Because as developers, good ones for that matter, we always have to be on the lookout for tools that’ll help us carryout tasks in an efficient and scalable manner.

The series of steps  outlined above, serve as a good use case for aws step functions.

- The sequence of service interaction is important
- State has to be managed with AWS service calls
- Decision trees, retries and error handling logic are required.

# Solutions Architecture

![alt text](https://raw.githubusercontent.com/trey-rosius/sam_stepfunctions/master/assets/sol_arch.png)
Let me quarterback this entire architecture for you please. Here’s what’s happening.

- A frontend application sends a mutation to Appsync.
- A Lambda resolver is invoked by Appsync, based on that mutation.
- Lambda gets the input from the mutation and starts a step functions workflow based on the input.

We’ll use Flutter and Amplify to build out the frontend application in the next tutorial.

### Create And Initialize a SAM Application

Open any Terminal/Command line interface and type in the command `sam init`. 






![alt text](https://raw.githubusercontent.com/trey-rosius/sam_stepfunctions/master/assets/apartment_studio.jpeg)
![alt text](https://raw.githubusercontent.com/trey-rosius/sam_stepfunctions/master/assets/stepfunctions_graph.png)
![alt text](https://raw.githubusercontent.com/trey-rosius/sam_stepfunctions/master/assets/success.png)

