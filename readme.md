## AWS Lambda using SAM
This SAM project is a simple lambda function that returns "Hello World" when invoked.

### Steps

#### 1. **Create a New Template File**

Create a new file called `template.yaml` in the root of your project. this file will contain the AWS SAM syntax in YAML format.

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Description: A starter AWS Lambda function.
Resources:
  helloworldpython3:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: app.lambda_handler
      Runtime: python3.9
      CodeUri: src/
      Description: A starter AWS Lambda function.
      MemorySize: 128
      Timeout: 3 
```

#### 2. **Create a New Folder**

Create a new folder called `src` in the root of your project. this folder will contain the source code of your lambda function.

#### 3. **Create a New File**

Create a new file called `app.py` in the `src` folder. this file will contain the source code of your lambda function.

```python
import json

def lambda_handler(event, context):
    
    return  'Hello World!'
```

#### 4. **Package**

Package the SAM template using the `sam package` command. This command will upload the local artifacts of your application to the S3 bucket you specify and output a new template that refers to the artifacts in S3.

```bash
aws cloudformation package --template-file template.yaml --s3-bucket atef-code-sam --output-template-file packaged.yaml
```

#### 5. **Deploy**

Deploy the packaged template using the `sam deploy` command. This command will create a Cloudformation Stack and deploy your SAM resources.

```bash
aws cloudformation deploy --template-file packaged.yaml --stack-name atef-sam-stack --capabilities CAPABILITY_IAM
```