# Health-Price-Transparency-Guide
Guide explaining the healthcare price transparency project and the steps to build the database

Link to Government Rule: https://www.cms.gov/priorities/key-initiatives/healthplan-price-transparency 

# TLDR version:
we are trying to build a health price comparison app using these steps: download .json file –> parse .json file –> export relevant data as .csv files –> clean .csv data in a SQL database manager –> upload cleaned data to Supabase -> build a front end on top of this database with the help of AI tools like Claude


# What is the main problem we are solving?

•	In the US, the prices for healthcare can differ by thousands of dollars for the same procedure in the same insurance plan. For example: If you went to the doctor to get an X-ray, you might pay only $100 at one place, but over $2000 at the neighboring hospital even though both hospitals are “in-network” for your insurance plan. 

•	Until now it was not possible to know about these prices, leading to patients being price gouged by hospitals and insurance companies. But a recent government rule now requires health insurance companies and hospitals to post their correct prices online.

•	But the main problem is that they are posting these prices in extremely large and complicated JSON files that are each 100+ GB in size and very poorly structured, making all of this data impossible to use for ordinary patients and businesses. 

•	By building a price transparency app, we are essentially converting this messy JSON data into a clean, user friendly sql database, which we can then incorporate into an interactive app for patients and business to use to save on healthcare costs. Economists are predicting savings of over $1 trillion per year from this solution, thus showing the massive market demand for this. 

# What is our business model: 2 services offered to businesses and individual patients

1.	Billing overpayment recovery service: 30-80% of medical bills contain errors leading to patients and their employers having to overpay. By identifying instances of these errors with the through price transparency data, we can help businesses save on their employees’ healthcare costs. We plan to charge a small percentage of money recovered as commission.
   
2.	Healthcare navigation service: When a doctor prescribes a medication or orders a procedure, patients can use our price transparency app to find which facilities and pharmacies will offer them the lowest cost for that medication/ medical procedure. This could be a subscription-based model that would ideally be paid for by the patients’ employers. 


# What exactly is price transparency data?

•	Price transparency data contains the negotiated rates between health insurance companies and hospitals, which is used to calculate how much a patient will pay. 

•	This data is stored as a JSON files that contains all of the rates for different procedures for any given health insurance plan. 

•	Price transparency files are found on the websites of health insurance companies.  These are also called “machine-readable files” by some people. 

•	To find the link to these files, just google “<health insurance company name> machine-readable file”

•	For example, this link takes you to the United Healthcare Website, which is the largest health insurance company in the US: https://transparency-in-coverage.uhc.com/ 

•	We search for the specific plan based on the patient’s employer


# How do we access this data?

1)	First, we need to access the “index” file. This JSON file contains links to other JSON files for a specific business. For example, this is the link to the “index” file for Saint Louis University employees. 

2)	Next, we need to extract all of the JSON files located in this main “index” file, by downloading the links that are listed in the “index” file. 

3)	Now that we have the file links, you will notice that this is a few gb, but this is a zipped file in gzip format. When we unzip it, it will become 100+GB. Because of this large size, I like to do all my preliminary data analysis in Google Collab instead of downloading it to my computer. 

# How to turn this massive JSON file into something “humanly readable”?

1)	The main challenge with analyzing this data is that all 100+gb of data is structured as a single deeply nested JSON object. So, when you try to use usual parsers to parse through this data, they always end up running out of RAM. 

2)	Instead, what has worked so far is to “flatten” this JSON file from this single object and convert it into a set of relational tables which we can then export in sql or csv format. 

3)	For this, follow the "Data Import Guide" file to download the data, and the "Data Analysis Guide" to clean the data and make it ready for uploading into Supabase. 
