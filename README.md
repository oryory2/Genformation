
<p align="center">
  <img src="https://github.com/JonathanP-Git/Geneformation/assets/55094482/1b1a6827-82bb-4024-ac1e-bd8faa97d811" alt="architecture" width="400" height="100" />
</p>

Genformation provides free access to reliable, easy to understand
information about genetic and rare diseases.

#
https://user-images.githubusercontent.com/55094482/213119002-b924650d-0200-4d3c-ac04-b6ad39c8ee09.mp4

### System Architecture - Implemented with Docker


**Client Side (Vue.js Container)**
Manages the website frontend, oversees user interface and interaction, and connects with the backend.

**Server Side (Python, Flask Container)**
Handles backend logic, processes user inputs, fetches data, and formats information for display.

**Database (MongoDB Container)**
Holds necessary data for the site, interacting with the Flask application to provide user-specific data.

**Nginx Container**
Functions as a reverse proxy and web server, directing HTTP requests to the appropriate containers.

**Continuous Integration/Deployment: Jenkins**
Used for automating build, test, and deployment, ensuring smooth development workflow.

Using Docker enhances flexibility and deployment efficiency, while Jenkins help with continuous integration and deployment.

<p align="center">
  <img src="https://github.com/JonathanP-Git/Geneformation/assets/55094482/445ce35a-94fb-4b84-a550-6d563ea3ef96" alt="architecture" width="500" height="440" />
</p>


## How to run the system locally
To run the system locally, you must run both frontend and backend servers.

> **Frontend server**: run ``` {father_directory}/Geneformation/flask-vue-crud/client | npm run lint --fix | npm run serve ```

Note: The npm  ``` run lint --fix ``` command is responsible for fixing the file and saving a lot of wasted time.

 > **Backend server**: run ``` {father_directory}/Geneformation/server | python3 app.py ```
 
 ## How to run the system using Docker
 
Pull the the images from docker-hub.

> Run the command ``` docker-compose up  ```

#
## Script documentation

In this project, there are several scripts designed to facilitate the workflow and ongoing maintenance of this project.
All of the scripts are located under the directory 'extras/scripts'.


### submissions_script 

<ins>Purpose</ins>

Inserting all clinVar submissions of genetic changes that were manually entered into the ClinVar website into the system's database.

<ins>process</ins>

First, a loading process of all the submissions is performed from the clinVar submissions text file.
Next, an augmentation is carried out for each submission: we add to it the corresponding gene name and mutation related to the same genetic change - we obtain this information using an API request to the ClinVar website.
Finally, after holding all the desired information for each submission, a writing of the documents takes place into an Excel file and insertion of all the documents into the database.

<ins>running instructions</ins>

 1. download the submission.txt file from ClinVar site (by mail), and put in your preference path - "path".
 2. open your mongoDB and make a connection, make sure that you have a DataBase inside called "Geneformation".
 3. if needed, install all the imports via your cmd (req, pymongo) -> cmd -> pip install "name".
 4. open the directory containing the specific script, and run the next command: python submissions_script.py "path".

Note: In order to receive an updated file containing all the documentation from the ClinVar website, please submit a request to the following email: clinvar@ncbi.nlm.nih.gov 




### metadata_mapping_script

<ins>Purpose</ins>

Creating the metadata for each existing gene, and inserting it into the database.
Creating and inserting mappings between non-"central" gene names to their "central" gene name.

<ins>process</ins>

First, a loading process of all the gene names is performed from the genenames text file.
Next, an augmentation is carried out for each gene name: we add to it all of his metadata - we obtain this information using a couple of API requests to different data sources.
Finally, after holding all the desired information for each gene name, we are inserting all this information to the database.
In this process we are also creating the different mapping between each non’”central” gene to his central gene name. Those mapping are also being inserted to the database, and they will help us to fetch the metadata for each existing non-"central" gene (we fetched the metadata of his central gene name instead).

<ins>running instructions</ins>

1. download the genes.txt file from genenames site, and put in your preference path - "path".
2. open your mongoDB and make a connection, make sure that you have a DataBase inside called  "Geneformation".
3. if needed, install all the imports via your cmd (req, pymongo) -> cmd -> pip install "name".
4. open the directory containing the specific script, and run the next command: python metadata_mapping_script.py "path".


Note: In order to receive the genenames file containing all the gene names: go to genenames site and download the following file: [Custom downloads | HUGO Gene Nomenclature Committee (genenames.org) ](https://www.genenames.org/download/custom/)
choose only those columns: Approved symbol, Previous symbols, Locus group.




## import_jason_script

<ins>Purpose</ins>

Help to import json files into mongoDB in an easy and fast way.


<ins>running instructions</ins>

Import all your .json files that can be found in a specific folder, and insert them into your Mongo “Geneformation” DataBase - each .json file will be a new collection in your DB.

running instructions

Assuming that you have saved the Python script file with the name import_files.py and you want to import JSON files from a directory located at /path/to/json/directory, you can call the import_files() method from the terminal using the following command:

python import_files.py /path/to/json/directory

Make sure that you have python installed on your system and that you have navigated to the directory containing the import_files.py script before running this command. This command will import all JSON files present in the specified directory into a MongoDB database.





