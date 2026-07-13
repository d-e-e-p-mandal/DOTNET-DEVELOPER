
# RESTful SERVICES 

**WHAT IS REST?**
- REST = Representational State Transfer
- It is an architectural style used to design web APIs.
- In simple: REST → rules to build APIs using HTTP

**A RESTful service is an API that :**
* Follows REST principles
* Uses HTTP methods
* Uses URLs to represent resources


Example : /api/employees

“employees” = resource


### CORE CONCEPTS OF REST

**Resource :**

- Anything that can be accessed via API

Employee, Product, User


**URI (Uniform Resource Identifier) :**
- Unique address of resource

URL : /api/employees/1


**Representation :**
- Data format of resource
```json
{
  "id": 1,
  "name": "Deep"
}
```
- Formats:
* JSON (most common)
* XML

##### HTTP METHODS (VERY IMPORTANT) :

**GET → Read data :**

GET /api/employees

- Fetch data


**POST → Create data :**

POST /api/employees

- Add new record


**PUT → Update full data :**

PUT /api/employees/1

- Replace data


**PATCH → Partial update :**

PATCH /api/employees/1

- Update specific fields


**DELETE → Remove data :**

DELETE /api/employees/1

- Delete resource


### HTTP STATUS CODES
200 → OK  
201 → Created  
204 → No Content  
400 → Bad Request  
401 → Unauthorized  
403 → Forbidden  
404 → Not Found  
500 → Server Error  


### REST PRINCIPLES
- Stateless
- Each request is independent
- Server does not store client state
- Client-Server
- Frontend ≠ Backend
- Separation of concerns


##### Uniform Interface

Same rules for all APIs

- Example:
GET /employees
POST /employees


##### Resource-Based
- URL represents resource, not action
- Wrong: /getEmployees
- Correct: /employees
- Cacheable : Responses can be cached


### REST API DESIGN RULES
**Use nouns, not verbs :**
- /employees ✔  
- /getEmployees ❌  

**Use plural resources :**
- /employees ✔  
- /employee ❌  

**Use proper HTTP methods :**
- GET    → fetch  
- POST   → create  
- PUT    → update  
- DELETE → delete  

- Use status codes properly

------------------------------------