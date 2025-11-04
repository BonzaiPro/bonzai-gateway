Bonzai Payment Gateway for WooCommerce

A custom WooCommerce payment gateway integrating with Bonzai Checkout.
This plugin handles payment session creation, customer redirection, and secure webhook-based confirmation from Bonzai.

✨ Features

Adds Bonzai as a payment method in WooCommerce checkout.

Creates a server-side payment session via the Bonzai API.

Redirects the customer to the Bonzai checkout page.

Handles incoming webhooks from Bonzai:

product_access_granted → marks order as completed.

product_access_revoked → marks order as refunded (default).

Idempotent webhook handling (no double-processing).

Security token validation (via query string or header).

Supports currency override (EUR / USD) or fallback to store currency.

Minimum order amount option to display gateway.

Detailed debug logs in WooCommerce → Status → Logs.

Handles API timeout gracefully.

Displays a custom notice if user returns before webhook confirmation.

🧩 Requirements

WordPress with WooCommerce installed and active.

A Bonzai account with API token and webhook configured.

Each product sold via Bonzai must include a custom field:

Key: bonzai_product_uuid

Value: the product’s UUID in Bonzai.

⚙️ Installation

Upload the plugin file to wp-content/plugins/, or zip and install via the WordPress admin panel.

Activate Bonzai Payment Gateway in Plugins.

Go to WooCommerce → Settings → Payments → Bonzai → Manage.

Configure the following:

API Token (required).

Webhook Token (required).

Redirect URL after payment (e.g. /thank-you, automatically suffixed with ?wc_order=ID).

Optional: Currency, Minimum Amount, Timeout, and Debug Logs.

For each product, add the custom field:

Key: bonzai_product_uuid

Value: the UUID from Bonzai.

⚠️ If bonzai_product_uuid is missing, checkout will fail gracefully with an error message.

🔔 Webhooks

The plugin registers a secure REST endpoint for Bonzai webhooks:

/wp-json/bonzai/v1/webhook


The Webhook Token is mandatory.

Bonzai must send it either:

As a query parameter: ...?token=YOUR_TOKEN

Or as an HTTP header: X-Bonzai-Token: YOUR_TOKEN

Supported events:

product_access_granted → marks order as completed.

product_access_revoked → marks order as refunded.

The exact webhook URL is displayed inside the gateway settings screen.

🧠 Order Flow Overview

Customer selects Bonzai at checkout.

Plugin creates a payment session via Bonzai API (amount, currency, email, product UUID, order ID...).

Customer is redirected to Bonzai checkout URL.

Bonzai sends a webhook on payment completion.

Plugin updates the WooCommerce order status based on the webhook event.

🧷 Settings Overview
Setting	Description
Enable Gateway	Turns Bonzai on/off
Title / Description	Text displayed at checkout
API Token	Authentication with Bonzai
Redirect URL	Page after payment
Currency	Force EUR / USD or use store currency
Minimum Amount	Only show if above threshold
API Timeout	Max seconds for Bonzai API calls
Debug Logs	Enable WooCommerce logging
Webhook Token	Security key for incoming webhooks
Webhook URL	Copy this to Bonzai dashboard
🛠 Debug & Troubleshooting

“Bonzai product not configured” → Add bonzai_product_uuid to the product.

Order stuck in pending → Check webhook delivery and token validity.

Unsupported currency → Only EUR and USD are supported by Bonzai.

API errors → Increase timeout and enable debug logs for details.

🧾 Logging

Enable Debug Logs to write to WooCommerce → Status → Logs.
Logs include:

Session creation requests/responses

Webhook payloads

Order updates and error traces

📄 License

Proprietary (you may replace with GPL or MIT as needed).
Author: Ramy
Version: 1.3.0
