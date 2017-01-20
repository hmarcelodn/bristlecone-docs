# Bristlecone Financing Solution #

Architecture and deployment process documentation for Bristlecone Financing.

## Application Deployment ##

1. Install a SQL Server Instance.
2. Download ***Technodrome*** .zip file from Google Docs.
2. Clone the project repository [https://bitbucket.org/bristlecone/bristleconefinancing](https://bitbucket.org/bristlecone/bristleconefinancing) and all *submodules*.
3. Go into ***Technodrome*** folder already downloaded on step 2.
4. Execute one of the restore files (check the configuration you have in the ***web.config*** file).
5. After running succesfully the restoring process it will create a secureLogin login and database user. Restart the SQL Service to reflect the changes otherwise the SQL account will not work.
6. Open your VS Solution > Build > Run.


## Application High Level Overview ##

The platform is essentialy a lease management/origination system. Its a web application with Administration logins that allow for the management of those applications and the creation of financing contracts. Below are described the different collaborators:

**Mobwi Project**

This is the main project where ***Applications*** are created:

1. *Customers* *(Most applications initiates here.)*
2. *Admin*
3. *Retailers*


Mobwi triggers ***TheDecider*** module from the *ApplicationControllers* of *Customers*, *Admin* and *Retailers* areas calling *ResumeDecidingAsync()*. Also mobwi uses ***HoradricCube*** to write data to the database.

**TheDecider Project**

This is the business rules engine that steps the customer's application into an approval process. Inside decider are ***"post decider actions"*** which invokes the ***Monopilizer*** API  which is the Pricing service and finally updates the database througth ***HoradricCube***. These results are visible on the main grid views inside of the Admin and Retailer areas. (e.g. \Areas\Admin\Views\Applications\Index.cshtml).


**TheInternet Project**

Transactional e-mails are sent out during TheDecider run via Correspondence project.

**Integration Projects**

External data is retrieved by using the following:

1. ***Mitochrondria***
2. ***SixthSense***
3. ***SupermanIII***


**Monopolizer API**

API for pricing retrieval and its not part of bristleconefinancing solution.

**CommunityChest Project**

Communicates to ***Monopolizer*** API.

**BeatifulMind Project**

1. ***UserService**:New customer "user" is created via BeautifulMind\UserService.*
2. ***AuditService**: Audit history of the application taking place are done via BeautifulMind\AuditService*.

## High Level Overview ##

Application High Level Overview.


![](https://raw.githubusercontent.com/hmarcelodn/bristlecone-docs/master/BristleCone%20OV.png)