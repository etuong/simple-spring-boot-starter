### Application
This is a very simple Spring Boot application that uses Flyway and Thymeleaf.

This app only has one endpoint (`http://localhost:8080/greeting?{name}`) that displays a Hello World message and an image.

To run locally, use `./gradlew clean bootRun --args='--spring.profiles.active=local'` so that the app uses application-local.properties

### Docker
First build the Docker image
```
docker build -t demo-mysql .
```

Then run the MySQL Docker image exposing the 3306 port and setting the environment variables.
Note that the MySQL variables have to match those of the application.properties
```
docker run --name mysql-db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=demo -e MYSQL_USER=demo -e MYSQL_PASSWORD=password -d mysql:8.0
```

Run this app's image and link the database to the MySQL container
```
docker run -p 8080:8080 --link mysql-db:mysql demo-mysql
```