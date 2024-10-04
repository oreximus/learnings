## What’s the Best React Native Storage Option?

**source**: https://www.youtube.com/watch?v=wVNPmxntwKQ

- There are multiple data storage options like:

  1. **Packages that expo recommends**
  2. **Databases and Storage options with "Remote Sync" options**
  3. **the cool kids in the block**

- There could various needs for your application to work like:
  - do you want to store the settings?
  - or thousands of rows of data?
  - how oftenly you are updating your app?
  - do you need to store the data offline or sync to the remote server?

### 1. Packages the Expo Suggests:

#### Async Storage:

    This is similar to the local storage in the Browser, and works well in the app, where we store the data in the form key value pair, and also in the form of JSON if you serialize it.

#### File System:

    For storing file and data into it, not really meant to work with data but still you can store JSON file here and use it later.

#### SecureStore

    Same as Async store but stores your data securely in a encrypted way in the local storage of your app.

#### Expo SQLite

    We can store the Data directly in the SQLite Database and use it according to our needs.
