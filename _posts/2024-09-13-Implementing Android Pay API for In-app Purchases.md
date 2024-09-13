# Implementing Android Pay API for In-app Purchases

In this blog post, we will explore how to implement the Android Pay API for in-app purchases in both Kotlin and Java for Android development. Android Pay API allows developers to integrate easy and secure payment options within their apps, making it convenient for users to make purchases.

## Getting Started

To begin, make sure you have the latest version of Android Studio installed. Create a new project or open an existing project you want to implement the Android Pay API in.

## Setting up Android Pay API

1. Enable Android Pay API: In your project's `build.gradle` file, add the following dependencies:
   ```groovy
   dependencies {
       implementation 'com.google.android.gms:play-services-wallet:18.1.0'
   }
   ```

2. Manifest Changes: Open your `AndroidManifest.xml` file and add the following permissions and service declarations:
   ```xml
   <uses-permission android:name="com.google.android.gms.permission.PAYMENT_BROADCAST_PERMISSION" />

   <application>
       <service
           android:name="com.google.android.gms.wallet.service.WalletService"
           android:exported="false" >
           <intent-filter>
               <action android:name="com.google.android.gms.wallet.service.BIND"/>
               <category android:name="android.intent.category.DEFAULT" />
           </intent-filter>
       </service>
   </application>
   ```

## Implementing Android Pay API in Kotlin

1. Create a new Kotlin file, e.g., `PaymentHelper.kt`, and implement the helper class as shown below:
   ```kotlin
   import android.app.Activity
   import android.content.Intent
   import com.google.android.gms.wallet.PaymentsClient
   import com.google.android.gms.wallet.Wallet
   import com.google.android.gms.wallet.WalletConstants

   class PaymentHelper(private val activity: Activity) {

       private lateinit var paymentsClient: PaymentsClient

       init {
           createPaymentsClient()
       }

       private fun createPaymentsClient() {
           val environment = WalletConstants.ENVIRONMENT_TEST // Use ENVIRONMENT_PRODUCTION for production

           val walletOptions = Wallet.WalletOptions.Builder()
               .setEnvironment(environment)
               .build()

           paymentsClient = Wallet.getPaymentsClient(activity, walletOptions)
       }

       fun isReadyToPay(): Boolean {
           // Check if device supports Android Pay and is set up
           TODO()
       }

       fun requestPayment() {
           // Request payment using Android Pay
           TODO()
       }

       fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
           // Handle the result of the payment request
           TODO()
       }
   }
   ```

2. Now, in your activity or fragment where you want to implement the Android Pay API, create an instance of the `PaymentHelper` class and call the necessary methods wherever required:
   ```kotlin
   class MainActivity : AppCompatActivity() {

       private lateinit var paymentHelper: PaymentHelper

       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)

           paymentHelper = PaymentHelper(this)

           if (paymentHelper.isReadyToPay()) {
               // Show Android Pay button or any UI for payment
               TODO()
           } else {
               // Display an alternative payment method
               TODO()
           }
       }

       override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
           super.onActivityResult(requestCode, resultCode, data)

           paymentHelper.onActivityResult(requestCode, resultCode, data)
       }
   }
   ```

## Implementing Android Pay API in Java

1. Create a new Java class, e.g., `PaymentHelper.java`, and implement the helper class as shown below:
   ```java
   import android.app.Activity;
   import android.content.Intent;
   import com.google.android.gms.wallet.PaymentsClient;
   import com.google.android.gms.wallet.Wallet;
   import com.google.android.gms.wallet.WalletConstants;

   public class PaymentHelper {

       private Activity activity;
       private PaymentsClient paymentsClient;

       public PaymentHelper(Activity activity) {
           this.activity = activity;
           createPaymentsClient();
       }

       private void createPaymentsClient() {
           int environment = WalletConstants.ENVIRONMENT_TEST; // Use ENVIRONMENT_PRODUCTION for production

           Wallet.WalletOptions walletOptions = new Wallet.WalletOptions.Builder()
                   .setEnvironment(environment)
                   .build();

           paymentsClient = Wallet.getPaymentsClient(activity, walletOptions);
       }

       public boolean isReadyToPay() {
           // Check if device supports Android Pay and is set up
           return false; // Implement your logic here
       }

       public void requestPayment() {
           // Request payment using Android Pay
           // Implement your logic here
       }

       public void onActivityResult(int requestCode, int resultCode, Intent data) {
           // Handle the result of the payment request
           // Implement your logic here
       }
   }
   ```

2. Similarly, in your activity or fragment where you want to implement the Android Pay API, create an instance of the `PaymentHelper` class and call the necessary methods wherever required:
   ```java
   public class MainActivity extends AppCompatActivity {

       private PaymentHelper paymentHelper;

       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);

           paymentHelper = new PaymentHelper(this);

           if (paymentHelper.isReadyToPay()) {
               // Show Android Pay button or any UI for payment
               // Implement your logic here
           } else {
               // Display an alternative payment method
               // Implement your logic here
           }
       }

       @Override
       protected void onActivityResult(int requestCode, int resultCode, Intent data) {
           super.onActivityResult(requestCode, resultCode, data);

           paymentHelper.onActivityResult(requestCode, resultCode, data);
       }
   }
   ```

## Conclusion

In this blog post, we learned how to implement the Android Pay API for in-app purchases in both Kotlin and Java for Android development. By integrating the Android Pay API, developers can provide a seamless and secure payment experience within their apps.
参考文献：

1. [How to Implement In-App Purchases in Android Apps](https://www.jjblogs.com/post/1191506)
