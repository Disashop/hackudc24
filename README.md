# HackUDC 2024 Forms API

This API provides support for managing forms and creating data based on those forms. It is part of the HackUDC 2024 challenge.

## Purpose

The purpose of this API is to allow developers to obtain a generic form definition, create forms based on those types, and retrieve data from those forms.

## Methods

The API contains the following methods:

- `GET /api/v1/formTypes`: Retrieves available form types.
- `POST /api/v1/formTypes/{form_type_id}`: Get a detailed form type.
- `GET /api/v1/forms`: Retrieves all created forms, optionally filtered by type.
- `POST /api/v1/forms`: Creates a new form based on an existing type.
- `GET /api/v1/forms/{form_id}`: Retrieves a specific form by its ID.

## Usage

Developers can use this API to build applications that require dynamic form management, such as mobile apps that allow users to complete various types of forms.


# Mock server

This API is configured with a mock server, deployed using Postman. This mock server can be used as a basis for mobile application development, although it is not mandatory. Participating teams in the challenge can choose to create their own API or use our API and configure their own mock. Regarding the provided mock, it has the following characteristics:

- It is deployed at https://48fcef17-883f-49d8-8d0f-6a9a559d107b.mock.pstmn.io.
- It simulates being a Raspberry device support system.
- To invoke the mock and obtain the different configured responses, specific headers must be used. The configuration of these headers can be obtained by downloading the Postman collection attached to this repository, although it is summarized here:
    - Any endpoint that does not receive parameters must be invoked by adding the header "mock: 1". This will return the mocked 2XX response. To test error cases, the header "error: 1" can be used.
    - For endpoints that receive identifiers as parameters, headers "form_type_id" or "form_id" must be used. In the case of the former, the mock is configured with IDs 1, 2, and 3, each with a different form type. ID 4 will return a 404 NOT FOUND response. In the case of form_id, values from 1 to 6 are configured, and 7 can be used to obtain a 404 NOT FOUND response.
