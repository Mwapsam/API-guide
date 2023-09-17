# Smart Saver Zambia API


# API Documentation For The Corporate App

### Customer Login API

Endpoint: 

    /api/customer/login/

- ***Method: POST***
- ***Permissions: AllowAny***

This API allows customers to log in to their accounts. It requires the following parameters in the request body:

- email: The email address of the customer.
- password: The password for the customer's account.
- corporate_id: The ID of the associated corporate.

**Request:**

        {
          "email": "customer@example.com",
          "password": "password123",
          "corporate_id": 123
        }

**Response:**

- Status: 200 OK
- Body:

        {
          "message": "Login successful.",
          "customer": {
            "id": 1,
            "name": "John Doe",
            "email": "customer@example.com",
            "corporates": [123],
            ...
          },
          "token": "ABCDEF123456"
        }


- Status: 400 Bad Request
- Body:

        {
          "message": "Invalid corporate."
        }

- Status: 401 Unauthorized
- Body:

        {
          "message": "Invalid email or password."
        }


## Corporate User Login API

Endpoint: 

          /api/corporate-user/login/

- ***Method: POST***
- ***Permissions: AllowAny***

This API allows corporate users to log in to their accounts. It requires the following parameters in the request body:

- email: The email address of the corporate user.
- password: The password for the corporate user's account.

**Request:**

            {
              "email": "user@example.com",
              "password": "password123"
            }

**Response:**

- Status: 200 OK
- Body:

        {
          "detail": "Login successful",
          "token": "ABCDEF123456"
        }

- Status: 404 Not Found
- Body:

        {
          "detail": "No CorporateUser found"
        }

## Corporate User Logout API
**Endpoint:** 

      /api/corporate-user/logout/

- ***Method: POST***

This API allows corporate users to log out from their accounts. It requires authentication with a valid token.

**Request:**
- No request body is required.

**Response:**
- Status: 200 OK
- Body:

        {
          "detail": "Logout successful"
        }

## Corporate User Create API
**Endpoint:** 

    /api/corporate-user/create/

- ***Method: POST***

This API allows creating a new corporate user. It requires authentication as a staff user.

**Request:**

        {
          "email": "user@example.com",
          "password": "password123",
          ...
        }

***Note: The exact fields required may vary based on your implementation.***

**Response:**

- Status: 201 Created
- Body:

        {
          "detail": "Corporate user created successfully",
          "corporate_user": {
            "id": 1,
            "email": "user@example.com",
            ...
          }
        }

- Status: 401 Unauthorized
- Body:

      {
        "detail": "Unauthorized"
      }
- Status: 400 Bad Request
- Body:

      {
        "field_name": [
          "Error message 1",
          "Error message 2"
        ],
        ...
      }

## Corporate Create API
**Endpoint:** 

      /api/corporate/create/

- ***Method: POST***

This API allows creating a new corporate.

**Request:**

      {
        "name": "ABC Corporation",
        "address": "123 Main Street",
        "phone": "0965234432",
        "email": "newcorporate@smartsaver.com",
        "owner": 17
      }

**Response:**
- Status: 201 Created
- Body:

      {
        "message": "Corporate created successfully",
        "corporate": {
          "id": 1,
          "name": "ABC Corporation",
          ...
        }
      }
- Status: 400 Bad Request
- Body:

      {
        "field_name": [
          "Error message 1",
          "Error message 2"
        ],
        ...
      }

## Customer Registration API
**Endpoint:** 

    /api/customer/register/

***- Method: POST***

This API allows registering a new customer. It does not require authentication.

**Request:**

    {
      "email": "user@example.com",
      "password": "password123",
      "corporate_id": 1,
      "first_name": "Sam",
      "last_name": "Mwape"
    }

**Response**
- Status: 201 Created
- Body:

      {
        "message": "Customer registration successful."
      }

- Status: 400 Bad Request
- Body:

      {
        "message": "Invalid corporate."
      }

## User CSV Upload API
**Endpoint:** 

    /api/bulk-customer-upload/

- **Method: POST**

This API allows uploading a CSV file containing user data and creating multiple users from it.

Request
The request should be a `multipart/form-data` request with the following parameters:

- csv_file: The CSV file containing user data.
- corporate_id: The ID of the corporate to associate the users with (The one uploading the file).

**Response**
- Status: 201 Created
- Body:

      {
        "message": "Users created successfully.",
        "users": [
          {
            "id": 1,
            "username": "user1",
            ...
          },
          {
            "id": 2,
            "username": "user2",
            ...
          },
          ...
        ]
      }
      
- Status: 400 Bad Request
- Body:

      {
        "field_name": [
          "Error message 1",
          "Error message 2"
        ],
        ...
      }

### Get Corporate Customers API

**Endpoint:**

      /api/corporate/{corporate_id}/customers/

- ***Method: GET***

This API allows retrieving the customers associated with a corporate.

**Parameters:**
- corporate_id (integer): The ID of the corporate.

**Response**

- Status: 200 OK
- Body:

      {
        "customers": [
          {
            "id": 1,
            "name": "John Doe",
            "email": "john.doe@example.com",
            ...
          },
          {
            "id": 2,
            "name": "Jane Smith",
            "email": "jane.smith@example.com",
            ...
          },
          ...
        ]
      }

### Delete Customer API
**Endpoint:**

    /api/customer/{customer_id}/delete/

- ***Method: DELETE***

This API allows deleting a customer.

**Parameters:**

- customer_id (integer): The ID of the customer to be deleted.

**Response**
- Status: 204 No Content

## **APP API IN REST**

1. **Register User API**

   Endpoint: `POST /api/register/`

   Request Body:
   ```
   {
     "first_name": "John",
     "last_name": "Doe",
     "notification_id": "some_notification_id",
     "email": "john.doe@example.com",
     "password": "password123"
   }
   ```

   Description: This API allows a user to register a new account. It creates a new user with the provided details and sends a verification email.

2. **Login User API**

   Endpoint: `POST /api/login/`

   Request Body:
   ```
   {
     "username": "john.doe@example.com",
     "password": "password123",
     "device_id": "some_device_id"
   }
   ```

   Description: This API allows a user to authenticate and obtain an access token. It verifies the user's credentials and returns an access token for subsequent API requests.

3. **Forgot Password API**

   Endpoint: `POST /api/forgot-password/`

   Request Body:
   ```
   {
     "email": "john.doe@example.com"
   }
   ```

   Description: This API initiates the password recovery process for a user. It sends a password reset link to the user's email address.

4. **Create Support Ticket API**

   Endpoint: `POST /api/support-tickets/`

   Request Body:
   ```
   {
     "phone_number": "1234567890",
     "message": "I need help with..."
   }
   ```

   Description: This API allows an authenticated user to create a support ticket. It associates the ticket with the user's customer account and stores the provided phone number and message.

5. **Upload Image API**

   Endpoint: `PUT /api/upload-image/`

   Request Body:
   ```
   {
     "image": <image_file>
   }
   ```

   Description: This API allows an authenticated user to upload an image. It updates the user's customer account with the uploaded image.

6. **Invite Member API**

   Endpoint: `POST /api/invite-member/`

   Request Body:
   ```
   {
     "email": "member@example.com"
   }
   ```

   Description: This API allows an authenticated user to invite a member to their account. It sends an invitation email to the provided email address.

Note: For all the APIs, make sure to include the access token in the request headers:
```
Authorization: Bearer <access_token>
```

```docker-compose -f docker-compose.dev.yml exec db psql -d smartsaver_db -U smartsaver -W```

```ALTER TABLE erp_customer ALTER COLUMN segment DROP NOT NULL;```

```ALTER TABLE erp_customer DROP COLUMN segment_id;```
