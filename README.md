# HackUDC 2024 Forms API

This API provides support for managing dynamic forms, allowing developers to create and retrieve
forms based on predefined types. It is designed to be used in mobile applications that require the
creation and management of dynamic forms, such as those used in data collection and surveys.

It is part of the HackUDC 2024 challenge.

## Usage

The API is provided as as an OpenAPI 3.0 specification that can be used to generate server and
client
code in a variety of languages or as a reference for manual implementation or extension.

The specification is available in the `openapi.yaml` file in the `rest` directory of this
repository.

### API Endpoints

The API contains the following methods:

- `GET /api/v1/formTypes`: Retrieves available form types.
- `POST /api/v1/formTypes/{form_type_id}`: Get a detailed form type.
- `GET /api/v1/forms`: Retrieves all created forms, optionally filtered by type.
- `POST /api/v1/forms`: Creates a new form based on an existing type.
- `GET /api/v1/forms/{form_id}`: Retrieves a specific form by its ID.

### Mock server

A testing mock server deployed with Postman is also provided, and can be used as a basis for mobile
application development. Teams can choose to use the provided API and mock, configure their own
mock, or even to modify
or extend the API if they wish to do so, as long as the basic functionality is maintained.

Regarding the provided mock, it has the following characteristics:

- It is deployed at https://c48b6359-2b3c-4ab5-829b-32afa3da6640.mock.pstmn.io.
- It simulates being a Raspberry device support system.
- To invoke the mock and obtain the different configured responses, specific headers must be used.
  The configuration of these headers can be obtained by downloading the Postman collection attached
  to this repository, although it is summarized here:
    - Any endpoint that does not receive parameters must be invoked by adding the header "mock: 1".
      This will return the mocked 2XX response. To test error cases, the header "error: 1" can be
      used.
    - For endpoints that receive identifiers as parameters, headers "form_type_id" or "form_id" must
      be used. In the case of the former, the mock is configured with IDs 1, 2, and 3, each with a
      different form type. ID 4 will return a 404 NOT FOUND response. In the case of form_id, values
      from 1 to 6 are configured, and 7 can be used to obtain a 404 NOT FOUND response.

#### Setting up the mock server with Postman

To deploy your own mock server with Postman, you can follow these steps:

1. Create a Postman account if you don't have one.
2. Download the Postman collection and environment from this repository (`postman` directory).
3. Import the collection into your Postman account.
4. Click on the "..." button next to the collection name and select ***Mock collection***.
5. Type a name for your mock server and click ***Create Mock Server***.
6. Click on ***Edit configuration***, check the ***Headers*** option on the bottom of the page, and
   add the following headers:
    - `mock`, `error`, `form_type_id`, and `form_id`
7. Update your environment variables to use the URL from your newly created mock server.
8. You are ready to start using your mock server. Open the collection and start making requests
   passing the required headers.

## Form model

The proposed form model describes the various fields, groups, and validations that compose a form,
providing insights into how data is organized and processed. Understanding the Form Model is
essential for developers looking to interact with the API for creating and managing dynamic forms.

### Form schema

- **form_type_id:** Unique identifier of the form type.
- **form_type_name:** Name of the form type.
- **form_type_description:** Description of the form type.
- **title_field:** Title of the form.
- **form_fields:** List of fields that compose the form.
- **form_groups:** List of groups that organize the fields within the form.

### Form field schema

- **field_id:** Unique identifier of the field.
- **field_name:** Name of the field.
- **field_type:** Type of the field (text, number, date, selection, etc.).
- **field_order:** Order of the field within the form.
- **field_required:** Indicates if the field is required.
- **field_description:** Description of the field.
- **field_readonly:** Indicates if the field is read-only.
- **field_default_value:** Default value of the field.
- **field_group:** Identifier of the group the field belongs to.
- **field_dependent_on:** Defines the dependency of the field on another field.
- **field_validations:** List of validations applicable to the field. For fields that require
  options, this field will contain the list of options in the `options` attribute.

### Field Groups

Optionally, fields can be organized into groups to provide a better user experience and
organization. When this happens, the `form_groups` attribute will contain a list of groups, each
with the
following attributes:

- **group_id:** Unique identifier of the group.
- **group_name:** Name of the group.
- **group_description:** Description of the group.
- **group_order:** Order of the group within the form.

Additionally, the `field_group` attribute of each field will contain the identifier of the group the
field belongs to.

### Dependent Fields

Fields can be dependent on other fields, meaning that their visibility or required status is
dependent on the value of another field. This is defined by the `field_dependent_on` attribute,
which contains the identifier of the field the current field is dependent on and the value that
triggers the dependency:

- **field_dependent_on:**
    - **field_id:** Identifier of the field the current field is dependent on.
    - **field_value:** Value that triggers the dependency.

### Field Validations

- **field_validations:** List of validations applicable to the field.

### Available Field Types

- **text:** Allows input of text.
- **number:** Allows input of numeric values.
- **date:** Allows selection of a date.
- **select:** Presents a list of options for selection.
- **checkbox:** Allows selection of boolean values.

These field types cover a variety of data input and selection needs within the form, providing
flexibility and functionality to effectively capture information, but can be extended to include
additional types as needed.


