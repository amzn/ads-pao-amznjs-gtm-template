# Amazon Advertising Tag - GTM Template

This repository hosts the Google Tag Manager (GTM) custom tag template for Amazon Advertising. It enables advertisers to deploy Amazon Ad Tags through GTM for conversion tracking, audience building, and attribution.

## Getting Started

1. In Google Tag Manager, go to **Templates > Tag Templates > Search Gallery**
2. Search for "Amazon Advertising Tag" and add it to your workspace
3. Create a new tag using the template
4. Enter your Tag ID(s) from Amazon DSP
5. Select your event name and region
6. Configure your trigger and publish

## Configuration

### Tag IDs
Add a Tag ID provided by Amazon DSP. These identify your advertiser account for conversion tracking.

### Event Name
Choose a **Standard** event (PageView, AddToShoppingCart, Checkout, Signup, Lead, Off-AmazonPurchases, etc.) or define a **Custom** event name.

### Region
Select the region that matches your Amazon DSP account:
- **NA** — North America, South America, Japan, and Australia
- **EU** — Europe

### Advanced Matching
Enable Advanced Matching to pass hashed user data (email, phone number, or Match ID) for improved attribution accuracy.

### Attributes
- **Default Attributes** — key-value pairs sent with standard events (value, brand, category, productId, attr1–attr10)
- **Off-AmazonPurchase Attributes** — includes currencyCode, unitsSold, and value in addition to standard attributes
- **Custom Attributes** — arbitrary key-value pairs for custom reporting

### TCFv2
If operating in GDPR regions, enable TCFv2 to pass consent signals (GDPR applicability, consent string, personal data flag) with your events.

### Amazon Consent
For Amazon's proprietary consent format, configure geo attributes (IP address, country code), Amazon ad storage/user data consent values, and GPP string.

## Consent Mode

This template integrates with [GTM's native Consent Mode](https://support.google.com/tagmanager/answer/10718549). It declares `access_consent` permissions for `ad_storage` and `ad_user_data`, and uses the `isConsentGranted` API to check consent state before firing.

**How it works:**

- If `ad_storage` or `ad_user_data` consent is denied, the tag will not fire.
- If consent is later granted (e.g. user accepts a cookie banner), the tag will fire normally on subsequent triggers.
- If no consent mode is configured in the container, the tag fires as usual with no behavior change.

**No additional setup required.** If your GTM container already has a Consent Management Platform (CMP) configured, the Amazon Ad Tag will automatically respect those consent signals.

## Version

Current version: **3.6**

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This project is licensed under the Apache-2.0 License.
