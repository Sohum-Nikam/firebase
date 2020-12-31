<!DOCTYPE html>
<html>
    <head>
    <meta charset="utf=8">
    <title> firebase web quickstart </title>
    <style media="screen">
        body{
            display: flex;
            min-height: 100vh;
            width: 100%;
            padding: 0;
            margin: 0;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }

        #uploader {
            -webkit-appearance: none;
            appearance: none;
            width: 50%;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

    <progress value="0" max="100" id="uploader">0%</progress>
    <input type="file" value="upload" id="filebutton" />
    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="https://www.gstatic.com/firebasejs/8.2.1/firebase-app.js"></script>
    <!-- TODO: Add SDKs for Firebase products that you want to use
        https://firebase.google.com/docs/web/setup#available-libraries -->
    <script src="https://www.gstatic.com/firebasejs/8.2.1/firebase-analytics.js"></script>
    <script defer src="https://www.gstatic.com/firebasejs/8.2.1/firebase-auth.js"></script>
    <script defer src="https://www.gstatic.com/firebasejs/8.2.1/firebase-firestore.js"></script>

    // ...
    <script>
    // Your web app's Firebase configuration
    // For Firebase JS SDK v7.20.0 and later, measurementId is optional
    var firebaseConfig = {
        apiKey: "AIzaSyBTwXNgbS9Ts6RBPKZYPZWglmKuvjJA6Ek",
        authDomain: "firebasics-72874.firebaseapp.com",
        databaseURL: "https://firebasics-72874-default-rtdb.firebaseio.com",
        projectId: "firebasics-72874",
        storageBucket: "firebasics-72874.appspot.com",
        messagingSenderId: "99058873730",
        appId: "1:99058873730:web:d41e3ede98d30c0ef98b9b",
        measurementId: "G-BNVPZ7F0SE"
    };
    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);
    firebase.analytics();

        //get elements 
        var uploader = document.getElementById('uploader');
        var filebutton = document.getElementById('filebutton');

        // listen for file selection
        filebutton:addEventListener('change', function(e) {
            // get file
            var file = e.target.files[0];

            // create a storage ref
            var storageRef = firebase.storage().ref('images' + file.name);

            // Upload file
            var task = storageRef.put(file);

            // Update progress bar
            task.on('state_changed',

                function progress(snapshot) {
                    var percentage = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
                    uploader.value = percentage;
                },

                function error(err) {

                },

                function complete() {

                }

            );
        });
    </script>

</body>
</html>
