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

## 7-IoT-Core

**7-IoT-Core** contains the CloudFormation template to setup the IoT Core as well as dependent components, such as EC2 to simulate the IoT Sensor, etc.

###  Contents

- `7-IoT-Core/scems-IoTCore.yaml`: CloudFormation template for setting up the environment.


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
- Clone the GitHub repository that contains the `7-IoT-Core/scems-IoTCore.yaml` file to your local machine.

```
git clone https://github.com/Ashok-PUG/Smart_City-Environmental_Monitoring_System.git

cd Smart_City-Environmental_Monitoring_System/7-IoT-Core
```


**4. Deploy the CloudFormation Stack**:

- Use the AWS CLI to create a CloudFormation stack using the provided YAML template.
- Replace `YOUR_STACK_NAME` with a suitable name for your stack.

```
aws cloudformation create-stack --stack-name YOUR_STACK_NAME --template-body file://7-IoT-Core/scems-IoTCore.yaml --parameters ParameterKey=KeyName,ParameterValue=<key name>
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