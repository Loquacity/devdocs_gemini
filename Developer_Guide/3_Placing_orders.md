### III. Placing Orders

The Shippit API is designed to handle a variety of order types, each with its own set of requirements and considerations. Understanding these order types is crucial for successful integration.

### Understanding Order Types

Shippit categorizes orders into several types, primarily based on the desired delivery speed and service level:

*   **Standard Orders:** These are regular shipments with an estimated delivery time of 3-5 business days.

*   **Express Orders:** These are faster shipments, typically delivered the next day after the order is placed.

*   **Priority Orders:** These are same-day deliveries, often used for urgent or time-sensitive shipments.

*   **Click & Collect Orders:** These are orders that customers pick up from a designated location, such as a retail store.

*   **On-Demand Orders:** These are similar to priority orders, but with a focus on immediate fulfillment, usually within a few hours.


Each order type has specific requirements in the API request payload, which we'll cover in the next section.

### International Orders

International orders have additional requirements compared to domestic orders. These include:

*   **Customs Information:** You'll need to provide details like tariff codes, country of origin, and customs declaration information.

*   **Duties and Taxes:** Depending on the destination country and the value of the goods, you may need to include information about duties and taxes.

*   **Recipient Identification:** Some countries require the recipient's identification number (e.g., passport number) for customs clearance.


Be sure to consult the Shippit API documentation for the specific requirements of the countries you ship to.

### Request Structure

The core of the Shippit API's order placement functionality is the `/orders` endpoint. To create an order, you send a POST request to this endpoint with a JSON payload containing the order details.

### Detailed Breakdown of the /orders Payload

The `/orders` payload is a nested JSON object with the following main sections:

*   `order`: This is the top-level object containing all the order information.

    *   `delivery_address`: The recipient's address (required).

    *   `items`: An array of items in the order (optional, but recommended for better tracking and reporting).

    *   `parcels`: An array of parcel specifications (required).

    *   `user_attributes`: Information about the customer (required).

    *   `courier_type` or `courier_allocation`: Specifies the service level or the specific courier (one of these is required).

    *   Various other optional fields, depending on the order type and courier.


We'll cover common mistakes to avoid when constructing this payload in the next section.

### Common Mistakes in Order Creation

#### Incorrect Units

Shippit expects specific units for various measurements in the `/orders` request payload:

*   **Parcel Dimensions:** Length, width, and depth should be in **meters**. A common mistake is to provide these values in centimeters or inches.

*   **Parcel Weight:** Weight should be in **kilograms**. Ensure you convert from other units like pounds or grams.


#### Missing Required Fields

The required fields for an order can vary depending on several factors:

*   **Order Type:** Standard, express, priority, click & collect, and on-demand orders have different requirements.

*   **Courier:** Different couriers may have specific data requirements.

*   **Domestic vs. International:** International orders typically require more information, such as customs declarations and tariff codes.


Carefully review the API documentation for the specific order type and courier you are using to ensure all required fields are included.

#### Incorrect Data Types

Ensure that the data types of the values you provide in the request payload match the expected types in the API documentation. For example:

*   **Quantities:** Should be integers.

*   **Prices:** Should be numbers (can include decimals).

*   **Booleans:** Should be `true` or `false`.


#### Address Validation

Shippit has strict address validation. If the `validate` field is set to `true` in the request, the order will only be saved if the address is valid. Common issues include:

*   **Incorrect Postcode:** Ensure the postcode matches the suburb and state.

*   **Invalid Suburb:** Double-check the spelling and ensure it is a valid suburb for the given postcode.

*   **Missing Address Components:** Some countries require additional address fields like `delivery_district_city`.

If the address is invalid, Shippit may return a `suggested_address` in the response, which you can use to correct the address.

#### Parcel and Product Specification

*   **Parcel Attributes vs. Product Attributes:** Understand the difference between these two fields and when to use each one. If you are specifying product details separately from parcel information, use both `parcel_attributes` and `product_attributes`. Otherwise, use only `parcel_attributes`.

*   **Parcel Allocation:** Be aware of the "Allocate each item in an order to a separate carton" setting in your Shippit account. This setting affects how Shippit allocates parcels based on the provided information.


#### Tracking Only Orders

*   **Required Fields:** When creating a tracking-only order (where the courier is booked outside of Shippit), ensure you provide the `tracking_only`, `courier_allocation`, and `parcel_attributes` -> `label_number` fields.

*   **Tracking Histories:** Consider providing `tracking_histories` to give the recipient more visibility into the order's progress.

### Code Examples

Shippit's documentation includes code examples in various languages, including:

*   **Click and Collect Order:** Demonstrates how to create an order for in-store pickup.

*   **Express Order:** Shows how to create an order for next-day delivery.

*   **International Order:** Illustrates the additional fields required for international shipments.

*   **Standard Order:** Provides a basic example of creating a standard order.

*   **Track Only Order:** Shows how to create an order for tracking only, where the shipment is booked outside of Shippit.

*   **Plain Label Order:** Demonstrates how to create an order without a courier, where the merchant handles delivery.

*   **On-Demand Order:** Shows how to create an order for immediate fulfillment.

*   **Priority Order:** Illustrates how to create an order for same-day delivery.


These examples can be found in the "Getting Started with API Payloads" section of the Shippit documentation. They provide a helpful starting point for understanding the structure and content of API requests for different order types.
