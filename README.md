# Task-03:
# React-project

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app) and features a complete CI/CD pipeline with Docker containerization and automated deployment to AWS EC2.

## Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Branch Strategy](#branch-strategy)
- [CI/CD Pipeline](#cicd-pipeline)
- [Deployment](#deployment)
- [Getting Started](#getting-started)
- [Available Scripts](#available-scripts)
- [Learn More](#learn-more)

## Overview

A React application with enterprise-grade DevOps practices including automated testing, Docker containerization, and multi-environment deployment strategy.

## Tech Stack

- **Frontend**: React
- **Containerization**: Docker
- **CI/CD**: GitHub Actions
- **Hosting**: AWS EC2
- **Registry**: Docker Registry

## Architecture

The application follows a three-tier deployment architecture:

```
Feature Branch → Staging Environment → Production Environment
     ↓                    ↓                      ↓
  Feature-1            Staging EC2            Main EC2
```

## Branch Strategy

This project implements a GitFlow-inspired branching model with three main branches:

### 1. `main` Branch
- **Production environment**
- Represents the live application
- Protected branch with PR requirements
- Automated deployment to production EC2 instance

### 2. `staging` Branch
- **Staging/Pre-production environment**
- Testing ground before production
- Deployed to separate staging EC2 instance
- Protected branch with PR requirements

### 3. `feature-1` Branch
- **Development branch**
- Used for developing new features
- Merged to staging via Pull Request for testing
  
### Workflow

1. **Feature Development**: Work on `feature-1` branch
2. **Staging Review**: Create PR from `feature-1` → `staging`
3. **Staging Testing**: Automated deployment to staging EC2
4. **Production Release**: Create PR from `staging` → `main`
5. **Production Deployment**: Automated deployment to production EC2

## CI/CD Pipeline

### GitHub Actions Workflow

The project uses GitHub Actions for automated CI/CD with the following steps:

1. **Code Checkout**: Pull latest code from repository
2. **Dependency Installation**: Run `npm install`
3. **Build Application**: Create production build
4. **Run Tests**: Execute test suite
5. **Docker Image Creation**: Build Docker image
6. **Push to Registry**: Upload image to Docker registry
7. **Deploy to EC2**: Pull image on EC2 and run container

### Deployment Triggers

- **Staging**: Automatically deploys when code is merged to `staging` branch
- **Production**: Automatically deploys when code is merged to `main` branch

### Environment Configuration

Each environment (staging and production) has:
- Dedicated EC2 instance
- Separate GitHub Actions workflow
- Independent Docker containers
- Environment-specific configurations

## Deployment

### Prerequisites

- AWS EC2 instances (staging and production)
- Docker installed on EC2 instances
- Docker registry access
- GitHub repository secrets configured

### EC2 Setup

1. Launch EC2 instances for staging and production
2. Install Docker on both instances
3. Configure security groups for required ports
4. Set up SSH access for GitHub Actions

### GitHub Secrets

Configure the following secrets in your GitHub repository:

```
AWS_HOST
AWS_HOST_STAGING
AWS_PEM_KEY
AWS_USERNAME
DOCKERPASS
DOCKERUSER
```

## Getting Started

### Local Development

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd <project-directory>
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm start
   ```

4. **Open your browser**
   Navigate to [http://localhost:3000](http://localhost:3000)

### Docker Development

1. **Build Docker image**
   ```bash
   docker build -t <image-name> .
   ```

2. **Run container**
   ```bash
   docker run -p 3000:3000 <image-name>
   ```

## Available Scripts

### `npm start`

Runs the app in development mode.  
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.  
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in interactive watch mode.  
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.  
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.  
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

## Learn More

### Create React App Documentation

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Additional Resources

- [Code Splitting](https://facebook.github.io/create-react-app/docs/code-splitting)
- [Analyzing the Bundle Size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)
- [Making a Progressive Web App](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)
- [Advanced Configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)
- [Deployment](https://facebook.github.io/create-react-app/docs/deployment)
- [Troubleshooting: `npm run build` fails to minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)

## Drive_link:
**https://drive.google.com/drive/folders/163WfSB_k15tXuQPfoNNWNRHMcdiFs9Js**
## Contributing

1. Create a feature branch from `staging`
2. Make your changes
3. Create a Pull Request to `staging`
4. Wait for automated tests to pass
5. Get approval from maintainers
6. Merge to staging for testing
7. After validation, create PR from `staging` to `main`
