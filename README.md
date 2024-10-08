# Smart_City-Environmental_Monitoring_System

## 3-EC2-IoT

**3-EC2-IoT** contains the CloudFormation template to setup EC2 to simulate IoT Sensor and IoT Core, as well as dependent components.

###  Contents

- `3-EC2-IoT/Smart_City_Environment-EC2-to-IoTCore.yaml`: CloudFormation template for setting up the environment.


###  Prerequisites

Before you can create the stack using the provided CloudFormation template, ensure you have the following:

- [x]  **AWS Account:** An active AWS account.
- [x]  **IAM User:** An IAM user with sufficient permissions to create the required resources (VPC, EC2, IoT, etc.).
- [x]  **AWS CLI:** Installed and configured on your local machine.
- [x] **EC2 Key Pair:** A key pair for accessing the EC2 instance.

###  Deployment Instructions

**1. Configure AWS CLI**:
- If not already installed, download and install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
- Configure the AWS CLI with your AWS access keys and set the region to us-east-1.


```
aws configure
```
`AWS Access Key ID []: <Access key>`

`AWS Secret Access Key []: <Secret access key>`

`Default region name []: <Region>`

`Default output format []: <text, json, table>`


**2. Create a Key Pair for EC2**:
- Create a Key Pair to enable SSH access to the EC2 instance. Save the key pair to your local machine.

```
aws ec2 create-key-pair --key-name <key name> --key-type rsa --key-format pem --query "KeyMaterial" --output text > <key-pair pem file name>.pem
```
**3. Clone the GitHub Repository**:
- Clone the GitHub repository that contains the `Smart_City_Environment-EC2-to-IoTCore.yaml` file to your local machine.

```
git clone https://github.com/Ashok-PUG/Smart_City-Environmental_Monitoring_System.git

cd Smart_City-Environmental_Monitoring_System/3-EC2-IoT
```


**4. Deploy the CloudFormation Stack**:

- Use the AWS CLI to create a CloudFormation stack using the provided YAML template.
- Replace `YOUR_STACK_NAME` with a suitable name for your stack.

```
aws cloudformation create-stack --stack-name YOUR_STACK_NAME --template-body file://Smart_City_Environment-EC2-to-IoTCore.yaml --parameters ParameterKey=KeyName,ParameterValue=<key name>
```

### Testing the Deployment:

1. After the stack is successfully created, you can SSH into the EC2 instance using the public DNS provided in the CloudFormation stack outputs.

2. Verify that the `EnvironmentalSensor1` service is running and the ***MQTT*** topic subscription using the **AWS IoT Core** console.

- MQTT Test:
  - `AWS IoT Core Dashboard`
    - Test
      - MQTT Test Client
        - Subscibe to a topic
          - Filer: `environmental/sensor`
           - Subscribe



##
***Note***: Hereafter, **Smart_City-Environmental_Monitoring_System** will be abbreviated as **scems** for short.
##

## IoT-Core

**IoT-Core** contains the CloudFormation template to setup the IoT Core as well as dependent components, such as EC2 to simulate the IoT Sensor, etc.

###  Contents

- `IoT-Core/scems-IoTCore.yaml`: CloudFormation template for setting up the environment.


###  Prerequisites

Before you can create the stack using the provided CloudFormation template, ensure you have the following:

- [x]  **AWS Account:** An active AWS account.
- [x]  **IAM User:** An IAM user with sufficient permissions to create the required resources (VPC, EC2, IoT, etc.).
- [x]  **AWS CLI:** Installed and configured on your local machine.
- [x] **EC2 Key Pair:** A key pair for accessing the EC2 instance.

###  Deployment Instructions

**1. Configure AWS CLI**:
- If not already installed, download and install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
- Configure the AWS CLI with your AWS access keys and set the region to us-east-1.


```
aws configure
```
`AWS Access Key ID []: <Access key>`

`AWS Secret Access Key []: <Secret access key>`

`Default region name []: <Region>`

`Default output format []: <text, json, table>`


**2. Create a Key Pair for EC2**:
- Create a Key Pair to enable SSH access to the EC2 instance. Save the key pair to your local machine.

```
aws ec2 create-key-pair --key-name <key name> --key-type rsa --key-format pem --query "KeyMaterial" --output text > <key-pair pem file name>.pem
```
**3. Clone the GitHub Repository**:
- Clone the GitHub repository that contains the `IoT-Core/scems-IoTCore.yaml` file to your local machine.

```
git clone https://github.com/Ashok-PUG/Smart_City-Environmental_Monitoring_System.git

cd Smart_City-Environmental_Monitoring_System/IoT-Core
```


**4. Deploy the CloudFormation Stack**:

- Use the AWS CLI to create a CloudFormation stack using the provided YAML template.
- Replace `YOUR_STACK_NAME` with a suitable name for your stack.
- Replace `<key name>` with your `KEY-PAIR` name (as mentioned above at point number 2).

```
aws cloudformation create-stack --stack-name YOUR_STACK_NAME --template-body file://scems-IoTCore.yaml --parameters ParameterKey=KeyName,ParameterValue=<key name> --capabilities CAPABILITY_NAMED_IAM
```

### Testing the Deployment:

1. After the stack is successfully created, you can SSH into the EC2 instance using the public DNS or IP address provided in the CloudFormation stack outputs.

2. Verify that the `EnvironmentalSensor1` service is running and the ***MQTT*** topic subscription using the **AWS IoT Core** console.

- MQTT Test:
  - `AWS IoT Core Dashboard`
    - Test
      - MQTT Test Client
        - Subscibe to a topic
          - Filer: `environmental/sensor`
           - Subscribe



## Timestream (Amazon Timestream: A Time Series Database)

**TimeStream** comprises a CloudFormation template that establishes the Amazon TimeStream, a time series database, along with its dependent components. These components include an EC2 for simulating an IoT sensor, an IoT-Core, and a Lambda function for writing published data from the IoT-Core into TimeStream, etc.

###  Contents

- `Timestream/scems-TimeStream.yaml`: CloudFormation template for setting up the environment.


###  Prerequisites

Before you can create the stack using the provided CloudFormation template, ensure you have the following:

- [x]  **AWS Account:** An active AWS account.
- [x]  **IAM User:** An IAM user with sufficient permissions to create the required resources (VPC, EC2, IoT, etc.).
- [x]  **AWS CLI:** Installed and configured on your local machine.
- [x] **EC2 Key Pair:** A key pair for accessing the EC2 instance.

###  Deployment Instructions

**1. Configure AWS CLI**:
- If not already installed, download and install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
- Configure the AWS CLI with your AWS access keys and set the region to us-east-1.


```
aws configure
```
`AWS Access Key ID []: <Access key>`

`AWS Secret Access Key []: <Secret access key>`

`Default region name []: <Region>`

`Default output format []: <text, json, table>`


**2. Create a Key Pair for EC2**:
- Create a Key Pair to enable SSH access to the EC2 instance. Save the key pair to your local machine.

```
aws ec2 create-key-pair --key-name <key name> --key-type rsa --key-format pem --query "KeyMaterial" --output text > <key-pair pem file name>.pem
```
**3. Clone the GitHub Repository**:
- Clone the GitHub repository that contains the `Timestream/scems-TimeStream.yaml` file to your local machine.

```
git clone https://github.com/Ashok-PUG/Smart_City-Environmental_Monitoring_System.git

cd Smart_City-Environmental_Monitoring_System/Timestream
```


**4. Deploy the CloudFormation Stack**:

- Use the AWS CLI to create a CloudFormation stack using the provided YAML template.
- Replace `YOUR_STACK_NAME` with a suitable name for your stack.
- Replace `<key name>` with your `KEY-PAIR` name (as mentioned above at point number 2).

```
aws cloudformation create-stack --stack-name YOUR_STACK_NAME --template-body file://scems-TimeStream.yaml --parameters ParameterKey=KeyName,ParameterValue=<key name> --capabilities CAPABILITY_NAMED_IAM
```

### Testing the Deployment:

1. After the stack is successfully created, you can SSH into the EC2 instance using the public DNS or IP address provided in the CloudFormation stack outputs.

2. Verify that the `EnvironmentalSensor1` service is running and the ***MQTT*** topic subscription using the **AWS IoT Core** console.

3. Run a query against Amazon Timestream data:
  - `AWS Timestream Core Dashboard`
    - Query editor
      - In the left pane, select the database and table
        - In the query editor, run a query with the following query string:
          ```
          SELECT * FROM <database_name>.<table_name> ORDER BY time DESC LIMIT 10
          ```
        - Example:
          ```
          SELECT * FROM "EnvironmentalMonitoring"."SensorData" ORDER BY time DESC LIMIT 10
          ```



## ECS-FARGATE (Amazon Elastic Container Service - Launch Type: FARGATE )

**ECS-FARGATE** comprises a CloudFormation template and other dependent files to setup the whole environment, such as ECS, CI/CD, load balancer, and above Timestream, etc.

###  Contents

1. `ECS-FARGATE/scems-ecs.yaml`: The cloud formation template establishes the entire environment. including:

- **ECR**: Container Image Rigistry
- **ECS**: ECS Cluster, a service with a launch type called Fargate
- **Load Balancer**: Application Load Balancer
- **Pipeline**: CodeBuild, CodeDeploy
- And above EC2, IoT-Core, Timestream.

2. `ECS-FARGATE/Application-Files/Docker`: Contains the files to build the Docker image.
    - The default *app.py* in the *Docker* is from the *version 1* image in *ECS-FARGATE/Application-Files/Flask/v1*.

3. `ECS-FARGATE/Application-Files/Flask`: Contains the version 1, version 2, and version 3 Flask application files. 

4. `ECS-FARGATE/CI-CD/CodeBuild/buildspec.yml`: The file used by **CodeBuild** to build the ***Docker image*** and push it to ***ECR***.

5. `ECS-FARGATE/CI-CD/CodeDeploy/imagedefinitions.json`: The file used by **CodeDeploy** to retrieve the ***Docker image*** from the ***ECR*** and to deploy it in the in the ***ECS***.


###  Prerequisites

Before you can create the stack using the provided CloudFormation template, ensure you have the following:

- [x]  **AWS Account:** An active AWS account.
- [x]  **IAM User:** An IAM user with sufficient permissions to create the required resources (VPC, EC2, IoT, etc.).
- [x]  **AWS CLI:** Installed and configured on your local machine.
- [x] **EC2 Key Pair:** A key pair for accessing the EC2 instance.
- [x] **CodeCommit:** A CodeCommit repository is created, and application files and CI/CD files are pushed to the repository.

###  Deployment Instructions

- ***Updating***

### Testing the Deployment:

- ***Updating***
