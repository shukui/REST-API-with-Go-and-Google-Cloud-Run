# REST-API-with-Go-and-Google-Cloud-Run
1. Activate Cloud Shell
   Click Activate Cloud Shell Activate Cloud Shell icon at the top of the Google Cloud console
2. gcloud auth list
3. gcloud config list project

   Name	      API
Cloud Build	 cloudbuild.googleapis.com
Cloud Run	    run.googleapis.com

Activate your project
gcloud config set project $(gcloud projects list --format='value(PROJECT_ID)' --filter='qwiklabs-gcp')

git clone https://github.com/rosera/pet-theory.git && cd pet-theory/lab08

