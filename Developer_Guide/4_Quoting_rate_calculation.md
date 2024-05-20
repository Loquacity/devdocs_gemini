### IV. Quoting and Rate Calculation

The Shippit API provides flexibility in how you handle shipping rates for your customers. You can either use the API to get real-time quotes from carriers or set up flat rates within your own system.

### /quotes Endpoint Usage

The `/quotes` endpoint is your tool for fetching live shipping rates from Shippit's integrated carriers. Here's how it works:

1.  **Send a POST request:** Structure your request payload with the necessary details, including:

    *   `dropoff_location`: The delivery address (suburb, postcode, state, country).

    *   `parcel_attributes`: An array describing each parcel (quantity and weight are required, dimensions are optional).

    *   Optional fields like `order_date` (for priority orders) and `return_all_quotes` (to get quotes from all available couriers).

2.  **Receive a response:** Shippit will return a JSON response containing quotes from different carriers, including:

    *   `courier_type`: The name of the carrier.

    *   `service_level`: The service level (standard, express, priority, on_demand).

    *   `quotes`: An array of quote objects, each with price and estimated delivery details.


### When to Use Quotes vs. Flat Rates

*   **Quotes:** Ideal when you need accurate, real-time shipping costs based on the specific order details (e.g., for large or heavy items, international shipments). This can help you avoid undercharging for shipping and potentially losing money.

*   **Flat Rates:** Simpler to implement and can provide a more predictable shipping cost for customers. However, they may not always reflect the actual cost of shipping, especially for orders with varying weights and destinations.


The best approach depends on your business model, product types, and target customers. You can even combine both methods, using quotes for certain products or destinations and flat rates for others.

### Handling Multiple Priority Carrier Responses

Since April 1, 2019, the `/quotes` endpoint may return multiple priority carrier options when available. The response will include a `courier_type` field for each quote, indicating the specific carrier offering that quote. You'll need to parse this response and decide how to present the options to your customers (e.g., display the cheapest option, allow the customer to choose).

### Rate Card Integration (Advanced)

If you have high shipping volumes or need more control over rate calculations, you can integrate Shippit's rate cards directly into your system. This involves fetching the rate card data from Shippit's API and then using it to calculate shipping costs based on your own logic. This is a more advanced use case and requires careful implementation to ensure accurate rate calculations.
