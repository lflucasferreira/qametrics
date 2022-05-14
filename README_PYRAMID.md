# Test Pyramid

In order to import the Test Pyramid results into the influxDB, first you need to set up your Google credentials. Maybe you will be requested to generate ...

1. Go to [console.cloud.google.com/iam-admin/serviceaccounts](https://console.cloud.google.com/iam-admin/serviceaccounts);
2. Select the project (or create it if you do not have yet)

    ![Pyramid - Google Select Project](resources/pyramid/pyramid_google_service_account_select_project.png)

3. Look for you service account and click on the `Manage keys` option. If you do not have a service account yet, please create one first, then download the file having your keys.

    ![Pyramid - Google Manage Keys](resources/pyramid/pyramid_google_service_account_manage_keys.png)

4. Now that you are in the `Keys` tab, click on the `ADD KEY` button in order to `Create new key`.

    ![Pyramid - Google Create Key](resources/pyramid/pyramid_google_service_account_create_key.png)

5. keep the JSON key type selected and click on the `CREATE` button.

    ![Pyramid - Google Create JSON Key](resources/pyramid/pyramid_google_service_account_create_json_key.png)

6. A JSON file will be downloaded, open it and it will look like the following (private information was removed for security reasons):

    ```json
    {
      "type": "service_account",
      "project_id": "[project_id]",
      "private_key_id": "[private_key_id]",
      "private_key": "-----BEGIN PRIVATE KEY-----\n[private_key]\n-----END PRIVATE KEY-----\n",
      "client_email": "lucasferreira-pyramid@[project_id].iam.gserviceaccount.com",
      "client_id": "[client_id]",
      "auth_uri": "https://accounts.google.com/o/oauth2/auth",
      "token_uri": "https://oauth2.googleapis.com/token",
      "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
      "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/lucasferreira-pyramid%40[project_id].iam.gserviceaccount.com"
    }
    ```

    6.1. Copy all JSON file content;

    6.2. Go to [onlinestringtools.com/escape-string](https://onlinestringtools.com/escape-string) and paste the content in the string section;

      ![Pyramid - Escape String](resources/pyramid/pyramid_escaped_string.png)

    6.3. Now copy the escaped string and paste it into the `GOOGLE_SHEETS_SERVICE_ACCOUNT_KEY` enrivonment variable

    ```string
    {\n      \"type\": \"service_account\",\n      \"project_id\": \"[project_id]\",\n      \"private_key_id\": \"[private_key_id]\",\n      \"private_key\": \"-----BEGIN PRIVATE KEY-----\\n[private_key]\\n-----END PRIVATE KEY-----\\n\",\n      \"client_email\": \"lucasferreira-pyramid@[project_id].iam.gserviceaccount.com\",\n      \"client_id\": \"[client_id]\",\n      \"auth_uri\": \"https://accounts.google.com/o/oauth2/auth\",\n      \"token_uri\": \"https://oauth2.googleapis.com/token\",\n      \"auth_provider_x509_cert_url\": \"https://www.googleapis.com/oauth2/v1/certs\",\n      \"client_x509_cert_url\": \"https://www.googleapis.com/robot/v1/metadata/x509/lucasferreira-pyramid%40[project_id].iam.gserviceaccount.com\"\n    }
    ```

7. Now you need to create your Google Access Token. For that, you will need to request an OAUTH2, fill in the Google Credentials and copy the generate access token to the `GOOGLE_SHEETS_ACCESS_TOKEN` environment variable. Follow the instructions below to create your Google Client ID and Secret:

    7.1. Visit the [console.developers.google.com/apis](https://console.developers.google.com/apis), select the project (otherwise, create one);

    7.2. Click on `Credentials` option, then click on `Create Credentials` button;

      ![Pyramid - Create OAuth Client ID](resources/pyramid/pyramid_google_credentials_create_oauth_client_id.png)

    7.3. Select `Web application` in the `Application type` field and set a name for your client ID. Example: `QA Metrics`.

      ![Pyramid - Create OAuth Client ID](resources/pyramid/pyramid_google_credentials_create_oauth_client_id_step2.png)

    7.4. At the page bottom, click `ADD URI` and type in `https://www.getpostman.com/oauth2/callback`, then click on the `CREATE` button.

      ![Pyramid - Create OAuth Client ID](resources/pyramid/pyramid_google_credentials_create_oauth_client_id_step3.png)

    7.5. Now download your credential file or simply copy your `Client ID` and `Client Secret` content to the Postman request in order to request your Account Token *manually*.

      ![Pyramid - Create OAuth Client ID](resources/pyramid/pyramid_google_credentials_create_oauth_client_id_step4.png)

    7.6. The downloaded credential file will look like the following (private information was removed for security reasons):

    ```json
    {
      "web": {
        "client_id":"[client_id].apps.googleusercontent.com",
        "project_id":"[project_id]",
        "auth_uri":"https://accounts.google.com/o/oauth2/auth",
        "token_uri":"https://oauth2.googleapis.com/token",
        "auth_provider_x509_cert_url":"https://www.googleapis.com/oauth2/v1/certs",
        "client_secret":"[client_secret]",
        "redirect_uris":["https://www.getpostman.com/oauth2/callback"]
        }
    }
    ```

8. Generate your Google OAuth Token in Postman, using the request `Generate Google OAuth2` [you just need to do it only once].

    8.1. In `Authorization` tab, insert your `Client ID` and `Client Secret` in the highlighted fields and click on `Get New Access Token`.

      ![Pyramid - Create OAuth Client ID](resources/pyramid/pyramid_postman_request_oauth2.png)

    8.2. A new popup window will be open and you just need to login to it by entering your email address and your password.

      ![Pyramid - Postman Login Email](resources/pyramid/pyramid_postman_google_login_email.png)

      ![Pyramid - Postman Login Password](resources/pyramid/pyramid_postman_google_login_password.png)

    8.3. Click on `Allow` button in order to authorize the Postman to request a new access token.

      ![Pyramid - Postman Login Email](resources/pyramid/pyramid_postman_google_login_allow.png)

    8.4. If everything went well, then you will see this screen informing that the authentication is complete.

      ![Pyramid - Postman Login Success](resources/pyramid/pyramid_postman_google_login_success.png)

    8.5. Now you just need to copy your access token and paste it into the `GOOGLE_SHEETS_ACCESS_TOKEN` environment field.

      ![Pyramid - Postman Login Success](resources/pyramid/pyramid_postman_manage_access_tokens.png)

Now you are good to go!
