### VI. Advanced Topics

This section covers more specialized use cases and troubleshooting techniques to help you get the most out of the Shippit API.

### Returns and Return Labels

Returns are an inevitable part of e-commerce, and the Shippit API aims to make them less of a headache. However, it's important to understand that the API's role in returns is somewhat limited.

#### Different Return Types and Their API Usage

Shippit distinguishes between several types of returns:

*   **Merchant-Initiated Returns:** The merchant creates a return label for the customer.

*   **Customer-Initiated Returns:** The customer requests a return through the Shippit Returns Portal.

*   **Automatic Returns:** Triggered by specific events (e.g., failed delivery).


The API is primarily used for creating return orders (`/returns/order` endpoint) and fetching order details for return requests (`/returns/request` endpoint). The exact flow and required parameters depend on the return type.

#### Limitations of the API in the Returns Process

While the API helps initiate returns within Shippit's system, it doesn't cover the entire returns process. For example:

*   **Customer Communication:** You'll likely need to handle communication with the customer outside of the API (e.g., sending return instructions).

*   **Physical Return of Goods:** The API doesn't manage the actual shipment of the returned item back to you.

*   **Refunds and Exchanges:** Processing refunds or exchanges typically happens within your own system, not through the Shippit API.


### Error Handling and Troubleshooting

Even with the best documentation, you might encounter errors when integrating with the Shippit API. Here's how to tackle them:

#### Common Error Codes and Their Meanings

Shippit's API returns standard HTTP status codes (e.g., 400 Bad Request, 404 Not Found), but it also has custom error codes in the response body. Refer to the API documentation for a complete list of error codes and their descriptions. Some common ones include:

*   `order_cannot_be_cancelled`: The order is in a state where it cannot be canceled.

*   `order_not_found`: The specified order tracking number doesn't exist.

*   `label_failed_rules_engine`: The order failed to meet your allocation rules.

*   `address_invalid`: The provided delivery address is invalid.

The most common Shippit error codes, excluding HTTP errors, are:

| Error Code | Description | Resolution |
|---|---|---|
| `order_cannot_be_cancelled` | The order is in a state where it cannot be canceled (e.g., already in transit). | If the order has not been picked up, contact Shippit customer service for assistance. |
| `order_not_found` | The specified order tracking number cannot be found in the Shippit system. | Double-check the tracking number for accuracy. If the issue persists, contact Shippit support. |
| `label_failed_rules_engine` | The order has not been allocated a valid courier due to allocation rules. | Review your allocation rules in Shippit settings and ensure they are configured correctly. |
| `label_failed_tracking_order` | You are trying to generate a label for a tracking order, which is not supported. Shippit only provides tracking for such orders. | If you need a label, generate it outside of Shippit and then create a tracking order. |
| `address_invalid` | The provided delivery address is invalid. | Double-check the address for accuracy and correct any errors. |
| `label_failed_order_processing` | The order is still being processed and cannot be labeled yet. | Wait for a few moments and try again. If the issue persists, contact Shippit support. |
| `label_failed_missing_courier` | No courier has been assigned to the order yet. | Ensure the order has been processed and allocated a courier. You can check the order status using the tracking endpoint. |
| `label_failed_invalid_quote` | The order has no valid quotes available. | Review your courier settings and ensure that at least one courier is enabled and can service the delivery address. |
| `label_failed_still_generating` | The label is still being generated. | Wait for a few moments and try again. |
| `label_failed_failed_request` | The label generation request failed. | Contact Shippit support for assistance. |
| `label_failed_courier_deprecated` | The assigned courier is no longer supported. | Update the order with a different courier allocation or contact Shippit support. |
| `order_not_available_to_label` | The order has not been processed yet and cannot be labeled. | Wait for the order to be processed and try again. |


#### Debugging Strategies

*   **Check the Response Body:** The error response usually contains a detailed message explaining the issue.

*   **Validate Your Request:** Double-check that your request payload matches the expected format and includes all required fields.

*   **Inspect API Logs:** If available, review your API logs to see the exact request and response details.

*   **Contact Shippit Support:** If you're unable to resolve the issue, don't hesitate to reach out to Shippit's support team for assistance.


### Whitelisting and Security

If your systems have strict security measures like firewalls, you'll need to whitelist Shippit's IP addresses and URLs to ensure smooth communication with the API. Refer to the "Whitelisting Shippit" documentation for the list of IP addresses and URLs to whitelist.

### Best Practices for Integration

*   **Use a Staging Environment:** Shippit provides a staging environment for testing your integration before going live.

*   **Handle Errors Gracefully:** Implement robust error handling in your code to catch and manage API errors effectively.

*   **Follow Rate Limits:** Be mindful of Shippit's rate limits to avoid getting temporarily blocked.

*   **Keep Your Integration Up-to-Date:** Shippit may update its API from time to time. Stay informed about changes and update your integration accordingly.


By following these advanced tips and best practices, you can ensure a smooth, secure, and reliable integration with the Shippit API.
