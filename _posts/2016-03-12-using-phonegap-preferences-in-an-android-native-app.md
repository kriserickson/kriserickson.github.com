---
layout: post
title: "Using PhoneGap Preferences in an Android Native App"
description: ""
category: Android
tags: [Programming, Android, Mobile, PhoneGap, Cordova]
---

When updating [RecipeFolder](https://recipe-folder.com) from a PhoneGap/Cordova hybrid to a Native Java app I initially
experienced a euphoria on how quick it was to develop in Android now.  6 months in, and still without having actually
shipped the update that euphoria is long gone.  Like any development finishing the last 10% takes 90% of the time,
and it has been mostly done for about 5 months now.  When I was initially planning on releasing the app (5 months ago),
I planned to not add any features and just go with a cleaner look (an approach which abandoned since this would be the
second time a rewrote the app basically from scratch to add no functionality so the release languishes while I add more
and more features) I realized that it would disrespectful to the users to lose all their preferences and force them
to login again.

I figured that since the users preferences was stored in <code>localStorage</code> there must be a way to retrieve them
in my Native App.   Knowing that WebKit (Chrome or the Android Browser) stores all of its localStorage data in a SqlLite
database, I realized that it must be possible to somehow import the preferences from the PhoneGap version of my app.
Since it took a bit of work, messing around, and trial and error to get it working right, I thought I might share the
results with my readers and might provide some insight and potentially help if you too, dear reader, decide to ever port
from Phonegap/Cordova app to a Native App.  Discovering the technique, I have now also used it to read and write preferences
in a background service for a PhoneGap app.

The localStorage database is located in <code>/data/data/com.yourphonegap.name/app_webview/Local Storage/file__0.localstorage</code>.
To get access to it the easiest way is through Android Device Monitor (if the device is rooted and you can access /data/data from
the file explorer):

![Download LocalStorage SqlLite](/img/import_preferences/download_sqlite.png)

If you don't have access to root, you can get the file through adb:

{% highlight shell %}
adb -d shell "run-as com.yourpackge.name cat /data/data/com.yourphonegap.name/app_webview/Local Storage/file__0.localstorage > /sdcard/file__0.localstorage"
adb pull /sdcard/file__0.localstorage
{% endhighlight %}

Now use your favorite [SQLite Browser](https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager/) to open the database.  You
are going to see one table (ItemTable), with two columns (key and value).  Now the values you see are going to be a little
hard to decipher as they are UTF-16 encoded blobs, but it is nice to at least have a look and see that what we are looking
at is a relatively normal SqLite database.  Now lets look at the code to get values from our table:

{% highlight java %}
ContextWrapper contextWrapper = new ContextWrapper(this);

// Find the data directory
File dataDir = new File(contextWrapper.getFilesDir().getParent());

// Get the localStorage file
File appWebViewFilesDir = new File(dataDir, "app_webview/Local Storage/file__0.localstorage");

// Make sure it exists...
if (appWebViewFilesDir.exists()) {

     SQLiteDatabase database = null;
     Cursor cursor = null;
     boolean success = false;
     try {
         // Open the sqlite database
         database = SQLiteDatabase.openDatabase(dbPath, null, SQLiteDatabase.OPEN_READONLY);

         // Get all the values in the item table, obviously you can query specific values if you want
         cursor = database.rawQuery("SELECT value FROM ItemTable", new String[]{});
         cursor.moveToFirst();
         while (!cursor.isAfterLast()) {
             // Our items are blobs
             byte[] itemByteArray = cursor.getBlob(0);

             // Decode the UTF-16 blob into a nice Java string...
             String itemString = new String(itemByteArray, Charset.forName("UTF-16LE"));

             // Just dump the values to the log
             Log.d(TAG, "Item Value: " + itemString);
             cursor.moveToNext();
         }
     } catch (IOError ex) {
         Log.e(TAG, "IO Error on getting email/password from previous version", ex);
     } catch (SQLiteException ex) {
         Log.e(TAG, "SQLite Execption", ex);
     } catch (Exception ex) {
         Log.e(TAG, "Execption", ex);
     } finally {
         // Safely close out our database..
         if (cursor != null) {
             cursor.close();
         }
         if (database != null) {
             database.close();
         }
     }
}
{% endhighlight %}

And that's it.  Now you can read all the localStorage you want from your old PhoneGap apps either as part of a hybrid
approach mobile development or if you are switching to a native android App from a PhoneGap app for whatever reason.  Hopefully
you find this useful, or at least a little educational.

This also can be done in iOS, but I haven't started the iOS port of RecipeFolder yet, so I if it presents the same
kind of issues I had when grabbing it on Android I might write an article for that as well.