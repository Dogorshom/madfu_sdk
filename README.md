# Madfu SDK for Flutter

Madfu SDK allows you to easily integrate the Madfu payment gateway into your Flutter applications.

![alt text](https://i.ibb.co/2n3dsrM/Madfu-Link-Flutter.png)

### Platform Compatibility

The Madfu SDK supports the following platforms:
- **iOS**
- **Android**

## Features

- Simple and easy-to-use widget for initiating payment processes.
- Callback functions for handling payment success, failure, cancellation, and errors.
- Supports both light and dark modes.
- Customizable environments for development and production.

## Installation

Add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  madfu_sdk: latestVersion
```
## Parameters

### Required Parameters

- **madfuOrderModel (MadfuOrderModel)**: The order model that contains all the necessary data for the payment process.
- **apiKey (string)**: The API Key provided by the Madfu Integration Team.
- **appCode (string)**: The App Code provided by the Madfu Integration Team.
- **authorization (string)**: The Authorization token provided by the Madfu Integration Team.
- **merchantUsername (string)**: Merchant username provided by the Madfu Integration Team.
- **merchantPassword (string)**: Merchant password provided by the Madfu Integration Team.

### Optional Parameters

- **madfuEnvironment (MadfuEnvironment)**: The environment to use for the payment process. Default is `MadfuEnvironment.live`.
- **isDarkMode (bool)**: The theme mode for the landing page of the payment process. Default is `false`.
- **onPaymentSuccess (Function()?)**: The function to be called when the payment is successful.
- **onPaymentFailure (Function()?)**: The function to be called when the payment fails.
- **onPaymentCancel (Function()?)**: The function to be called when the payment is cancelled.
- **onPaymentError (Function()?)**: The function to be called when there is an error during the payment process.


## Usage

Here's a basic example of how to use the MadfuWidget in your Flutter application:

```dart
import 'package:flutter/material.dart';
import 'package:madfu_sdk/madfu_sdk.dart';

void main() async {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Madfu Pay Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.blue),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Madfu Pay Demo'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});
  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MadfuWidget(
                      appCode: "your_app_code",
                      apiKey: "your_api_key",
                      authorization: "your_authorization",
                      madfuEnvironment: MadfuEnvironment.test,
                      madfuOrderModel: MadfuOrderModel(
                          order: MadfuOrderData(
                            taxes: 13.04,
                            actualValue: 86.96,
                            amount: 100,
                            merchantReference: "123456",
                          ),
                          guestOrderData: GuestOrderData(customerMobile: "5XXXXXXXX", lang: "ar"),
                          merchantUrls: MerchantUrls(
                            success: "your_success_url",
                            failure: "your_failure_url",
                            cancel: "your_cancel_url",
                          ),
                          orderDetails: [
                            OrderDetails(
                              productImage: "https://via.placeholder.com/100x100",
                              productName: "Product Name",
                              totalAmount: 50,
                              count: 1,
                              sku: "123Product",
                            )
                          ]),
                      onPaymentSuccess: () {
                        // Handle payment success
                      },
                      onPaymentFailure: () {
                        // Handle payment failure
                      },
                      onPaymentCancel: () {
                        // Handle payment cancellation
                      },
                      onPaymentError: () {
                        // Handle payment error
                      },
                    ),
                  ),
                );
              },
              child: const Text('Pay Now With Madfu'))
        ],
      ),
    );
  }
}
```
### Madfu Order Model Parameters

#### Order Details

The order details are encapsulated in the `MadfuOrderData` object, which contains the following required fields:

- **taxes (double)**: The taxes amount. (required)
- **actualValue (double)**: The actual value of the order. (required)
- **amount (double)**: The total amount of the order. (required)
- **merchantReference (String)**: The merchant reference for the order (Order ID from your system). (required)

#### Guest Order Data

The guest order data is encapsulated in the `GuestOrderData` object, which contains the following fields:

- **customerMobile (String)**: The customer mobile number. (required)
- **customerName (String)**: The customer name. (Optional)
- **lang (String)**: The language of the customer. (required)

#### Merchant URLs

The merchant URLs are encapsulated in the `MerchantUrls` object, which contains the following required fields:

- **success (String)**: The success URL. (required)
- **failure (String)**: The failure URL. (required)
- **cancel (String)**: The cancel URL. (required)

#### Order Details List

The `orderDetails` is a list of `OrderDetails` objects that contains the product details. At least one `OrderDetails` object is required. Each `OrderDetails` object contains the following fields:

- **productName (String)**: The product name.
- **sku (String)**: The product SKU.
- **productImage (String)**: The product image URL.
- **count (int)**: The product count.
- **totalAmount (double)**: The total amount of the product.

### Support

If you encounter any issues or have questions, please contact our support team at [support@madfu.com](mailto:support@madfu.com).

### Contributions

Contributions to the SDK are welcome! You can open an issue or submit a pull request on GitHub if you have any improvements or bug fixes.

---

For more details, please refer to the [official documentation](https://madfuapis.readme.io).