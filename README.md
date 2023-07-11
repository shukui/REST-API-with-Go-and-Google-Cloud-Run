# REST-API-with-Go-and-Google-Cloud-Run
1. Activate Cloud Shell
   Click Activate Cloud Shell Activate Cloud Shell icon at the top of the Google Cloud console
2. gcloud auth list
3. gcloud config list project

   Name	      API
Cloud Build	 cloudbuild.googleapis.com
Cloud Run	    run.googleapis.com

## Activate your project
gcloud config set project $(gcloud projects list --format='value(PROJECT_ID)' --filter='qwiklabs-gcp')

git clone https://github.com/rosera/pet-theory.git && cd pet-theory/lab08


## Dockerfile
FROM gcr.io/distroless/base-debian10
WORKDIR /usr/src/app
COPY server .
CMD [ "/usr/src/app/server" ]

## Build binary with following command
go build -o server    
ls -la   

## Deploy REST API
This command builds a container with your code and puts it in the Container Registry of your project.
gcloud builds submit \
  --tag gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.1

You can see the container if you click: Navigation menu > Container Registry
Once the container has been built, deploy it:
gcloud run deploy rest-api \
  --image gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.1 \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --max-instances=2

## Create Database and Import Data
 Navigation Menu > Firestore, Click the Select Native Mode button, Wait for the database to be created.
 Migrate the import files into a Cloud Storage bucket that has been created for you:
 
 gsutil cp -r gs://spls/gsp645/2019-10-06T20:10:37_43617 gs://$GOOGLE_CLOUD_PROJECT-customer

import this data into Firebase:
gcloud beta firestore import gs://$GOOGLE_CLOUD_PROJECT-customer/2019-10-06T20:10:37_43617/


## Build and deploy
go build -o server

gcloud builds submit \
  --tag gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.2

gcloud run deploy rest-api \
  --image gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.2 \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --max-instances=2
  
