# Steps to start-up in the IBM Cloud Environment

## Run Mongo Server
1. Navigate to xrwvm-fullstack_developer_capstone/server/database
2. Build the nodeapp
  docker build . -t nodeapp
3. Start the server
  docker-compose up
4. Launch the application on Port 3030 (Using 'Launch application') - You should see 'Welcome to the Mongoose API'
5. Open djangoapp/env and replace the backend_url if needed with the url from step 4

## Run Sentiment Analysis Microservice
1. In the code engine CLI, change to server/djangoapp/microservices directory
  cd xrwvm-fullstack_developer_capstone/server/djangoapp/microservices
2. Run the following command to docker build the sentiment analyzer app
  docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer
3. Push the docker image by running the following command.
  docker push us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer
4. Deploy the senti_analyzer application on code engine.
  ibmcloud ce application create --name sentianalyzer --image us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer --registry-secret icr-secret --port 5000
5. Connect to the URL that is generated to access the microservices and check if the deployment is successful.
6. Open djangoapp/.env and replace the code engine deployment url with the deployment URL from above.
  sentiment_analyzer_url=your code engine deployment url

##To be completed##
8. Initialize the server
  pip install virtualenv
  virtualenv djangoenv
  source djangoenv/bin/activate
9. Install required packages
  python3 -m pip install -U -r requirements.txt
10. Perform model migrations:
  python3 manage.py makemigrations
  python3 manage.py migrate
  python3 manage.py runserver
