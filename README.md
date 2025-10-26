## Setup Instructions (Local Development)

1. **Clone the repository:**
```bash
git clone https://github.com/triptijain07/MyShop.git
cd MyShop
Install dependencies:

bash
Copy code
npm ci
Create a .env file (copy from sample_ENV_file.txt) and fill in your credentials:

env
Copy code
MONGODB_URL="mongodb+srv://<username>:<password>@cluster0.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0"
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your_secret"
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME="Root"
NEXT_PUBLIC_CLOUDINARY_API_KEY="YOUR_API_KEY"
CLOUDINARY_SECRET="YOUR_CLOUD_SECRET"
Run the app locally:

bash
Copy code
npm run dev
Docker Setup
Build the Docker image:

bash
Copy code
docker build -t myshop:latest .
Run the container with environment variables:

bash
Copy code
docker run -d -p 3000:3000 --name myshop --env-file .env myshop:latest
Check container logs:

bash
Copy code
docker logs myshop
CI/CD with GitHub Actions
Workflow file: .github/workflows/deploy.yml

Trigger: On push to main branch

Workflow Steps:
Checkout repository

Setup Node.js

Install dependencies

Build Next.js app

Log in to Docker Hub

Build and push Docker image

SSH into EC2 instance and deploy container

Secrets used in GitHub Actions
Secret Name	Description
DOCKERHUB_USERNAME	Docker Hub username
DOCKERHUB_TOKEN	Docker Hub access token
EC2_HOST	EC2 public IP
EC2_SSH_KEY	EC2 private key (.pem)
MONGODB_URL	MongoDB Atlas connection URL
NEXTAUTH_URL	App URL
NEXTAUTH_SECRET	NextAuth secret
CLOUD_NAME	Cloudinary cloud name
CLOUD_API_KEY	Cloudinary API key
CLOUD_SECRET	Cloudinary secret key

Deployment Steps
Push changes to main branch:

bash
Copy code
git add .
git commit -m "Your commit message"
git push origin main
GitHub Actions workflow will automatically:

Build Docker image

Push to Docker Hub

SSH into EC2

Pull latest image and run container

Access the app in browser:

cpp
Copy code
http://<EC2_PUBLIC_IP>:3000

Notes
Never commit .env or any secrets to the repository

Use GitHub Actions secrets for production deployments

Always rebuild the Docker image after dependency changes


