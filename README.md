# Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS

## How to run?

### STEPS:

#### 1. Clone the repository
```bash
git clone https://github.com/entbappy/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS.git
```

#### 2. Create a conda environment after opening the repository
```bash
conda create -n medibot python=3.10 -y
conda activate medibot
```

#### 3. Install the requirements
```bash
pip install -r requirements.txt
```

#### 4. Create a `.env` file in the root directory and add your Pinecone & OpenAI credentials as follows:
```
PINECONE_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
OPENAI_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

#### 5. Store embeddings to Pinecone
```bash
python store_index.py
```

#### 6. Run the application
```bash
python app.py
```

Now, open up localhost in your browser.

---

## Techstack Used
- Python
- LangChain
- Flask
- GPT
- Pinecone
- AWS (CICD Deployment with Github Actions)

---

## AWS-CICD Deployment Steps

1. **Login to AWS console.**
2. **Create IAM user for deployment** (with specific access):
	- EC2 access: Virtual machine
	- ECR: Elastic Container Registry to save your docker image in AWS

### Description: About the deployment
1. Build docker image of the source code
2. Push your docker image to ECR
3. Launch your EC2
4. Pull your image from ECR in EC2
5. Launch your docker image in EC2

### Policy:
- AmazonEC2ContainerRegistryFullAccess
- AmazonEC2FullAccess

### Steps:
1. Create ECR repo to store/save docker image
	- Save the URI: `315865595366.dkr.ecr.us-east-1.amazonaws.com/medicalbot`
2. Create EC2 machine (Ubuntu)
3. Open EC2 and install docker in EC2 Machine:
	- Optional:
	  ```bash
	  sudo apt-get update -y
	  sudo apt-get upgrade
	  ```
	- Required:
	  ```bash
	  curl -fsSL https://get.docker.com -o get-docker.sh
	  sudo sh get-docker.sh
	  sudo usermod -aG docker ubuntu
	  newgrp docker
	  ```
4. Configure EC2 as self-hosted runner:
	- Go to `Settings > Actions > Runner > New self-hosted runner > Choose OS` and run the commands one by one.
5. Setup GitHub secrets:
	- `AWS_ACCESS_KEY_ID`
	- `AWS_SECRET_ACCESS_KEY`
	- `AWS_DEFAULT_REGION`
	- `ECR_REPO`
	- `PINECONE_API_KEY`
	- `OPENAI_API_KEY`

