
**UCB Data Analysis Module 12**
## NoSQL Challenge - Analysis using PyMongo and MongoDB Compass

---------------
### Purpose:
The UK Food Standards Agency has requested evaluation of some of the ratings data for various food establishments across the United Kingdom.  This analysis will assist journalists and food critics to decide which businesses to cover in future articles.  

**Part 1: Database and Jupyter Notebook Set Up**  
  1. Imported .json file to MongoDB.  DB name = "uk_food";  collection = "establishments"
  2. Import libraries
       ```
       # Import dependencies
       from pymongo import MongoClient
       from pprint import pprint
       ```
  3. Create an instance of Mongo Client and assign collection to a variable.
     ```
     # Create an instance of MongoClient
     mongo = MongoClient(port=27017)

     # assign the collection to a variable
     establishments = db['establishments']
     ```

**Part 2: Update the Database**  
  1. Add a new restaurant entry to the database. (verify addition of entry)
     ```
      # Create a dictionary for the new restaurant data
      new_rd = {'BusinessName':'Penang Flavours',  'BusinessType':'Restaurant/Cafe/Canteen',
                'BusinessTypeID':'',  'AddressLine1':'Penang Flavours', 'AddressLine2':'146A Plumstead Rd',
                'AddressLine3':'London',  'AddressLine4':'',  'PostCode':'SE18 7DY', 'Phone':'',
                'LocalAuthorityCode':'511', 'LocalAuthorityName':'Greenwich',
                'LocalAuthorityWebSite':'http://www.royalgreenwich.gov.uk',
                'LocalAuthorityEmailAddress':'health@royalgreenwich.gov.uk',
                'scores':{'Hygiene':'', 'Structural':'', 'ConfidenceInManagement':''}, 'SchemeType':'FHRS',
                'geocode':{'longitude':'0.08384000', 'latitude':'51.49014200'},
                'RightToReply':'', 'Distance':4623.9723280747176, 'NewRatingPending':True}

      # Insert the new restaurant into the collection
      establishments.insert_one(new_rd)
     ```

  3. Edit new entry. (verify entry update)
     ```
      # Update the new restaurant 'Penang Flavours' with the correct BusinessTypeID
      establishments.update_one({"BusinessName": "Penang Flavours"}, {"$set": {"BusinessTypeID": btype["BusinessTypeID"]}})
     ```

  5. Delete all entries located in "Dover".  (verify deletion)
     1. See notebook.
  7. Change data type for lat/long coordinates from String to Decimal.  (verify)
     1. See notebook.
  9. Set unexpected Ratings Values to null.  (verify)
      ```
      # Set non 1-5 Rating Values to Null
      non_ratings = ["AwaitingInspection", "Awaiting Inspection", "AwaitingPublication", "Pass", "Exempt"]
      establishments.update_many({"RatingValue": {"$in": non_ratings}}, [ {'$set':{ "RatingValue" : None}} ])
      ```
  11. Change data type for Ratings Values to integer.
      1. See notebook.

**Part 3: Exploratory Analysis**  Created queries to address questionspertaining to database entries.
  1. See notebook.  

--------------
### Contents of Repository:
- Code Scripts
  - 2 x .ipynb python notebooks (NoSQL_setup_rjh.ipynb | NoSQL_analysis_rjh.ipynb)
- **FOLDER:** Resources
  - 1 x .json data file for import (establishments.json)
- 1 x README file

-------------------
### Contributions:  
N/A - just blood, sweat and tears

------------------
### License:
[MIT](https://choosealicense.com/licenses/mit/)
