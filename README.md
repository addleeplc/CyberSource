# CyberSource Flex Samples (NodeJS)

This repository provides simple examples demonstrating usage of the CyberSource Flex SDK using either a headless JavaScript call (express-flexjs) or a fully customizable hosted field/microform (express-microform) which is incorporated into your checkout page.  For more details on Secure Acceptance Flex visit our Developer Guide at https://developer.cybersource.com/api/developer-guides/dita-flex/SAFlexibleToken.html

## Usage

1. Clone or download this repository.
2. cd into either the microform or flexjs directory
3. Update app.js with your [CyberSource sandbox credentials](https://ebc2test.cybersource.com). 
4. Run ```npm install``` in the sample you want to try (express-microform or express-flexjs).
5. Run ```DEBUG=express-microform:* npm start``` or ```DEBUG=express-flexjs:* npm start```.
6. Browse to http://localhost:3000/checkout in your browser

## Requirements
* Node
* Express
* NPM


## API Reference
While these examples use the JavaScript libraries which we recommend as the most convenient option, you can try out the APIs behind the JavaScript SDKs by visiting our API Reference at https://developer.cybersource.com/api/reference/api-reference.html

## Background on PCI-DSS

Storing your customer’s card data can dramatically increase your repeat-customer conversion rate, but can also add additional risk and [PCI DSS](https://www.pcisecuritystandards.org/pci_security/) overhead. You can mitigate these costs by tokenizing card data. CyberSource will store your customer’s card data within secure Visa data centers, replacing it with a token that only you can use. 

Secure Acceptance Flexible Token is a secure method for Tokenizing card data, that leaves you in total control of the customer experience. Your customer’s card number is encrypted on their own device - for example inside a browser or native app - and sent directly to CyberSource. This means card data bypasses your systems altogether. This can help you qualify for [SAQ A](https://www.pcisecuritystandards.org/documents/Understanding_SAQs_PCI_DSS_v3.pdf) based PCI DSS assessments for web-based integrations, and [SAQ A-EP](https://www.pcisecuritystandards.org/documents/Understanding_SAQs_PCI_DSS_v3.pdf) for native app integrations.

You are in total control of the look and feel, with the ability to seamlessly blend the solution in to your existing checkout flow, on web or in-app.

On-device encryption helps to protect your customers from attacks on network middleware such as app accelerators, DLPs, CDNs, and malicious hotspots.

The token can be used in lieu of actual card data in server-side requests for other CyberSource services, for example to make a payment, using our REST APIs: https://developer.cybersource.com/api/reference/api-reference.html

## Samples

### JavaScript (Flex API) Sample

This sample demonstrates how your checkout form can remain exactly as it is today, with the only addition of a JavaScript call to tokenize the customer's credit card information. This happens directly between their browser and CyberSource, replacing the provided data with a secure PCI-compliant token. This can then be sent to your server along with the other non-PCI order data.  This can help achieve PCI-DSS SAQ A-EP level compliance for your application.  

### Microform Sample

This sample demonstrates how you can replace the sensitive data fields (credit card number) on your checkout form with a field (Flex Microform) hosted entirely on CyberSource servers. This field will accept and tokenize the customer's credit card information directly from their browser on a resource hosted by CyberSource, replacing that data with a secure PCI-compliant token. This can then be sent to your server along with the other non-PCI order data.  This can help achieve PCI-DSS SAQ A level compliance for your application as even your client-side code does not contain a mechanism to handle the credit card information.


## Using the Flex Payment Token

You can use the token generated to make a payment with the CyberSource REST API (https://developer.cybersource.com/api/reference/api-reference.html).  

Place the token in the CustomerId field:

```json
{
  "clientReferenceInformation": {
    "code": "TC50171_3"
  },
  "processingInformation": {
    "commerceIndicator": "internet"
  },
  "paymentInformation": {
    "customer": {
      "customerId": "7500BB199B4270EFE05340588D0AFCAD"
    }
  },
  "orderInformation": {
    "amountDetails": {
      "totalAmount": "22",
      "currency": "USD"
    },
    "billTo": {
      "firstName": "John",
      "lastName": "Doe"
    }
  }
}

```

