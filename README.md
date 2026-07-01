# Amazon Advertising Tag - GTM Template

This repository hosts the Google Tag Manager (GTM) custom tag template for Amazon Advertising. It enables advertisers to deploy Amazon Ad Tags through GTM for conversion tracking, audience building, and attribution.

## Getting Started

1. In Google Tag Manager, go to **Templates > Tag Templates > Search Gallery**
2. Search for "Amazon Advertising Tag" and add it to your workspace
3. Create a new tag using the template
4. Enter your Tag ID(s) from Amazon DSP
5. Choose your Configuration Mode, Event Name, and Region
6. Configure your trigger and publish

## Configuration

### Configuration Mode

- **Manual** — configure all fields using [GTM dataLayer variables](https://support.google.com/tagmanager/answer/7683362?hl=en#data_layer)
- **Automatic (GA4)** — automatically reads event attributes from the [GA4 ecommerce](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce) `eventModel` in the dataLayer (value, currency, brand, category, productId, user data). Manually set attributes override auto-populated values.

### Tag IDs
Add a Tag ID provided by Amazon DSP. These identify your advertiser account for conversion tracking.

### Event Name
Choose a **Standard** event (PageView, AddToShoppingCart, Checkout, Signup, Lead, Off-AmazonPurchases, etc.) or define a **Custom** event name.

### Region
Select the region that matches your Amazon DSP account:
- **NA** — North America, South America, Japan, and Australia
- **EU** — Europe

### Client Deduplication ID
A unique identifier (e.g., transaction ID, order ID) used to prevent duplicate conversions when the same event is sent from both client-side and server-side.

### Advanced Matching
Enable Advanced Matching to pass hashed user data (email, phone number, or Match ID) for improved attribution accuracy.

### Attributes
- **Default Attributes** — key-value pairs sent with standard events (value, brand, category, productId, attr1–attr10)
- **Off-AmazonPurchase Attributes** — includes currencyCode, unitsSold, and value in addition to standard attributes
- **Custom Attributes** — arbitrary key-value pairs for custom reporting

### TCFv2
If operating in GDPR regions, enable TCFv2 to pass consent signals (GDPR applicability, consent string, personal data flag) with your events.

### Amazon Consent
Check **Enabled** to pass Amazon Consent Signal (ACS) data with your events.

**Fields:**
- **Country Code** (required) — ISO 3166 two-letter code indicating the legal origin of the request (e.g., US, GB, DE, JP)
- **IP Address** — optional, the user's IP address for geo determination
- **Amazon Ad Storage** — consent for ad storage. Accepted values: `GRANTED`, `DENIED`, `true`, `false`
- **Amazon User Data** — consent for user data processing. Accepted values: `GRANTED`, `DENIED`, `true`, `false`
- **Global Privacy Platform string** — optional IAB GPP consent string from your CMP

**Notes:**
- Country code is always required for Amazon to process your data
- For EEA traffic, you must provide at least one consent signal (TCF, GPP, or ACS)
- If multiple signals are provided, Amazon uses TCF and ignores ACS
- The consent library defaults all signals to DENIED until explicitly set

## Consent Mode

This template integrates with [GTM's native Consent Mode](https://support.google.com/tagmanager/answer/10718549). It declares `access_consent` permissions for `ad_storage` and `ad_user_data`, and uses the `isConsentGranted` API to check consent state before firing.

**How it works:**

- If `ad_storage` or `ad_user_data` consent is denied, the tag will not fire.
- If consent is later granted (e.g. user accepts a cookie banner), the tag will fire normally on subsequent triggers.
- If no consent mode is configured in the container, the tag fires as usual with no behavior change.

**No additional setup required.** If your GTM container already has a Consent Management Platform (CMP) configured, the Amazon Ad Tag will automatically respect those consent signals.

## Version

Current version: **4.0**

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This project is licensed under the Apache-2.0 License.
