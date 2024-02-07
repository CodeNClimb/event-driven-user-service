# EVENT DRIVEN USER INFORMATION SERVICE

## ABOUT THE SERVICE
This repository uses event driven architecture to allow users to be added to a database. A publisher microservice fires a series of messages containing the details of an individual to the event broker(solace), after which subscriber service will pick up the data and add it to database. 

## SOLACE
Solace is an event broker that enables message-oriented middleware services that routes information between applications, devices and user interfaces. Learn more about solace and how it functions by visiting their [official docs](https://docs.solace.com/).


## SETTING UP - CLONE THE PROJECT
- Ensure you have Docker up and running.
- Open a terminal or command prompt (Powershell on Windows and Terminal or linux or macOS)
- Navigate to the directory in which you want to clone the project as shown below
```powershell
cd path/to/your/directory
```
- Run 
```powershell
git clone git@github.com:msackey-IW/event-driven-user-service.git
```
- Alternatively, in the [project repository](https://github.com/msackey-IW/event-driven-user-service) you can navigate to `code -> Open with GitHub Desktop` and clone the repository through GitHub Desktop.
- Run the code snippet below in the terminal.
```powershell
cd event-driven-user-service
```
- Run the code snippet below in your terminal.
```powershell
docker-compose up -d
```
- The above command creates 2 event driven microservices(publisher and subscriber), solace, a postgeSQL database and pgAdmin to access the postgres db. 
- The publisher fires a list of user details to the topic `Topic/People/Add` to which the consumer subscribes.
- The subscriber then takes all the data and persists it in the posgresSQL database.
- Due to the size fo the images, the application may take some time to get up and running. Allow for up to 10 minutes.

## TESTING THE APPLICATION

- Open the pgAdmin graphical user interface by navigating to the url below in your web browser.
```
http://localhost:5050
```
- Login using the credentials below.
```json
{
    "username/email": "admin@admin.com",
    "password": "admin"
}
```

- Once logged in, click the `add new server` button.
- In the `Name` input field, input `Postgres DB`.
- Click on `connections` in the top menu.
- In the `Host name /address` name field, input `db`.
- In the password field, input `admin`.
- Click the `save` button.
- On the left panel, navigate to `Postgres DB -> Databases -> admin`.
- In the top menu, click on `Tools -> Query Tool`.
- In the now created query box, input the SQL command below.
```sql
SELECT * FROM users;
```
- The query should output all the users who have been successfully added the database.


