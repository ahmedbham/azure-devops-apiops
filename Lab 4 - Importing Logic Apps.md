# Lab 4: Importing Consumption and Standard Logic Apps to Azure API Management

## Creating a Consumption Logic App with HTTP Trigger

1. **Open Azure Portal**
    Navigate to the [Azure Portal](https://portal.azure.com/).

2. **Create a New Logic App**
    1. In the left-hand menu, select **Create a resource**.
    2. Search for **Logic App** and select **Logic App** from the results.
    3. Click **Create**.

3. **Configure Logic App**
    1. Provide a **Name** for your Logic App.
    2. Select your **Subscription** and **Resource Group**.
    3. Choose the **Location** for your Logic App.
    4. Click **Review + create** and then **Create**.

4. **Add HTTP Trigger**
    1. Once the Logic App is created, click on **Logic App Designer**.
    2. In the designer, select **When an HTTP request is received** trigger.

5. **Define the Response**
    1. Click on **+ New step**.
    2. Search for **Response** and select the **Response** action.
    3. Set the **Status Code** to `200`.
    4. In the **Body** field, enter the text: `I received the message`.

6. **Save the Logic App**
    Click **Save** to save your Logic App.

Your Consumption Logic App is now ready and will respond with "I received the message" when triggered via HTTP.

## Creating a Standard Logic App with HTTP Trigger
1. **Open Azure Portal**
    Navigate to the [Azure Portal](https://portal.azure.com/).

2. **Create a New Logic App**
    1. In the left-hand menu, select **Create a resource**.
    2. Search for **Logic App (Standard)** and select **Logic App (Standard)** from the results.
    3. Click **Create**.

3. **Configure Logic App**
    1. Provide a **Name** for your Logic App.
    2. Select your **Subscription** and **Resource Group**.
    3. Choose the **Location** for your Logic App.
    4. Click **Next: Hosting**.
    5. Select the **Plan type** and **SKU**.
    6. Click **Review + create** and then **Create**.

4. **Add HTTP Trigger Using Template**
    1. Once the Logic App is created, click on **Logic App Designer**.
    2. In the designer, select **Templates**.
    3. Search for **Request-Response: Receive and respond to messages over HTTP or HTTPS** and select the template.

5. **Configure the Template**
    1. Follow the prompts to configure the HTTP trigger and response actions as needed.
    2. Set the **Status Code** to `200`.
    3. In the **Body** field, enter the text: `I received the message`.

6. **Save the Logic App**
    Click **Save** to save your Logic App.

Your Standard Logic App is now ready and will respond with "I received the message" when triggered via HTTP.



## Importing Consumption Logic Apps to Azure API Management

### 1. Open Azure Portal
Navigate to the [Azure Portal](https://portal.azure.com/).

### 2. Go to API Management Service
Select your API Management instance.

### 3. Add a New API
1. In the left-hand menu, select **APIs**.
2. Click on **+ Add API**.
3. Choose **Logic App** from the options.

### 4. Select Logic App
1. In the **Logic App** section, click on **Browse**.
2. Select your Consumption Logic App from the list.
3. Click **Select**.

### 5. Configure API Settings
1. Provide a **Display name** for your API.
2. Set the **Name** and **API URL suffix**.
3. Click **Create**.

### 6. Review and Save
Review the settings and click **Save**.

### 7. Test the API
1. Navigate to the **Test** tab.
2. Select an operation and click **Send** to test the API.

## Importing Standard Logic Apps to Azure API Management
### 1. Open Azure Portal
Navigate to the [Azure Portal](https://portal.azure.com/).

### 2. Go to API Management Service
Select your API Management instance.

### 3. Add a New API
1. In the left-hand menu, select **APIs**.
2. Click on **+ Add API**.
3. Choose **Blank API** from the options.

# Steps to Import Logic App (Standard) into Azure API Management

To import a Logic App (Standard) into Azure API Management (APIM), follow these steps:

1. **Manual Registration**
   - Since direct import from “Create from Azure Resource” is not available for Logic App (Standard), you will manually register the Request trigger URL from workflows as a blank API in APIM.

2. **Divide the Request URL**
   - Split the Logic Apps Workflow URL into two parts:
     - **Part 1**: `https://stdla1.azurewebsites.net:443/api/`
     - **Part 2**: `/test2/triggers/manual/invoke?api-version=2020-05-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=<123abc>`

3. **Configure Backend**
   - Place **Part 1** URL into either:
     - Webservice URL
     - Backend HTTP(s) endpoint

4. **Set Target**
   - Select target as HTTP(s) endpoint, click on override, and provide the first part of your request URL.

5. **Add Frontend URL**
   - Add **Part 2** URL into the frontend section.

6. **Testing**
   - Upon testing, you should receive a **200 OK** response.


Your Standard Logic App is now imported to Azure API Management and can be accessed via the API endpoint.


## Conclusion
You have successfully imported a Consumption Logic App to Azure API Management.
