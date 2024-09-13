# Building a Photo Editing App with Android Graphics Framework

In today's digital age, photo editing has become an essential part of our lives. Whether it's adding filters, removing blemishes, or adjusting the brightness, we all love to enhance our photos before sharing them with the world. In this tutorial, we will learn how to build a photo editing app using the Android Graphics Framework.

## Introduction to Android Graphics Framework

The Android Graphics Framework is a robust set of libraries and APIs that allow developers to create visually stunning and responsive user interfaces. It provides tools to handle image rendering and manipulation, enabling developers to build powerful photo editing applications.

## Setting up the Project

To begin, we need to set up our project. We can use either Kotlin or Java for our app development. Let's start by creating a new Android project in Android Studio.

1. Open Android Studio and click on "Start a new Android Studio project."
2. Choose a project name and select the language as either Kotlin or Java.
3. Select the minimum SDK version and choose an empty activity template.
4. Click "Finish" to create the project.

## Adding Dependencies

Once our project is set up, we need to add the necessary dependencies to work with the Android Graphics Framework.

1. Open your project's `build.gradle` file.
2. Add the following dependencies under the `dependencies` section:

    ```
    implementation 'androidx.appcompat:appcompat:1.3.1'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.1'
    implementation 'androidx.appcompat:appcompat:1.3.1'
    implementation 'androidx.core:core-ktx:1.6.0'
    implementation 'androidx.navigation:navigation-fragment-ktx:2.3.5'
    implementation 'androidx.navigation:navigation-ui-ktx:2.3.5'
    implementation 'com.github.bumptech.glide:glide:4.12.0'
    ```

3. Sync your project with Gradle files.

## Building the User Interface

Next, let's design the user interface for our photo editing app. We will create a simple layout with an image view and some buttons for user interactions.

1. Open the `activity_main.xml` file.
2. Replace the existing layout code with the following code:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <ImageView
            android:id="@+id/imageView"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:scaleType="fitCenter"
            android:src="@drawable/placeholder_image" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            android:gravity="center">

            <Button
                android:id="@+id/btnFilter"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Apply Filter" />

            <Button
                android:id="@+id/btnBrightness"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Adjust Brightness" />

            <Button
                android:id="@+id/btnSave"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Save Image" />
        </LinearLayout>
    </RelativeLayout>
    ```

3. Replace `@drawable/placeholder_image` with the default image you want to display in the image view.

## Implementing Photo Editing Functionality

Now, let's dive into the photo editing functionality of our app. We will start by loading an image using Glide library and then implement the necessary methods for applying filters, adjusting brightness, and saving the edited image.

1. Open the `MainActivity.kt` file.
2. Replace the existing code with the following code:

    ```kotlin
    import android.content.Intent
    import android.graphics.Bitmap
    import android.graphics.ColorMatrix
    import android.graphics.ColorMatrixColorFilter
    import android.net.Uri
    import android.os.Bundle
    import android.provider.MediaStore
    import android.widget.Button
    import android.widget.ImageView
    import androidx.appcompat.app.AppCompatActivity
    import com.bumptech.glide.Glide

    class MainActivity : AppCompatActivity() {
        private lateinit var imageView: ImageView

        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(R.layout.activity_main)

            imageView = findViewById(R.id.imageView)

            // Load image using Glide library
            Glide.with(this)
                .load(R.drawable.placeholder_image)
                .into(imageView)

            val btnFilter: Button = findViewById(R.id.btnFilter)
            btnFilter.setOnClickListener {
                applyFilter()
            }

            val btnBrightness: Button = findViewById(R.id.btnBrightness)
            btnBrightness.setOnClickListener {
                adjustBrightness()
            }

            val btnSave: Button = findViewById(R.id.btnSave)
            btnSave.setOnClickListener {
                saveImage()
            }
        }

        private fun applyFilter() {
            // Apply a filter to the image
            val colorMatrix = ColorMatrix().apply {
                setSaturation(0f) // Convert to grayscale
            }
            val colorFilter = ColorMatrixColorFilter(colorMatrix)
            imageView.colorFilter = colorFilter
        }

        private fun adjustBrightness() {
            // Modify brightness of the image
            // Implement your logic here
        }

        private fun saveImage() {
            // Save the edited image to the device gallery
            imageView.isDrawingCacheEnabled = true
            val bitmap = Bitmap.createBitmap(imageView.drawingCache)
            imageView.isDrawingCacheEnabled = false

            val uri = MediaStore.Images.Media.insertImage(
                contentResolver,
                bitmap,
                "Edited_Image",
                "Image edited using the photo editing app."
            )

            // Open the saved image in the gallery
            val intent = Intent()
            intent.action = Intent.ACTION_VIEW
            intent.data = Uri.parse(uri)
            startActivity(intent)
        }
    }
    ```

    Make sure to replace `placeholder_image` in the `load()` method with the image you want to display initially.

With the above code, we have implemented the basic functionalities of our photo editing app. You can further enhance it by adding features like cropping, rotating, and applying advanced filters.

## Conclusion

In this tutorial, we learned how to build a photo editing app using the Android Graphics Framework. We set up the project, added dependencies, designed the user interface, and implemented the photo editing functionality. With this foundation, you can now explore more advanced editing features and create your own unique photo editing app. Happy coding!
参考文献：

1. [Building a Todo List App with Room Database in Android](https://www.jjblogs.com/post/1165193)
