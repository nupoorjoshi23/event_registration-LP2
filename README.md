# Online Event Registration System — MERN Stack

A full-stack MERN application for registering users for tech events. Registrations are stored in a cloud-hosted MongoDB Atlas database.

## 🏗️ Tech Stack

| Layer     | Technology                  |
| --------- | --------------------------- |
| Frontend  | React + Vite                |
| Backend   | Node.js + Express           |
| Database  | MongoDB Atlas (Cloud)       |
| Styling   | Vanilla CSS (Dark Theme)    |
| Deploy    | AWS EC2                     |

## 📁 Project Structure

```
event-registration/
├── backend/
# AWS EC2 Hosting Guide

This guide covers only the steps needed to host the app on an AWS EC2 Ubuntu instance.

## Step 1: Launch an EC2 Instance

- **AMI:** Ubuntu 22.04 LTS
- **Instance type:** t2.micro (free tier eligible)
- **Security Group Inbound Rules:**

| Type       | Port | Source    | Purpose     |
| ---------- | ---- | --------- | ----------- |
| SSH        | 22   | My IP     | SSH access  |
| Custom TCP | 5000 | 0.0.0.0/0 | App access  |

## Step 2: Connect to EC2

```bash
chmod 400 your-key.pem
ssh -i your-key.pem ubuntu@<YOUR_EC2_PUBLIC_IP>
```

## Step 3: Install Dependencies on EC2 (Node 22)

```bash
sudo apt update && sudo apt upgrade -y

# Install Node.js 22.x
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs

# Verify
node -v    # v22.x.x
npm -v

# Install Git and PM2
sudo apt install -y git
sudo npm install -g pm2
```

## Step 4: Clone the Project

```bash
cd ~
git clone <YOUR_GITHUB_REPO_URL> event-registration
cd event-registration
```

## Step 5: Configure Backend Environment

```bash
cd backend
npm install

cp .env.example .env
nano .env
```

Set only these values:

```env
PORT=5000
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/event-registration?retryWrites=true&w=majority
```

## Step 6: Build the Frontend

```bash
cd ../frontend
npm install
npm run build
```

## Step 7: Start the App with PM2

```bash
cd ../backend
pm2 start server.js --name event-registration
pm2 save
pm2 startup    # Follow the printed command to enable auto-start on reboot
```

## Step 8: Access the App

Open your browser:

```
http://<YOUR_EC2_PUBLIC_IP>:5000
```

## MongoDB Atlas Network Access

Add your EC2 public IP in MongoDB Atlas **Network Access**, or use `0.0.0.0/0` for testing.

## Optional: PM2 Commands

```bash
pm2 status
pm2 logs event-registration
pm2 restart event-registration
pm2 stop event-registration
pm2 delete event-registration
```
- Create and download your `.pem` key pair
