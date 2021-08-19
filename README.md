Semantic sentence similarity using MLSTM

The files required to train the model from scratch on any system is present in the GitHub repository given below.
https://github.com/Rajath-SRH/mlstm_keras
The files required to deploy the application on Heroku Cloud is in the repository below
https://github.com/rajath-analytics/mlstm_keras
The application is hosted on Heroku cloud - https://mlstm.herokuapp.com/
To reproduce the application on the system, please clone or download the repository to your workspace.

Note : The working directory should be set to “mlstm_keras” folder. The paths specified in the code are relative to this folder.

Data Collection
Data required for training is present in /data. The file is snli_1.0_train.csv.

Training the model
Execution flow of Manhattan – LSTM:
To implement Manhattan LSTM below four python files are to be placed in the same
absolute path.
1.	util.py – This file does all the preprocessing for the sentences.
2.	train.py – In this file we define and train the model
3.	predict.py – To predict scores for sentence pairs using the saved model.
4.	word2vec.py – Creates a custom word embedding file for the dataset so that it does not use word2vec model entirely.

MLSTM model is trained using train.py file that imports util.py as a module having functions developed for word embeddings, padding and calculation of Manhattan distance.

Sequence to train the model:
Step 1 : First execute the file word2vec.py for dataset in /data - snli_1.0_train.csv with 550K sentence pairs to generate a .w2v file which we later use for embedding.

Step 2 : Replace the embedding file with a newly generated .w2v present in /data folder in 
function word2vec of util.py in order to create embeddings. (This step needs to be done only if you change the file name specified)

Step 3 : Run train.py
Specify the relative path of the dataset used to train the model. 

Step 4: Model is then saved to evaluate for a new dataset. Model accuracy
and loss are plotted and saved as a .png file. Both the saved model .h5 file and the training plot image will be present in /data folder.

Model can be evaluated by running predict.py file.
Step 1: A new dataset with 20 sentence pairs test-20.csv is given as input for prediction.

Step 2: util.py file is imported as a module in predict.py with all functions defined to implement zero padding and calculate Manhattan distance.

Step 3 : Finally scores for the sentence pairs are predicted from the trained
model loaded using model.load().

Step 4 : Predicted Scores vary between range 0-100%. The higher the value the more similar the two sentences are.

Web Application and cloud deployment in Heroku cloud
The files required to bundle the model and its dependencies are
1.	Procfile  - Specify what file needs to run when the application is requested.
2.	app.py – Flask application definition: We process the input from the html form and send it for prediction by loading the model present in the /data folder.
3.	/templates – HTML form to take inputs from user
4.	Requirement.txt – specify the application dependencies to create a custom environment for the application to run on the server.
5.	runtime.txt – specify the python version for the server. Heroku by default takes python 3.9
6.	test-20-csv in /data folder – Dummy file to get the dataframe for the user inputs fetched from web form.

Sequence to run the application in local system:

Step 1 : Run app.py – In the application output log you will receive the IP address	where the flask application runs on localhost. Open a browser window add enter the IP address.

Step 2 : A simple HTML page is used which takes the user input. Enter the sentence pair for which sentence similarity needs to be computed. Click predict similarity button to get the scores. The scores will be computed and displaced within seconds.

Cloud Deployment in Heroku:

Fork the repository given below to a GitHub repository. This is required to connect Github using account credentials to deploy the code in Heroku cloud.
https://github.com/rajath-analytics/mlstm_keras - Does not have training datasets therefore smaller in size.s

Steps to deploy in cloud:
Step1: Create an account in Heroku cloud

Step2 : Create a new app. Give a suitable name for application and create the app.

 
Step3 : Under Deploy tab, choose deployment method as GitHub.

 
Connect to the repository and submit it for deployment by clicking on the “Deploy Branch” button.
This will set up the python environment required to run the application. After few minutes the app will be deployed. Use the “Open app” button to start the application.
