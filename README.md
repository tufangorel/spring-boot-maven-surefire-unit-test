## spring-boot-maven-surefire-unit-test

1- Purpose : Customize maven test phase to execute only unit tests <br/>
2- Reason : maven-surefire-plugin executes all the Test classes in test/java directory but we want to only execute unit tests for each maven build. <br/>
3- To execute only specified unit tests for each maven build from the console run the following maven command : <br/>
NOT : Execute maven command from where the pom.xml is located in the project directory. <br/>
<pre> 
$ mvn clean install <br/>
</pre>

[INFO] --- maven-surefire-plugin:3.0.0-M5:test (default-test) @ spring-boot-maven-surefire-unit-test --- <br/>
[INFO] <br/>
[INFO] ------------------------------------------------------- <br/>
[INFO]  T E S T S <br/>
[INFO] ------------------------------------------------------- <br/>
[INFO] Running com.company.customerinfo.service.unit.test.ProductServiceUnitTest <br/>
[INFO] Tests run: 2, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.747 s - in com.company.customerinfo.service.unit.test.ProductServiceUnitTest <br/>
[INFO] <br/>
[INFO] Results: <br/>
[INFO] <br/>
[INFO] Tests run: 2, Failures: 0, Errors: 0, Skipped: 0 <br/>

4- surefire-reports can be accessed from the application directory : "target/surefire-reports" <br/>

![maven_surefire_plugin](doc/maven-surefire.png) <br/>

### Tech Stack
Java 11 <br/>
H2 Database Engine <br/>
spring boot <br/>
spring boot starter data jpa <br/>
spring boot starter web <br/>
spring boot starter test <br/>
hibernate <br/>
logback <br/>
maven <br/>
maven-surefire-plugin <br/>
springfox-swagger-ui <br/>
datasource-proxy <br/>
Docker <br/>
<br/>

### Docker build run steps
NOT : Execute docker commands from where the DockerFile is located. <br/>
<pre>
$ docker system prune <br/>
$ docker build . --tag demo  <br/>
$ docker run -p 8080:8080 -e "SPRING_PROFILES_ACTIVE=dev" demo:latest <br/>
</pre>

## API OPERATIONS
### Save store with products successfully to database

Method : HTTP.POST <br/>
URL : http://localhost:8080/customer-info/store/save <br/>

Request : 
<pre>
curl --location --request POST 'http://localhost:8080/customer-info/store/save' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "jeans_store",
  "products": [
    {
      "name": "prod1"
    },
    {
      "name": "prod2"
    },
    {
      "name": "prod3"
    }
  ]
}'
</pre><br/>

Response : 

HTTP response code 200 <br/>
<pre>
{
    "id": 1,
    "name": "jeans_store",
    "products": [
        {
            "id": 1,
            "name": "prod3"
        },
        {
            "id": 2,
            "name": "prod1"
        },
        {
            "id": 3,
            "name": "prod2"
        }
    ]
}
</pre>


### List Store saved to database

Method : HTTP.GET <br/>
URL : http://localhost:8080/customer-info/store/list <br/>

Request : 
<pre>
curl --location --request GET 'http://localhost:8080/customer-info/store/list'
</pre><br/>

Response : 

HTTP response code 200 <br/>
<pre>
[
    {
        "id": 1,
        "name": "jeans_store",
        "products": [
            {
                "id": 1,
                "name": "prod3"
            },
            {
                "id": 2,
                "name": "prod1"
            },
            {
                "id": 3,
                "name": "prod2"
            }
        ]
    }
]
</pre><br/>
