# firebase-store
MIT xPro Week 26 Video 26.6

You now need to set up storage for your Firebase application. This is a low-cost alternative to many of the storage solutions provided by large cloud providers like AWS or Microsoft Azure. 

Again, you should reference the Firebase storage library and write the code for the UI elements within the storage.html file. Next, configure the storage settings within the storage.js file.

1. Set up cloud storage in your firebase project. No permissions for this small prototype project. Choose a nearby location for speed considerations.

After the Storage is created for the project. Goto rules link and allow read and write without any conditionals.

If you stuck and can't create a storage bucket for your project on the firebase website, then [use the CLI](https://stackoverflow.com/questions/74750161/why-i-receive-an-error-while-creating-firebase-storage/74750337#74750337)

```firebase init storage```

```firebase deploy --only storage```

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write;
    }
  }
}
```


```
{
apiKey: "AIzaSyA0Qwq8mysTh3V1jSksRwKsKdgZ1cxJ_O8",
  authDomain: "authentification-984e3.firebaseapp.com",
  databaseURL: "https://authentification-984e3-default-rtdb.firebaseio.com",
  projectId: "authentification-984e3",
  storageBucket: "authentification-984e3.appspot.com",
  messagingSenderId: "67601999533",
  appId: "1:67601999533:web:aa0fe9acf57e382027c824"
}
```

2. Add the firbase libraries, UI element for file, submit upload, submit download, status of the operation, image and the .js script reference to the html.

```
<!DOCTYPE html>
<html>
<head>
    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="https://www.gstatic.com/firebasejs/7.24.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/7.24.0/firebase-storage.js"></script>    
</head>

<input type="file" id="file" name="file" multiple><br><br>
<input type="submit" id="upload">
<input type="submit" id="download" value="Download"><br><br>
<div id="status"></div><br><br>
<img src="" id="image" width="200px">
<script src="storage.js"></script>
</html>
```

3. Create the firebase function

```
(function(){

}());
```

- Define the Web App's configuration object. This is provided in the firbase project settings. An example of the object is shown in step 1 above.

- Initialize Firebase

- Add the storage feature. Create a root reference.

- get UI elements by id

- enter code to upload a file to storage.

- enter code to download a file from storage.

```
(function(){

	// Your web app's Firebase configuration
	// For Firebase JS SDK v7.20.0 and later, measurementId is optional
	var firebaseConfig = {
		apiKey: "AIzaSyA0Qwq8mysTh3V1jSksRwKsKdgZ1cxJ_O8",
  		authDomain: "authentification-984e3.firebaseapp.com",
  		databaseURL: "https://authentification-984e3-default-rtdb.firebaseio.com",
  		projectId: "authentification-984e3",
  		storageBucket: "authentification-984e3.appspot.com",
  		messagingSenderId: "67601999533",
  		appId: "1:67601999533:web:aa0fe9acf57e382027c824"
	};
	// Initialize Firebase
	firebase.initializeApp(firebaseConfig);

	// Create a root reference
	var storage = firebase.storage();
	var storageRef = storage.ref();

	// get elements
	const file     = document.getElementById('file');
	const upload   = document.getElementById('upload');	
	const download = document.getElementById('download');		
	const status   = document.getElementById('status');	
	const image    = document.getElementById('image');

	// upload file
	upload.addEventListener('click', e => {
		// Create a file reference
		var ref = storageRef.child('globe');
		let photo = document.getElementById("file").files[0];

		// upload
		ref.put(photo).then(function(snapshot) {
			console.log('Uploaded a blob or file!');
			status.innerHTML = 'Uploaded blob or file!'
		});
	});

	// download file
	download.addEventListener('click', e => {
		// file reference
		var ref = storage.ref('globe');

		ref.getDownloadURL().then(function(url) {
			// insert url into an <img> tag to "download"
			image.src = url;
			status.innerHTML = 'Downloaded blob or file!'			

		}).catch(function(error){console.log(error)});


	});


}());
```

4. Drag the html to the browser and upload an image file. Check the firebase project Storage to see if an image named "globe" was added.