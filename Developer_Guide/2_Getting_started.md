### II. Getting Started

Before you can start sending requests to the Shippit API, you'll need to set up a few things:

### Creating a Shippit Account

If you don't already have one, head over to the Shippit website and create a new account. This will give you access to the Shippit dashboard, where you can manage your settings, view your orders, and more.

### Obtaining API Keys and Secrets

To interact with the API, you'll need a set of API credentials:

1.  **API Key:** This is a public identifier for your Shippit account.

2.  **API Secret:** This is a confidential value used to authenticate your API requests.


You can find your API Key in your Shippit account settings under **Settings > Integrations**.

Shippit allows you to create multiple API secrets, each with its own set of permissions. This is useful if you want to restrict access to certain parts of the API for different applications or users. To create a new API secret, click on the "+ New API Secret" button in the Integrations settings.

**Important Note:** The API Secret is only displayed once during creation. Make sure to copy it and store it securely, as you won't be able to retrieve it later.

### Authentication

Shippit's API uses Bearer authentication. This means you need to include your API Secret in the `Authorization` header of every request you send. The header should look like this:

```
Authorization: Bearer YOUR_API_SECRET
```

**Important Security Note:** Do not include your API Secret directly in the URL of your requests. This is considered insecure and is deprecated by Shippit.

### Common Authentication Errors and Troubleshooting

If you encounter authentication errors, double-check the following:

*   **Correct API Secret:** Ensure you're using the correct API Secret and that it hasn't expired.

*   **Authorization Header:** Verify that the `Authorization` header is included in your request and formatted correctly.

*   **API Key Activation:** Make sure you've added a valid credit card to your billing details in Shippit to activate your API key.


If you're still having trouble, refer to the "Troubleshooting" section of this guide or contact Shippit support for assistance.
