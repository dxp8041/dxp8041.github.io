# dxp8041.github.io
Final Deliverables

Motivation and objectives:
The objective of this project was to implement the recommender system in which  users will be recommended businesses based on their previous preferences. When people like certain stuff and that stuff is liked by someone else, then there is some similarity between these users. So, based on the preferences shown by the second user, we can predict the items for the first user. Doing this will not only will improve the customers to the current businesses but also help people to select the businesses  want to go for next time.

Data mining/analysis tasks tackled
Any system that predict the items or services is called a recommender system. In this project, I built the recommender system based on Collaborative filtering. Collaborative filtering is categorized into two groups. One is memory based algorithms and another one is model based methods.

In the memory based methods, the entire rating matrix is built and the system use that rating matrix to recommend products to the user. Rating matrix is built from the ratings given by the user. In this dataset, various users id provide rating to the business. These ratings are ordinal values from 1 to 5. 

In this project, I implemented the item-based collaborative filtering in which rating given by users are stored into the data structures, and later on used as computing cosine similarity in order to predict the businesses for the user. 

Design of Methods:
There are two major files in the recommender system. One is BigData.java and the other one is Recommender.java.

Class BigData.java
There are three Map structures in the BigData.java. They are users, reviewsByUser and businesses. So, when the recommender system is run, the system displays a message “Big data load Started”. The path of the yelp_dataset must be provided earlier to the execution of the system. Then the system will use loadBusinesses() method to load the current businesses under businesses map data structure. After loading businesses, the system will use loadUsers and loadReviews methods respectively. Furthermore, there are four methods implemented in BigData.java which primary responsibilities are to get the user related businesses, reviews and user itself using user id and business id.

Similary, Business.java, Review.java and User.java classes are created and their respective getters and setters methods are created. 

Recommender.java
The Second major class is Recommender.java. I have implemented the item based  collaborative filtering algorithm. Collaborating filtering works by building a huge dataset in the database and recognizes the pattern in which the previous users’ rating is compared for its decision making. Suppose user A has liked certain restaurants previously, then the key to recommend user A with other types of restaurant is to look at the neighbor users who have previously liked and used the restaurants. When the program gets this information, then those businesses are withdrawn from the dataset and are displayed to the user. 

However, one of the main challenges of implementing this algorithm was the performance. Since the dataset we were given was extremely large, there had been some compromise on the performance. Furthermore, in order to accurately recommend, we needed more dataset that will have millions of potential neighbors. This algorithms effectively work on tens of thousands of neighbors in real time, but searching for tens of millions of people and their  preferences is certainly a tedious task for the computer. 

Let me briefly describe the details of the algorithm used in this project. The project uses item-based collaborative filtering. Item based collaborative filtering searches the set of items the target user has rated and computes how similar they are to the user that recommendation is building.The similarity between two items i and j is to first isolate the users who have rated both of these items and then apply a similarity computation technique to determine the similarity. 

Calculation of Cosine Similarity For Collaborative Filtering:
Weighted Sum:
This method predicts item i for user u by computing the sum of items given by user on the items similar to i. Each rating is weighted by corresponding similarity sI,J between item i and j.

Implementation of methods:
WebMain.java:
WebMain.java is a java class that initiates apache server in port 8080. The contents of this class file is collected from “” and can also be seen on references. WebMain.java’s primary responsibility is to get the arguments and process it. We provide our yelp_data set path on program arguments. The following steps will allow you to set the path for you data set.

First Step is to Click Run
Select Run configurations
Under main class=recommender.WebMain Go to  arguments->program
arguments=%pathToYeldJsonsFolder%


where pathToYeldJsonsFolder - path to yeld jsons folder

Once the data set path is provided and the system is run, the BigData.load(args[0]);
which is the static method in BigData class is initiated. 

BigData.load(arg[0])
On console, Create message “Big data load started”
Use loadBusinesses(floderPath) to create a map structure of business
Use loadUsers(folderPath) to create a map structure of users.
Use loadReviews(folderPath) to create a map structure of reviews.
Display message “Big data load ended”.
If there are any exceptions, display “Failed to load big data”.

BigData.loadUsers(String folderPath)
Create object parser of JSONParser().
Iterate through each line of users data set using folderPath plus + "/yelp_academic_dataset_business.json"
Create JSONObject that creates object of json line.
Create user object of User class.
Assign id,averageStars,reviewCount and name to user object from json object.
Once successfully loaded, display a message “Users  loaded successfully”

At this point we have a huge data structure of businesses.


BigData.loadReviews(String folderPath)
Create object parser of JSONParser().
Iterate through each line of reviews data set using folderPath plus + "/yelp_academic_dataset_business.json"
Create JSONObject that creates object of json line.
Create review object of Review class.
Assign businessId, userId, stars, date to business object from json object.
Once successfully loaded, display a message “Reviews loaded successfully”

At this point we have a huge data structure of businesses.


BigData.loadBusinesses(String folderPath)
Create object parser of JSONParser().
Iterate through each line of Business data set using folderPath plus + "/yelp_academic_dataset_business.json"
Create JSONObject that creates object of json line.
Create business object of Business class.
Assign id, name, address,city,state,reviewCount and stars to business object from json object.
Once successfully loaded, display a message “Businesses loaded successfully”

At this point we have a huge data structure of businesses.



BigData.getUserReviews(String userId)

 Returns a list of reviews issued by user with id=userId
  BigData.getReviewsByUsers()
Returns all reviews available

BigData.getBusinessById(String businessId)
   
   Returns business data of business with id=businessId
   
  
BigData.getBusinessById(String userId)
  
   Returns user data of a user with id=userId
   

Recommender.java
Recommender.java has two fields. One is k and another one is NUM_TO_RECOMMEND. k is for k-nearest algorithms. I have set k=8 and number of businesses to recommend is set to 4.

recomend(String userId):List<Business>

/**
   * Recommends businesses to the user with id=userId
   */

System display message to GUI “User to investigate= “ plus user id.
System creates an object  pqueue of java standard class PriorityQueue which stores top k nearest neighbors.
Create object of list userReviews that has a list of all reviews done by that particular user.
Create a map of userReviewByBusiness.
For each userReviews, add to map userReviewsByBusiness.
calculate cosine similarity using calcCosineSimilarity function.
Loop through all users in the Big Data.
Skip if it is the same user data.
Find all recommended businesses by using k neighbours.
calcCosineSimilarity(Map<String, Review> user1ReviewsByBusiness, List<Review> user2Reviews):double
The result is in the range [-1..1]
Indicates perfect similarity
Indicates perfect negative similarity
Calculate the sum of user 1 rating from user1ReviewsByBusiness map and name it to x2sum.
Then loop through reviews of user2.
Handle only business which rated both users.
Add all rating that the user 1 and user 2 provided.
Add all ratings of user 2 from user2ReviewsByBusiness map and name it to y2sum.
Multoply the square root of x2sum and y2sum and assign it to name denominator
if denominator is greater than 0, our cosine similarity will be xy/ denominator.


How to Run the project on your machine?
How to run:
1. Move directory 'recommender.zip' to eclipse workspace from https://github.com/dxp8041/dxp8041.github.io 
2. Open eclipse.
3. Import maven project: in eclipse: File -> Import.. -> Maven (Existing Maven Projects) -> select 'recommender' folder -> Finish
4. Run WebMain: Run -> Run configurations... -> main class=recommender.WebMain, arguments->program arguments=%pathToYeldJsonsFolder%
where pathToYeldJsonsFolder - path to yeld jsons folder
5. After Jetty server is started, in browser go to http://localhost:8080

Project structure:
1. src\main\java - root of the java classes:
   a. BigData.java - in-memory storage of yeld data, provides method to retrive users, revies, businesses;
   b. User.java, Review.java, Business.java - yeld entities;
   c. Recommender.java - implementation of collaborative filtering algorithm;
   d. ConsoleMain.java - entry point of console app;
   e. WebMain.java - entry point of web app(starts Jetty server listening on port 8080).
2. src\main\resources\web - root of the web app:
   a. login.jsp and main.jsp - java JSP pages for login and main logic correspondingly;
   b. WEB-INF\web.xml - deployment descriptor (in this case specifies default page);
   c. img - folder containing images for the web app;
   d. css/bootstrap.css and recommender.css - css for this 



Resources used:
1. Jetty - web server http://eclipse.org/jetty/
2. Jetty official example of embedded server https://github.com/jetty-project/embedded-jetty-jsp
3. css - http://getbootstrap.com/
4. bootstrap examples http://getbootstrap.com/getting-started/ 


The site is running on my machine:

http://71.8.126.41:8080/



