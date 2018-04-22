# bank-slips-api

API REST with Spring Boot

# Installation
Ensure that Java 8 and Maven 3.2 are installed

# Git Clone
Clone this repo: git clone https://github.com/adrianoprezende/bank-slips-api.git

# Usage
Running the Spring Boot app
Navigate to the directory into which you cloned the repo and execute this: mvn spring-boot:run

Once started you can access the APIs on port 8080, e.g. http://localhost:8080/rest/bankslips

# API Specification
# POST
http://localhost:8080/rest/bankslips
Create a new bankslip
Json body example:
{
	"due_date":"2018-01-01",
	"total_in_cents":"100000",
	"customer":"Trillian Company",
	"status":"PENDING"
}

Expected possible status:
PENDING, PAID, CANCELED

Expected due_date format:
yyyy-MM-dd

# GET
http://localhost:8080/rest/bankslips
List all bankslips that was created

# GET
http://localhost:8080/rest/bankslips/{id}
Gets the bankslip with the id passed as argument, if exists.
If the bank slip has expired, the fine is calculated.

Fine rules:
● Until 10 days: Fine of 0,5% is applied.
● Above 10 days: Fine of 1% is applied.

Response Example:
{
    "statusCode": 200,
    "message": "Ok",
    "listError": null,
    "object": {
        "id": "379a345e-2439-4f7e-a486-73bb5d011930",
        "customer": "Trillian Company",
        "status": "PENDING",
        "fine": "1000",
        "due_date": "2018-01-01",
        "total_in_cents": "100000"
    }
}

# PUT
http://localhost:8080/rest/bankslips/{id}/pay
Pays the bankslip with the id passed as argument, chaging it's status to PAID.


# DELETE
http://localhost:8080/rest/bankslips/{id}/cancel
Cancels the bankslips with the id passed as argument, changing it's status to CANCELED.


