# Lab For Uni - Setup Instructions

## What's Been Done
✅ Created dedicated folder on desktop: "Lab For Uni"
✅ Cloned repository: https://github.com/djnzx/iad-practice
✅ Git configured with your credentials (timurkartsan / tymur.kartsan@e-u.edu.ua)

## What You Need to Do Next

### 1. Install Docker Desktop
- Go to: https://www.docker.com/products/docker-desktop/
- Download Docker Desktop for Windows
- Install with administrator privileges
- Restart your computer if prompted
- Start Docker Desktop

### 2. After Docker is Installed
Once Docker is running, I'll help you with:
- Building the Jupyter notebook Docker container
- Starting the container
- Running the code
- Committing results to your GitHub repository

### 3. GitHub Repository
You'll also need to manually create the GitHub repository:
- Go to https://github.com/timurkartsan
- Create a new repository named: "Lab For Uni"
- Make it public
- Don't initialize with README (we already have files)

## Repository Structure
```
Lab For Uni/
├── README.md (this file)
├── iad-practice/ (cloned repository)
│   ├── dev-env/ (Docker setup)
│   │   ├── docker-compose.yml
│   │   ├── Dockerfile
│   │   └── Makefile
│   └── practice/ (Jupyter notebooks)
└── .git/ (your Lab For Uni repository)
```

## Next Steps After Docker Installation
Run these commands in PowerShell from the "Lab For Uni" folder:

```bash
cd iad-practice/dev-env
docker compose build
docker compose up -d
```

Then access Jupyter at: http://localhost:8888