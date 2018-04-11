# SmartPlan Notebook

## Prerequisites
### Mongodb:
* MongoDB is a popular open-source document-oriented database developed by 10gen, later called the MongoDB Inc. In this case, documents are created and stored in BSON files, Binary JSON (JavaScript Object Notation) format, so all JS types of data are supported. 
* What we need to do:
  + First: Install Mangodb on your local machine. For more information check the following link.

    + [link](https://www.mongodb.com/download-center#atlas)

  + Second: Install RoboMongo on your local machine. RoboMongo is a visual tool helping you manage Database Mongodb. 
  + Note: Before creating a connection in RoboMongo you need to follow a preliminary procedure. So, please watch the following youtube link: 
 
    + [link](https://www.youtube.com/watch?v=1uFY60CESlM)


### JSON and BSON:
* JSON, or JavaScript Object Notation, is a minimal, readable format for structuring data. The two primary parts that make up JSON are keys and values. Together they make a key/value pair.
* Key: A key is always a string enclosed in quotation marks.
* Value: A value can be a string, number, boolean expression, array, or object.
* Key/Value Pair: A key value pair follows a specific syntax, with the key followed by a colon followed by the value. Key/value pairs are comma separated.
* BSON is the binary encoding of JSON-like documents that MongoDB uses when storing documents in collections.
* For more information: 
 
  + [link](https://www.tutorialspoint.com/json/index.htm)


## About the notebook
* The provided notebook can be used for N-1 Replication and Optimization studies.
* This notebook contains the following steps:
1. Import the required libraries
2. Connect to the database
3. Submit Investment_Catalog to database
4. Create the commander file and submit data to database
5. Run N-1 Replication or/and Optimization studies
6. Filter the obtained results

#### Note 1: 
Before running the current jupyter notebook:
* create a folder in Drive "C" called job_stack
* create a folder in Drive "C" called TARA which contains tara_1702.exe

#### Note 2: 
job_manager.py file should be run seperately, after submitting data to database.
