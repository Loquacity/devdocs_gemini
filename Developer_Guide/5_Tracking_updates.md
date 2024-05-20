### V. Tracking and Updates

Shippit offers two primary methods for keeping tabs on your shipments: pull-based tracking using the `/track` endpoint and push-based updates via webhooks.

### Pull-Based Tracking (`/track` Endpoint)

This method involves periodically sending requests to the `/orders/{tracking_number}/track` endpoint to fetch the latest status of an order. It's a simple way to get on-demand updates whenever you need them.

#### How to Poll for Updates

1.  **Construct the URL:** Replace `{tracking_number}` with the actual Shippit tracking number of the order you want to track.

2.  **Send a GET request:** Use your preferred HTTP client or library to send a GET request to the constructed URL, including your authentication headers.

3.  **Parse the response:** Shippit will return a JSON response containing the current status of the order, along with a history of tracking events.


You can choose the frequency of your polling based on your needs. For example, you might poll every few hours for standard orders or more frequently for express or priority orders.

#### Mapping Shippit Statuses to Your System

Shippit uses specific status codes to represent the different stages of an order's journey. These statuses might not directly match the terminology used in your own system. Refer to the "Similarities in the UI and API Workflow" documentation for a detailed mapping of Shippit statuses to their corresponding meanings in the Shippit web interface. You'll need to translate these statuses into your own system's equivalents for a seamless user experience.

### Webhooks (Push-Based)

If you need real-time updates on your orders, webhooks are the way to go. Shippit will send a POST request to a URL you specify whenever there's a change in an order's status. This eliminates the need for constant polling and ensures you're always up-to-date.

To set up webhooks, you'll need to configure a webhook URL in your Shippit account settings. The webhook payload will contain detailed information about the order and the specific event that triggered the webhook.

**Note:** Webhooks are a more advanced feature and require you to set up a server endpoint to receive and process the incoming requests.
