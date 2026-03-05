\# Customers Management API



\## Overview



Customers Management API is a RESTful service built with MuleSoft that exposes CRUD operations for managing customers.



The API allows clients to:



\* Search for customers

\* Create a new customer

\* Retrieve a customer by ID

\* Update an existing customer

\* Delete a customer



The application is built using \*\*Mule 4\*\* and deployed to \*\*Anypoint Platform\*\*.



---



\# API Base URL



```

https://customers-management-api-lgc39y.5sc6y6-2.usa-e2.cloudhub.io/api

```



---



\# Data Model



Customer entity:



| Field       | Type     | Description           |

| ----------- | -------- | --------------------- |

| id          | number   | Unique identifier     |

| firstName   | string   | Customer first name   |

| lastName    | string   | Customer last name    |

| email       | string   | Customer email        |

| dateOfBirth | date     | Customer birth date   |

| createdAt   | datetime | Creation timestamp    |

| updatedAt   | datetime | Last update timestamp |



---



\# Endpoints



\## 1. Search Customers



Search for customers using optional query parameters.



```

GET /customers

```



\### Query parameters



| Parameter | Type   | Description         |

| --------- | ------ | ------------------- |

| email     | string | Filter by email     |

| lastName  | string | Filter by last name |



\### Example request



```

GET /customers?email=john@email.com\&lastName=Smith

```



\### Response



```

200 OK

```



```

\[

&nbsp; {

&nbsp;   "id": 1,

&nbsp;   "firstName": "John",

&nbsp;   "lastName": "Smith",

&nbsp;   "email": "john@email.com",

&nbsp;   "dateOfBirth": "1990-01-01",

&nbsp;   "createdAt": "2026-03-04T16:43:36.639031+00:00",

&nbsp;   "updatedAt": "2026-03-04T16:43:36.639031+00:00"

&nbsp; }

]

```



---



\# 2. Create Customer



```

POST /customers

```



\### Request body



```

{

&nbsp; "firstName": "John",

&nbsp; "lastName": "Smith",

&nbsp; "email": "john@email.com",

&nbsp; "dateOfBirth": "1990-01-01"

}

```



\### Response



```

201 Created

```



```

{

&nbsp; "id": 10,

&nbsp; "firstName": "John",

&nbsp; "lastName": "Smith",

&nbsp; "email": "john@email.com",

&nbsp; "dateOfBirth": "1990-01-01",

&nbsp; "createdAt": "2026-03-04T16:43:36.639031+00:00",

&nbsp; "updatedAt": "2026-03-04T16:43:36.639031+00:00"

}

```



---



\# 3. Retrieve Customer



```

GET /customers/{id}

```



\### Example



```

GET /customers/10

```



\### Response



```

200 OK

```



```

{

&nbsp; "id": 10,

&nbsp; "firstName": "John",

&nbsp; "lastName": "Smith",

&nbsp; "email": "john@email.com",

&nbsp; "dateOfBirth": "1990-01-01",

&nbsp; "createdAt": "2026-03-04T16:43:36.639031+00:00",

&nbsp; "updatedAt": "2026-03-04T16:43:36.639031+00:00"

}

```



---



\# 4. Update Customer



```

PATCH /customers/{id}

```



\### Example request



```

{

&nbsp; "firstName": "UpdatedName"

}

```



\### Response



```

200 OK

```



```

{

&nbsp; "id": 10,

&nbsp; "firstName": "UpdatedName",

&nbsp; "lastName": "Smith",

&nbsp; "email": "john@email.com",

&nbsp; "dateOfBirth": "1990-01-01",

&nbsp; "createdAt": "2026-03-04T16:43:36.639031+00:00",

&nbsp; "updatedAt": "2026-03-04T17:43:36.639031+00:00"

}

```



---



\# 5. Delete Customer



```

DELETE /customers/{id}

```



\### Response



```

204 No Content

```



Customer is successfully deleted and no response body is returned.



---



\# Security



The API is secured using \*\*OAuth 2.0\*\*.



\### Scopes



| Scope            | Description                            |

| ---------------- | -------------------------------------- |

| customers:read   | Allows reading customer data           |

| customers:write  | Allows creating and updating customers |

| customers:delete | Allows deleting customers              |



Authentication must be provided in the request using a valid OAuth 2.0 access token.



---



\# Database



Customer data is stored in a \*\*PostgreSQL database hosted on Supabase\*\*.



The Mule application interacts with the database \*\*via the Supabase REST API\*\*, which exposes PostgreSQL tables as REST endpoints.



This approach allows secure access to the database without exposing direct database credentials.



---



\## Database Technology



\* Database: PostgreSQL

\* Hosting: Supabase

\* Access Method: REST API (Supabase auto-generated endpoints)



---



\## Customer Table Schema



The API operates on the `customers` table with the following structure:



```

CREATE TABLE customers (

&nbsp; id BIGSERIAL PRIMARY KEY,

&nbsp; first\_name VARCHAR(100),

&nbsp; last\_name VARCHAR(100),

&nbsp; email VARCHAR(255),

&nbsp; date\_of\_birth DATE,

&nbsp; created\_at TIMESTAMP,

&nbsp; updated\_at TIMESTAMP

);

```



---



\## Communication Flow



```

Client

&nbsp;  ↓

MuleSoft API

&nbsp;  ↓

HTTP Request

&nbsp;  ↓

Supabase REST API

&nbsp;  ↓

PostgreSQL Database

```



---



\## Notes



All database operations (create, read, update, delete) are executed through the Supabase REST endpoints.



Sensitive credentials such as API keys are stored in external configuration files and are not hard-coded in the application.



Supabase REST API was used to simplify database access and avoid exposing direct database credentials.



---



\# Running the Application



\## Requirements



\* Java 8 or higher

\* Maven

\* Anypoint Studio (Mule 4 compatible)



---



\## Steps



1\. Clone the repository



```

git clone <repository\_url>

```



2\. Import project into Anypoint Studio



```

File → Import → Existing Maven Project

```



3\. Run the application



```

Right click project → Run As → Mule Application

```



---



\# Running Tests



The project uses \*\*MUnit\*\* for automated testing.



Run tests using Maven:



```

mvn clean test

```



Test results and coverage reports will be generated automatically after execution.



---



\# Deployment



The application is deployed to \*\*Anypoint Platform\*\*.



Reviewers can access the running API using the deployed public endpoint or by importing the provided Postman collection.



---



\## Environment Configuration



The application uses externalized configuration properties.



Sensitive values such as API keys are not stored in the source code and are instead provided at runtime via Anypoint Platform.



Example properties:



```

supabase.url=https://your-project.supabase.co/rest/v1

supabase.apiKey=${supabaseApiKey}

```



The `supabaseApiKey` value is configured as a secure property or runtime parameter in Anypoint Platform during deployment.



This approach ensures that sensitive credentials are not exposed in the code repository.



---



\# Postman Collection



The repository includes a \*\*Postman collection\*\* together with a \*\*development environment configuration\*\*.



These files allow reviewers to easily import the requests into Postman and test all API endpoints against the deployed environment.



To test the API:



1\. Import the Postman collection from the repository.

2\. Import the provided \*\*Dev Environment\*\* file.

3\. Select the environment in Postman.

4\. Execute the requests.



---



\# Security



The API is secured using \*\*OAuth 2.0\*\*.



\### Scopes



| Scope            | Description                            |

| ---------------- | -------------------------------------- |

| customers:read   | Allows reading customer data           |

| customers:write  | Allows creating and updating customers |

| customers:delete | Allows deleting customers              |



Authentication must be provided in the request using a valid OAuth 2.0 access token.



\### Generating an Access Token



An OAuth 2.0 access token is required to call the API endpoints.



The repository includes a \*\*Postman collection\*\* that contains a request for generating the OAuth 2.0 token.



To obtain a token:



1\. Import the Postman collection from the repository.

2\. Execute the \*\*Get OAuth Token\*\* request included in the collection.

3\. Copy the returned `access\_token`.

4\. Use the token in subsequent API requests in the `Authorization` header.



Example header:



```

Authorization: Bearer <access\_token>

```



The token generation request is preconfigured in the provided Postman collection and uses the development environment variables.



```



\# Additional Notes



\* The project follows the \*\*standard Mule Maven project structure\*\*.

\* No sensitive credentials are stored in the code.

\* Configuration values are externalized in properties files.

\* The API follows REST best practices and standard HTTP response codes.



