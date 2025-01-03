# Two-Screen Android Application

This repository contains an Android application written in Kotlin that demonstrates a simple two-screen app. The app captures a username and password on the first screen and displays a welcome message with the username on the second screen.

## Features
- Two screens:
  1. **Login Screen**: Accepts username and password input.
  2. **Welcome Screen**: Displays a personalized welcome message.
- Implements basic Android navigation using `Intent`.
- User-friendly layout and responsive design.

## Code Explanation

### 1. **MainActivity.kt**
The `MainActivity` is the first screen where the user enters their username and password.

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val usernameEditText = findViewById<EditText>(R.id.usernameEditText)
        val passwordEditText = findViewById<EditText>(R.id.passwordEditText)
        val submitButton = findViewById<Button>(R.id.submitButton)

        submitButton.setOnClickListener {
            val username = usernameEditText.text.toString()
            val intent = Intent(this, WelcomeActivity::class.java)
            intent.putExtra("USERNAME", username)
            startActivity(intent)
        }
    }
}
```
- **Components Used**:
  - `EditText`: For username and password inputs.
  - `Button`: For submitting the inputs.
- **Intent**: Used to navigate to the second screen (`WelcomeActivity`) and pass the username.

### 2. **WelcomeActivity.kt**
The `WelcomeActivity` is the second screen that displays a welcome message using the username passed from `MainActivity`.

```kotlin
class WelcomeActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_welcome)

        val username = intent.getStringExtra("USERNAME")
        val welcomeTextView = findViewById<TextView>(R.id.welcomeTextView)
        welcomeTextView.text = "Welcome, $username!"
    }
}
```
- **Components Used**:
  - `TextView`: For displaying the welcome message.
- **Intent**: Retrieves the username from the previous activity.

### 3. **Layouts**
#### `activity_main.xml`
Defines the layout for the first screen.
```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/usernameEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Username" />

    <EditText
        android:id="@+id/passwordEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Password"
        android:inputType="textPassword" />

    <Button
        android:id="@+id/submitButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Submit"
        android:layout_marginTop="16dp" />
</LinearLayout>
```

#### `activity_welcome.xml`
Defines the layout for the second screen.
```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:id="@+id/welcomeTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Welcome!"
        android:textSize="24sp"
        android:textStyle="bold" />
</LinearLayout>
```

### 4. **AndroidManifest.xml**
Adds the second activity to the app manifest.
```xml
<activity android:name=".WelcomeActivity"></activity>
```

## How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/two-screen-app.git
   ```
2. Open the project in Android Studio.
3. Build and run the app on an emulator or physical device.
4. On the first screen, enter a username and password, then click the **Submit** button.
5. The second screen will display a welcome message with the entered username.

## Dependencies
- Android Studio (latest version recommended).
- Kotlin support enabled in Android Studio.

## Folder Structure
```
.
├── app
│   ├── src
│   │   ├── main
│   │   │   ├── java/com/example/twoscreenapp
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── WelcomeActivity.kt
│   │   │   ├── res
│   │   │   │   ├── layout
│   │   │   │   │   ├── activity_main.xml
│   │   │   │   │   ├── activity_welcome.xml
│   │   │   │   ├── values
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   ├── themes.xml
├── build.gradle
├── AndroidManifest.xml
```

