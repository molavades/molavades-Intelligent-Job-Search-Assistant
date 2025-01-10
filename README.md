# Intelligent Job Search Assistant

[![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=apache-airflow&logoColor=white)](https://airflow.apache.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white)](https://www.snowflake.com/)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3-FF9900?style=for-the-badge&logo=amazons3&logoColor=white)
[![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com)
[![LangChain](https://img.shields.io/badge/🦜️_LangChain-008080?style=for-the-badge&logo=chainlink&logoColor=white)](https://github.com/langchain-ai/langchain)
[![LangGraph](https://img.shields.io/badge/LangGraph-FF6F61?style=for-the-badge&logo=graph&logoColor=white)](https://github.com/langchain-ai/langgraph)
![Poetry](https://img.shields.io/badge/Poetry-%233B82F6.svg?style=for-the-badge&logo=poetry&logoColor=0B3D8D)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)
[![GitHub Actions](https://img.shields.io/badge/Github%20Actions-282a2e?style=for-the-badge&logo=githubactions&logoColor=367cfe)](https://github.com/features/actions)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
![Google Cloud](https://img.shields.io/badge/GoogleCloud-%234285F4.svg?style=for-the-badge&logo=google-cloud&logoColor=white)

---
# Introduction

Navigating the competitive job market can be overwhelming, with candidates often struggling to identify relevant opportunities and optimize their application materials for specific roles. Traditional job boards provide limited options, while tailoring resumes and cover letters for individual job descriptions is time-consuming and subjective. This project introduces an intelligent system that expands job searches across multiple sources and provides actionable insights to improve profile optimization, enhancing job-seeking efficiency and success rates.

The **Intelligent Job Search Assistant** aims to simplify and enhance the job application process by offering:

- Access to the latest job opportunities aggregated from multiple sources via the Google SERP API.
- Real-time feedback on the relevance of selected jobs to the user's resume and cover letter.
- Actionable suggestions to tailor application materials for specific roles, increasing the chances of getting shortlisted.

---

# Project Overview

The **Intelligent Job Search Assistant** provides a comprehensive suite of features to support users throughout their job search journey:

1. **Job Data Collection**: Aggregates job listings from multiple sources using Google SERP API and stores them in Snowflake.
2. **User Management**: Facilitates user sign-up, login, and profile management, including resume and cover letter uploads.
3. **Job Search and Filtering**: Allows users to search for jobs by role and view detailed job information.
4. **Application Assistance**: Uses AI to provide feedback on resume and cover letter relevance to specific job descriptions.
5. **Job Tracking**: Enables users to save jobs, track application statuses, and mark applications as submitted.
6. **Analytics**: Offers insights into the user's job search process through descriptive statistics and visualizations.

---
# Problem Statement 

Job seekers currently face several critical challenges in their job search process:

### Limited Job Discovery
- Restricted access to opportunities across multiple platforms
- Difficulty in finding relevant positions matching their skills
- Time-consuming manual searches across different job boards

### Application Material Optimization
- Lack of real-time feedback on resume and cover letter effectiveness
- Challenge in tailoring documents to specific job requirements
- No standardized way to measure application material relevance

### Application Management
- Loss of job details after listings are removed from original sources
- Inefficient tracking of multiple job applications
- No centralized system for managing application statuses

### Feedback and Analytics Gap
- Absence of data-driven insights into application performance
- No visibility into success patterns and areas for improvement
- Limited understanding of job market trends

---

# Desired Outcome

Our solution aims to deliver a comprehensive platform offering:

### Core Features
- Aggregated job listings from multiple sources via **Google SERP API integration**
- AI-powered analysis of resumes and cover letters using **OpenAI** and **LangChain**
- Natural language job search capabilities through **SQL Agent**
- Secure document storage in **AWS S3** and structured data in **Snowflake**
- Real-time application tracking and status management

### Advanced Capabilities
- Personalized feedback system for application optimization
- Analytics dashboard for tracking application metrics
- **JWT token-based authentication** for secure access
- **Docker-containerized deployment** on **GCP VM**

---
# Architecture Diagram
![image](https://github.com/user-attachments/assets/1dbf9f88-b5b9-4186-a3f6-ef7b1591d211)

## Application Workflow Diagram
Below is a representation of the data flow and application workflow within the system:

```mermaid
graph TD
    %% Data Flow %%
    subgraph Data Flow
        A[Google Jobs Scraping via Google SERP API] --> B[Preprocessing and Transformations]
        B --> C[Airflow]
        C --> Cd[Load Data into Snowflake Database]
    end

    %% Application Flow %%
    subgraph Application Flow
        Login_Signup --> D[Login or Signup]
        D -->|Signup| E[Save User Details to Snowflake Users Database, Resume and Cover Letter to S3]
        D -->|Login| G[Authenticate with JWT Token]
        
        G --> H[User Logged In]
        
        H --> I[User Asks for Jobs in Natural Language]
        I --> J[SQL Agent Writes SQL Query in the Backend]
        J --> K[Retrieve Jobs Data from Snowflake Job Listings Database]
        K --> L[Display Job Listings Data to User]
        L --> R[Set Job Status as Applied]

        L --> M[User Selects Particular Job to Save]
        M --> N[Saves Selected Job Details in Snowflake Saved Jobs DB]

        H --> OO[View Saved Jobs from Snowflake Saved Jobs DB]
        OO --> FF[Set Job Status as Applied]
        OO --> GG[Check Relevance with Profile and Save Feedback and Job Details in Snowflake Results DB]

        L --> P[Check Selected Job Relevance with Profile]
        P --> PQ[Sends Job Description Along with Resume and Cover Letter to OpenAI for Structured Feedback]
        PQ --> Q[Save Feedback and Job Details in Snowflake Results DB]

        R --> S[Save Status in Snowflake Results DB]

        H --> T[Analytics Option]
        T --> U[Analytics for the Applied Jobs from Snowflake Results DB]
    end



## Application Screenshots

### Homepage / Landing Page
The landing page introduces users to the **Intelligent Job Search Assistant** platform, highlighting key features:
- Natural language job search
- AI-powered profile matching
- Application tracking
![image](https://github.com/user-attachments/assets/19f486c3-8b90-49d3-86b7-33934a6cf9b7)

Users can:
- **Sign in** or **Create a New Account**
- Access the four main sections after authentication:
  1. **Intelligent Job Search**: Natural language job search interface
  2. **Saved Jobs**
  3. **Application Materials**
  4. **User Analytics**
- **Job Listings Analytics**

---

### Login / Signup Page
A dual-purpose authentication page where:
- Existing users can log in using their credentials.
- New users can switch to the signup form to create an account.
![image](https://github.com/user-attachments/assets/e56d28ed-193f-4cb6-a9ec-1e5509cd946a)

**Security**: Features **JWT token-based authentication** for secure access.

---

### User Registration Page
New users can:
- Create their account by providing personal details.
- Upload their **resume** and **cover letter** in PDF format.
![image](https://github.com/user-attachments/assets/9b644d30-08e8-4f11-a2a7-24a091d75a02)

**Storage**:
- Documents are securely stored in **AWS S3**.
- User details are saved in the **Snowflake database**.

---

### Job Search Results Page
Displays job listings retrieved from **Snowflake** based on the user's natural language query.
![image](https://github.com/user-attachments/assets/d5e8bbfd-10d9-4607-9dd6-c46c318e391f)

---

### Job Details View
A detailed view of selected jobs, including:
- Complete job description
- Company information
- Application link
- Option to **Save the Job**
![image](https://github.com/user-attachments/assets/06dbf28c-a0ae-40c2-8f2d-bf0cf60f2bd5)

---

### Saved Jobs Page
Manage all saved jobs with options to:
- View job details
- Generate feedback
- Update application progress
- **Delete a Job** if no longer needed
![image](https://github.com/user-attachments/assets/3d87d58e-ef95-43b6-8665-0aa8c97c2b79)

---

### Profile Relevance Page
- Shows AI-powered analysis comparing the user's resume and cover letter with the selected job description.
- Provides **structured feedback** for optimization.
![image](https://github.com/user-attachments/assets/af2911fc-5f23-4068-898d-1bcc4dab32ee)
![image](https://github.com/user-attachments/assets/792057ce-82b4-414c-a437-f1593a386f03)

---

### Application Materials
Manage and update application-related documents such as resumes and cover letters.
![image](https://github.com/user-attachments/assets/be5c5427-9c75-4c6c-98ef-3ec0998031ce)

---

### User Analytics
Visual representation of the user's job search journey, including:
- Application statistics
- Job search trends
- Profile performance metrics
![image](https://github.com/user-attachments/assets/8638c7bb-038c-4b38-a272-ddb5cd92af4f)

---

# Project Tree
```
├── Airflow
│   ├── config
│   ├── dags
│   │   ├── jobs_data_dag.py
│   │   ├── multijob_transformed.py
│   │   └── upload_table.py
│   ├── docker-compose.yaml
│   ├── dockerfile
│   ├── poetry.lock
│   └── pyproject.toml
├── FastAPI_Services
│   ├── Dockerfile
│   └── main.py
├── LICENSE
├── PoC
│   ├── DataAcq_PoC.ipynb
│   ├── jobserp.py
│   ├── jobserp_multijob.py
│   ├── jobserp_multijob_dated.py
│   ├── software_engineer_jobs.csv
│   ├── software_engineer_jobs.json
│   ├── sql_agent.ipynb
│   ├── sql_agent_poc.ipynb
│   ├── tech_jobs.csv
│   └── tech_jobs.json
├── README.md
├── Streamlit_UI_App
│   ├── Dockerfile
│   ├── Home.py
│   ├── pages
│   │   ├── 1_🔑Login_Signup.py
│   │   ├── 2_🔍 Intelligent_Job_Search.py
│   │   ├── 3_📂Saved_Jobs.py
│   │   ├── 4_📄Application_Materials.py
│   │   ├── 5_📊User_Analytics.py
│   │   └── 6_📋Job_Listings_Analytics.py
│   └── utils.py
├── diagrams
│   ├── Agents_diag.py
│   ├── Final_proj_diag.py
│   ├── airflow_icon.png
│   ├── arxiv_icon.png
│   ├── cfa_icon.png
│   ├── docker_icon.png
│   ├── docling_ico.png
│   ├── docling_icon.png
│   ├── fastapi_icon.png
│   ├── google_jobs_icon.png
│   ├── google_search_icon.jpg
│   ├── intelligent_job_search_assistant_architecture.png
│   ├── job_assistant_architecture.png
│   ├── langgraph_icon.png
│   ├── openai_icon.png
│   ├── pinecone_icon.png
│   ├── rag_icon.png
│   ├── selenium_icon.png
│   ├── serp_icon.png
│   ├── snowflake_icon.png
│   ├── streamlit_icon.png
│   └── updated_research_assistant_system.png
├── docker-compose.yml
├── poetry.lock
├── project-tree.txt
├── pyproject.toml
└── tests
    ├── __init__.py
    ├── pytest.ini
    ├── test_integration.py
    └── test_unit.py
```

---
# Instructions for Setting Up the Data Pipeline and Application Services Locally

## Prerequisites
Ensure the following tools are installed:
- **Python 3.12.7**
- **Poetry** for dependency management
- **Docker** and **Docker Compose** or the **Docker** desktop app for containerization

## Required Environment Variables
Create a `.env` file in the root directory and populate it with the following keys:

```plaintext
# OpenAI API Key
OPENAI_API_KEY=<your_openai_api_key>

# SERP API Key
SERP_API_KEY=<your_serp_api_key>

# Snowflake Database Configuration
SNOWFLAKE_ACCOUNT=<your_snowflake_account>
SNOWFLAKE_USER=<your_snowflake_user>
SNOWFLAKE_PASSWORD=<your_snowflake_password>
SNOWFLAKE_JOBSDB=<your_jobs_database>
SNOWFLAKE_USER_PROFILES_DB=<your_user_profiles_database>
SNOWFLAKE_USER_RESULTS_DB=<your_user_results_database>
SNOWFLAKE_SCHEMA=<your_snowflake_schema>
SNOWFLAKE_WAREHOUSE=<your_snowflake_warehouse>

# AWS S3 Configuration
AWS_ACCESS_KEY_ID=<your_aws_access_key>
AWS_SECRET_ACCESS_KEY=<your_aws_secret_access_key>
AWS_REGION=<your_aws_region>
AWS_S3_BUCKET_NAME=<your_s3_bucket_name>

# JWT Authentication
SECRET_KEY=<secret_key_for_jwt>
ALGORITHM=<alogorithm_type>
ACCESS_TOKEN_EXPIRE_MINUTES=<time>
```

---

## Setting Up and Running Airflow
Navigate to the Airflow directory:
```
cd Airflow
```
Initialize Poetry
```
poetry init
poetry shell
``````
Intall dependencies
```
poetry install
```
Build and start Docker containers for Airflow:
```
docker compose build --no-cache
docker compose up
```
---

## Running Streamlit and FastAPI Services Locally

Initialize Poetry
```
poetry init
poetry shell
``````
Intall dependencies
```
poetry install
```
Run the Streamlit application
```
streamlit run Streamlit_UI_App/Home.py
```
Run the FastAPI backend
```
uvicorn FastAPI_Services.main:app --reload
```

---

##  Running Streamlit and FastAPI Services Using Docker Containers Locally
From the root directory, build and start the Docker containers
```
docker compose build --no-cache
docker compose up
```
---
