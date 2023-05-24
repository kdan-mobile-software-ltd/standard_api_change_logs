# Ver.3.3.2
## CHANGE LOGS

### Released Date

- Production Env: 2023/05/25
- Sandbox Env: 2023/05/24

### API Updated

Add `reviewed_by` parameter in following APIs:
- Part I. Admin
    - Task
        - `POST` Create Task
        - `POST` Create Template

# Ver.3.3.1
## CHANGE LOGS

### Released Date

- Production Env: 2023/03/24
- Sandbox Env: 2023/02/24

### New APIs

- Part I. Admin
  - Task
    - `POST` Review Task
        - To check the value filled in fields by signers and determine to pass or return to the signer.
    - `POST` Review Finish
        - The signer confirms the check result and finishes the sign stage.

### API Updated
- Part I. Admin
  - Task
    - `GET` Read Task
      - Moving `Client`, `IP-Address` from query parameters to headers.
      - Adding new optional parameter `with_signature_infos` and an example for this. You can pass `true` to the parameter to obtain the signature fields info in the response.


# Ver.3.3.0
## CHANGE LOGS

### Released Date

- Production Env: 2022/11/03
- Sandbox Env: 2022/10/03

### New APIs

- Part I. Admin
    - Signature
      - `POST` Create Stamp
          - Using a raw image to create a new stamp signature that can be used to fill in a signature field.

      - `DELETE` Delete Signatures
          - To delete the specified signatures.

### API Updated
- Part I. Admin
    - Task
        1. `POST` Quick Create Task (Create by the Template)
            - return an error `400934 template_need_sms_verify`,
              if using the template in which signers should be verified with SMS OTP and not providing the signer's phone in the request body.

### Postman Document Updated
- Part II. Group
  - Callback Event
    1. Add `digit_cert_task_uploaded` event
    2. Add `digit_cert_audit_trail_uploaded` event
    > You can trigger some actions when receiving these 2 events, such as downloading the completed task file.


# Ver.3.2.0
## CHANGE LOGS

### Released Date

- Production Env: 2022/09/15
- Sandbox Env: 2022/08/10

### New APIs

- `POST` Share Sign Link
  - Let the sign task owner obtain each stage's sign link, which is as same as the email quick sign link. (Default 2 days expired)

### API Updated
- Part I. Admin
    - Task
      1. `POST` Create Task
         - Remove `need_otp_verify` in `meta_data_object`
         - Add `verify` in `stage_object`
         - Add a new OTP verification type: `sms`. It can be configured separately from the email type or set simultaneously.

### API Bug Fixed
- Part I. Admin
    - Task
      1. `GET` Read Task
         - Change 2 parameters in the request body to query parameters.
         - Add a new response of the `400048` error code, representing that the query parameter `client` is invalid or not provided.
      2. `POST` Create Task, `POST` Quick Create Task (Create by the Template)
         - Check if email format is valid
           - Add a new response of `400220` error code, representing that the email of signer or cc user is invalid.

### API Deprecated
- Part I. Admin
    - Task
        1. `GET` Share Link v3

### Postman Document Updated
- Update preparing environment (https://dottedsign.preparing.kdanmobile.com/) => sandbox environment (https://dottedsign-api.qa.kdanmobile.com/)
- To comply with the Restful API style, we let all GET API requests to use `query params` instead of JSON body.
    **Notice: Incorrect settings will cause the request to fail.**
  1. `GET` Audit Trails PDF File
  2. `GET` Audit Trails Raw Data
  3. `GET` Read Task
  4. `GET` Search Task
  5. `GET` Task List
  6. `GET` Task List (Admin)
  7. `GET` Single Template
- Limit the query parameter `per_page` to 20. Passing a number greater than 20 will be recognized as 20.
  1. `GET` Search Task
  2. `GET` Task List
  3. `GET` Task List (Admin)
  4. `GET` Template List
- Typo
  1. `GET` Audit Trails PDF File: task_id => id

# Ver.3.1.5
## CHANGE LOGS

### Released Date

- Preparing Env: 2021/11/3
- Production Env: 2021/11/8

### New APIs

- `POST` Quick Create Task (Create by the Template)
- `GET` Audit Trials Raw Data
### New Features (Update Existing APIs)

For task and template features:
- Custom message (message and completed_message) and related settings.
- Sign field options settings.
- Sign stage attachment settings.

We add new features in Standard API, here is the renewed API's description and example list below.

- Part I. Admin
  - Task
    1. `POST` Create Task 
    2. `GET` Read Task
    3. `PUT` Sign Task
  - Template
    1. `POST` Create Template
    2. `GET` Template List
    3. `GET` Single Template
    4. `PUT` Update Template
- Part II. Group
  - Callback Event

### API Bug Fixed

- `GET` Search Task
  - Also renewed the description and examples.

### Change API Doc Name

> The API route is the same, only changed Postman's API description.

- `GET` Audit Trail => `GET` Audit Trails PDF File
- `POST` Resend Signer => `POST` Resend Request to Signer

# Ver.3.1.4

## CHANGE LOGS

1. Renew Login / Refresh API 200 ok response example.
2. Modify API descriptions to new preparing website.
3. Renew `GET` Template List API for missing path parameters description and example.
4. Renew `POST` Create Task API deadline for not expired time integer.

# Ver.3.1.3

## CHANGE LOGS

1. Part I. Admin => Task => POST Resend Signer
    - Add new API for resending email to signer for notification.

# Ver.3.1.2

## CHANGE LOGS

1. Part I. Admin => Task => POST Create Task
    - Remove the input parameter `source`.
2. Part II. Group All APIs must use secret_key to request only.
3. For security reasons, we provide another new api_key call `secret_key`. To know how and when to use `api_key` or `secret_key`, please check the **Developer Guide**.

# Ver.3.1.1

## CHANGE LOGS

1. Add the embedded iframe src URL examples
2. Move all what the embedded src URL APIs called into Reference folder.
    - You don't need to understand the whole APIs how to work in the embedded mode, just embedded it and it will work available.

# Ver.3.1.0

## CHANGE LOGS

1. Updated the sign_host Enterprise API to the v3 route.
   1. sign_host path is updated. However, request headers, parameters and response body still same:
        - older version path (`deprecate`): **{{sign_host}}/api/v2/enterprise/**
        - new v3 path: **{{sign_host}}/api/enterprise/v3/**
    2. If your are use v2 **Part I. Admin/Task `GET` Single Task API**, it will not support at v3 API. 
        - Change to **Part I. Admin/Task `GET` Read Task API** instead.
> Note: We still keep all old version API for using, but they will **deprecate no longer**.
2. Add new V3 API for embedded mode.
    - We add **Part IV. Embedded** and **Part V. File** sections. You can use those APIs to embedded kiosk mode in your service.
3. Updated some API descriptions and examples


# Ver.3.0.1

## CHANGE LOGS

1. New Feature for Search Key!!!
    - Now you can do more things by standard api!
```
You can add the search key to the textfield when creating the task. 
Signer filled value on the textfield is the search value. 
Then, you can use search key and search value at search API to find target tasks.
```
---

- New API `POST Create Template` for creating a template. You can add the search key when creating template.
- New API `PUT Update Template` for updating the template setting. You can modify the search key when updating template.
- New API `GET Search Task` for searching the tasks by search key and value.

2. We can do better for API document.
    - Renew response example (200 OK) at `GET Template List` API and description for search key feature.
    - Renew response example (200 OK) at `GET Single Template` API and description for search key feature.
    - Renew description at `GET Task List` and `GET Task List (Admin)` APIs.
    - Add a new response example (200 OK) at `POST Create Task` which is reference `GET Single Template`  200 OK response example.
    - Update `POST Modify Group Information` for more clear description.
    - Update `POST Refresh Token` for adding {{data_center_host}} 401 error response which you need to request the refresh.
    - Update `Callback event` description for guiding user to check Examples of callback events.


# Ver.3.0.0

## CHANGE LOGS

1. Each APIs will require the api-key at the header and change to new api path.
    - We use api-key for identify your group to improve security.


```
If you are using the older version of kdan standard api, please contact our Enterprise Account Manager for requesting your group's api-key.
```


> NOTICE: For **old version users**, it will affect:
>
> Must require api-key at header if you are using them.
>
> - `POST` {{data_center_host}}/api/v3/file_objects/indirect_upload
> - `GET` {{sign_host}}/api/v2/enterprise/sign_tasks/{{completed_task_id}}

- Change to the new api path.
    - APIs will change to the enterprise url path and must require api-key at header, too.
- Modify the response format
    - `{{sign_host}}/api/v2/sign_tasks` => {{sign_host}}/api/v2/enterprise/sign_tasks
    - response {category} property will not be supported recently, please using `tasks` property instead! For more detail please check this API description.

2. Sign Event Callback 
    - Kdan Standard API now supports webhooks to easily integrate external applications to your server.
    - If your group member is the task owner or signer, we will send the task sign events for you.
    - Outgoing webhooks will send an HTTP POST request to a valid callback url using JSON format. 
3. New APIs for Group Control
    - Now you can operate your own group by standard api!
        - Get your group detail information.
        - Modify your group name or add callback url.
       - Regenerate api-key if you need.