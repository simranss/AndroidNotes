<!-- title: Android Development -->

# Android Development

## Books

### Recommended

1. Android Notes For Professionals - Unknown website
2. Android Studio 3.0 Development Essential (Android 8 Edition)
3. Android Cookbook: Problems and solutions for anroid developers

### Others

1. Professional Android - Reto Meier
2. Android Programming: Pushing the limits - Erik Hellman
3. Android aaplication Development all-in-one for dummies
4. Android Security Cookbook - Keith Makan
5. Android Programming - The big nerd ranch guide

## Custom colors for Logcat messages

### Steps

1. File -> Settings -> Editor -> Color Scheme -> Android Logcat
2. Choose the option from the left side for the type of logcat message.
3. Uncheck the option `Inherit values from` in the right side.
4. Choose the color in the `Foreground`.

## Some useful things for the editor

### Splitting the editor

You can split the editor by right-clicking the file you want to split and choose the option from the menu.

### Parameters

You can know what parameters does a function want by keeping the cursor within the paranthesis and pressing `Ctrl + P`.
Extremely useful since half of the time one needs to find about the parameters on the internet.

### Documentation

You can view the official documentation for a function or any declaration by placing the cursor over the declaration and pressing `Ctrl + Q`.

### Reformatting

You can reformat the code by pressing `Ctrl + Alt + L`.
This helps a lot for files too big for formatting one line at a time.

## App Components

### Activities

A single screen with UI. An android app may have multiple activities.

### Services

A service runs in background. There are two types of services:

1. Foreground: Service that runs in the background but informing the user about it.
2. Background: Service that runs in the background and doesn't necessarily inform the user about it.

Examples:

+ a music player would be running in the background even after the applcation is closed, but informs the user about the process through a notification. (foreground)
+ a service that downloads data from the internet in background (background)

### Content Providers

it manages shared app data. Through content providers, other apps can query or even modify the data stroed by an app.

### Broadcast Receivers

It responds to system-wide broadcast of announcements (eg: a broadcast announcong that the screen has turned off, the battery is low, etc).
Broadcast receivers don't have UI but they can show notification to alert the user.

## Activity Lifecycle

### `onCreate(Bundle savedInstanceState)`

This method is called when the activity is created.
This is the ideal location to perform most of the initialization tasks.

### `onRestart()`

This method is called when the activity is about to restart after having previously stopped by the runtime system.

### `onStart()`

This method is called immediately after the `onCreate()` or `onRestart()` methods.
This method indicates that the activity is about to become visible to user.
This call is followed by a call to `onResume()` or `onStop()` depending if the activity moves to the top of the activity stack or is pushed down the stack by another activity.

### `onResume()`

This method is called to indicate that the activity is now at the top of the activity stack and is the activity with which the user is interacting.

### `onPause()`

This method is called to indicate that a previous activity is about to become the foreground activity.
This call will be followed by a call to either the `onResume()` or `onStop()` method depending on whether the activity moves back to the foreground or becomes invisible to the user.

### `onStop()`

This method is called when the activity is now no longer visible to the user.
The two possible scenarios that may follow this call are a call to `onRestart()` in the event that the activity moves to the foreground again, or `onDestroy()` if the activity is being terminated.

### `onDestroy()`

This method is called when the activity is about to get destroyed.

## Saving and restoring the state of an activity

### Saving

```java
@override
protected void onSaveInstanceState(Bundle outState) {
  super.onSaveInstanceState(outState);
  //Suppose you want to save the text entered by the user in an editText
  CharSequence userText = editText.getText();
  outState.putCharSequence("userText", userText);
}
```

### Restoring

```java
@Override
protected void onRestoreInstanceState(Bundle savedInstanceState) {
  super.onRestoreInstanceState(savedInstanceState);
  CharSequence userText = savedInstanceState.getCharSequence("userText");
  editText.setText(userText);
}
```

## TextView

### Spannable TextView

#### Spannable color

```java
//initialise the textView
TextView textView = findViewById(R.id.text_view);

//initialise the spannable
Spannable spannable = new SpannableString(firstWord + lastWord);

//color for the first word
spannable.setSpan(new ForegroundColorSpan(firstWordColor), 0, firstWord.length(), Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
//color for the second word
spannable.setSpan(new ForegroundColorSpan(lastWordColor), firstWord.length(), (firstWord.length() + lastWord.length()), Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);

//set the text of the textView as the spannable
textView.setText(spannable);
```

#### Spannable font

```java
//initialise the textView
TextView textView = findViewById(R.id.text_view);

//initialise the spannable
Spannable spannable = new SpannableString(firstWord + lastWord);

//font size for the first word
spannable.setSpan(new RelativeSizeSpan(1.1f), 0, firstWord.length(), Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
//font size for the second word
spannable.setSpan(new RelativeSizeSpan(0.8f), firstWord.length(), (firstWord.length() + lastWord.length()), Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);

//set the text of the textView as the spannable
textview.setText(spannable);
```

### Strikethrough TextView

#### Strikethrough the entire text

```java
String sampleText = "This is a test strike";
textView.setPaintFlags(tv.getPaintFlags() | Paint.STRIKE_THRU_TEXT_FLAG);
textView.setText(sampleText);
```
