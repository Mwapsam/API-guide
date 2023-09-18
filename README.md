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

7. **Corporate List API**

   Endpoint: `/api/corporate/list/`
   - Method: GET
   - Permissions: IsAdmin

     Description: This API allows administrators to retrieve a list of all corporates. It requires JWT authentication for access.

     *Response*
     ## Success Response

     - Status: 200 OK
     - Body: List of corporate objects serialized using `CorporateSerializer`.

       ```[
          {
            "id": 1,
            "name": "Example Corporate 1",
            // Additional corporate information
          },
          {
            "id": 2,
            "name": "Example Corporate 2",
            // Additional corporate information
          },
          // ... more corporate objects
        ]
        ```

8. **Corporate Users List API**
       
     Endpoint: `/api/corporate/users/list/`

   - Method: GET
   - Permissions: IsAdmin

     Description: This API allows administrators to retrieve a list of all corporate users. It requires JWT authentication for access.

     ## Response
     *Success Response*
     - Status: 200 OK
     - Body: List of corporate user objects serialized using CorpUserSerializer.

       ```
               [
                  {
                    "id": 1,
                    "username": "user1",
                    "email": "user1@example.com",
                    // Additional corporate user information
                  },
                  {
                    "id": 2,
                    "username": "user2",
                    "email": "user2@example.com",
                    // Additional corporate user information
                  },
                  // ... more corporate user objects
                ]
       ```
       *Error Response*
       - Status: 401 Unauthorized (if authentication fails)
       - Status: 403 Forbidden (if the user is not an admin)

 9. **Create Payment Page Token API**

    Endpoint: `/api/payment/token/create/`
    
    - Method: POST
      This API allows users to create a payment page token for a specified tier.

    ***Request***
    ```
        {
          "tier_id": 1
        }
    ```
    tier_id: The ID of the tier for which the payment page token should be created.
    
    ***Response***
    *Success Response*
    - Status: 200 OK
    - Body:
      ```
          {
              "transactionToken": "ABCDEF123456"
          }
      ```

    transactionToken: The token for the payment page.
    
    ***Error Response***
    - Status: 400 Bad Request
    - In case of errors, the response will contain an error message.
    
    Note: This API interacts with a payment gateway to create a payment page token. It's essential to handle errors gracefully and provide appropriate error messages and status codes as needed.

 10. **Create Add Card Token API**

     Endpoint: `/api/payment/card/token/create/`

     Method: POST
     This API allows users to create a payment page token for adding a card.
    
     ***Request***
        The request does not require any additional parameters. The user making the request is automatically associated with their account.

     ***Response***
     *Success Response*
     - Status: 200 OK
     - Body:
       ```
           {
              "transactionToken": "ABCDEF123456"
            }
       ```

       transactionToken: The token for adding a card.
       ***Error Response***
        - Status: 400 Bad Request
        - In case of errors, the response will contain an error message.
 
        Note: These payment-related APIs interact with a payment gateway to create tokens. Handle errors gracefully and provide appropriate error messages and status codes as needed.
       
11. **Send OTP API**

    Endpoint: `/api/send-otp/`

    Method: POST
    Permissions: AllowAny
    This API allows sending a One-Time Password (OTP) to a specified mobile number.

    ***Request***
    ```
        {
          "mobile_number": "1234567890",
          "dial_code": "+1"
        }
    ```
    - mobile_number: The mobile number to which the OTP should be sent.
    - dial_code: The dial code or country code for the mobile number.
      
    ***Response***
    *Success Response*
    - Status: 200 OK
    - Body:
    ```
        {
          "success": true
        }
    ```
    - success: Indicates whether the OTP was successfully sent.
    *Error Response*
    - Status: 400 Bad Request
    Note: In case of errors, the response will contain an error message. The API sends an OTP to the provided mobile number and stores it in the database for verification. Handle errors gracefully and provide appropriate error messages and status codes as needed.

12. **Verify OTP API**

    Endpoint: `/api/verify-otp/`
    - Method: POST
    - Permissions: IsAuthenticated
      This API allows users to verify an OTP (One-Time Password) for authentication.

    ***Request***
    ```
        {
          "otp": "123456"
        }
    ```
    - otp: The OTP to be verified.
      
    ***Response***
    *Success Response*
    - Status: 200 OK
    - Body:
      ```
          {
              "success": true
          }
      ```
    - success: Indicates whether the OTP was successfully verified.
    *Error Response*
    - Status: 400 Bad Request
    - In case of errors or incorrect OTP, the response will contain an error message.
    
    Note: Handle OTP verification errors gracefully and provide appropriate error messages and status codes as needed.

14. **Update Mobile Number API**

    Endpoint: `/api/update-mobile-number/`
    
    - Method: POST
    - Permissions: IsAuthenticated
      
     This API allows users to update their mobile number and dial code.
    ```
        {
          "mobile_number": "1234567890",
          "dial_code": "+1"
        }
    ```
    - mobile_number: The new mobile number to be updated.
    - dial_code: The new dial code or country code to be updated.
    ***Response***
    *Success Response*
    - Status: 200 OK
    - Body:
      ```
          {
              "mobile_number": "+11234567890"
          }
      ```
    - mobile_number: The updated mobile number with the new dial code.
    *Error Response*
    - Status: 400 Bad Request
    - In case of errors, the response will contain an error message. Handle errors gracefully and provide appropriate error messages and status codes as needed.

16. **Create Payment Token 2 API**

    Endpoint: `/api/payment/token2/create/`
    - Method: POST
    - Permissions: IsAuthenticated
      This API allows users to create a payment token for a subscription with optional discount code.

    ***Request***
    ```
        {
          "data": {
            "subscription_id": 1,
            "discount_code": "DISCOUNT123"
          }
        }
    ```
    - data.subscription_id: The ID of the subscription for which the payment token should be created.
    - data.discount_code: (Optional) Discount code to be applied.
      
    ***Response***
    *Success Response*
    - Status: 200 OK
    - Body:
      ```
          {
              "transactionToken": "ABCDEF123456"
          }
      ```
    - transactionToken: The token for the payment.
    *Error Response*
    - Status: 400 Bad Request
    - In case of errors, the response will contain an error message.

18. **Verify Payment Token API**

    Endpoint: `/api/payment/token/verify/`
    - Method: POST
    - Permissions: IsAuthenticated
      This API allows users to verify a payment token.
      ```
          {
              "token": "ABCDEF123456"
          }
      ```
    - token: The payment token to be verified.
    ***Response**
    *Success Response*
    - Status: 200 OK
    - Body:
      ```
          {
              "success": true
          }
      ```
      - success: Indicates whether the payment token was successfully verified.
    *Error Response*
    - Status: 400 Bad Request
    - In case of errors, the response will contain an error message.


20. **Create CGrate Payment API**

     Endpoint: `/api/payment/cgrate/create/`
    - Method: POST
    - Permissions: IsAuthenticated
      This API allows users to process a mobile money payment with an optional discount code.

    ***Request***
    ```
      {
          "data": {
            "subscription_id": 1,
            "mobile_number": "1234567890",
            "discount_code": "DISCOUNT123"
          }
        }
    ```
    - data.subscription_id: The ID of the subscription for which the payment should be processed.
    - data.mobile_number: The mobile number for the payment.
    - data.discount_code: (Optional) Discount code to be applied.
      
    ***Response***
    *Success Response*
    - Status: 200 OK
    - Body:
    ```
        {
          "success": true
        }
    ```
    - success: Indicates whether the payment was successfully processed.
    *Error Response*
    - Status: 400 Bad Request
    - In case of errors, the response will contain an error message.




