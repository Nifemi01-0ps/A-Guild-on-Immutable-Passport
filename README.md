#  INTEGRATING IMMUTABLE PASSPORT INTO YOUR APPLICATION
A Complete Guide and Sample Application for Seamless User Authentication and Secure Transactions
### Step 1: Creating a Simple Application
You can either create a simple application or use an existing repository to integrate Immutable Passport. Here's a basic example:
```
<!DOCTYPE html>
<html>
<head>
    <title>Immutable Passport Integration</title>
</head>
<body>
    <h1>Welcome to the Immutable Passport Integration Demo</h1>
    <div id="user-info"></div>

    <script src="app.js"></script>
</body>
</html>
```
### Step 2: Registering the Application on Immutable Developer Hub
Go to the Immutable Developer Hub ```(https://developer.immutable.com)``` and register your application to obtain the required credentials (client ID, client secret, and redirect URI).

### Step 3: Installing and Initializing the Passport Client
Use npm or yarn to install the Immutable Passport client.
<br/>
```npm install immutable-passport```
<br/>
Then, initialize the client in your app.js file.
```
const { Passport } = require('immutable-passport');

const passport = new Passport({
    clientId: 'YOUR_CLIENT_ID',
    clientSecret: 'YOUR_CLIENT_SECRET',
    redirectUri: 'YOUR_REDIRECT_URI'
});
```
### Step 4: Logging in a User with Passport
Implement a login function to authenticate users.
<br/>
```
const login = async () => {
    const url = passport.getLoginURL();
    // Redirect the user to the provided URL
};
```
### Step 5: Displaying User Information
After a successful login, display the ID token, access token, and the user's nickname.
<br/>
``` javascript
// After successful login
const userInfoDiv = document.getElementById('user-info');
userInfoDiv.innerHTML = `
    <p>ID Token: ${passport.getIdToken()}</p>
    <p>Access Token: ${passport.getAccessToken()}</p>
    <p>Nickname: ${passport.getUserInfo().nickname}</p>
`;
```
### Step 6: Logging Out a User
Allow users to log out of the application.
<br/>
```
const logout = () => {
    passport.logout();
    // Redirect the user to the home page or any other desired location
};
```
### Step 7: Initiating a Transaction
To initiate a transaction, use the Passport instance and call the appropriate function, for example, sending a placeholder string and obtaining the transaction hash.
```
const initiateTransaction = async () => {
    const transactionHash = await passport.sendTransaction('Placeholder string');
    // Handle the transaction hash
};
```
### Sample Application
```
<!DOCTYPE html>
<html>
<head>
    <title>Immutable Passport Integration Sample App</title>
</head>
<body>
    <h1>Immutable Passport Integration Sample App</h1>
    <div id="user-info">
        <p>Login to view user information</p>
    </div>
    <button onclick="login()">Login</button>
    <button onclick="logout()">Logout</button>

    <script src="https://cdn.jsdelivr.net/npm/immutable-passport@1.0.0/dist/immutable-passport.min.js"></script>
    <script>
        const { Passport } = window.ImmutablePassport;

        const passport = new Passport({
            clientId: 'YOUR_CLIENT_ID',
            clientSecret: 'YOUR_CLIENT_SECRET',
            redirectUri: 'YOUR_REDIRECT_URI'
        });

        const login = async () => {
            const url = passport.getLoginURL();
            window.location.href = url;
        };

        const logout = () => {
            passport.logout();
            document.getElementById('user-info').innerHTML = '<p>User logged out</p>';
        };

        const displayUserInfo = () => {
            const userInfoDiv = document.getElementById('user-info');
            userInfoDiv.innerHTML = `
                <p>ID Token: ${passport.getIdToken()}</p>
                <p>Access Token: ${passport.getAccessToken()}</p>
                <p>Nickname: ${passport.getUserInfo().nickname}</p>
            `;
        };

        // Check for authentication on page load
        if (passport.isAuthenticated()) {
            displayUserInfo();
        }

        // Handle authentication callback from the redirect URI
        const urlParams = new URLSearchParams(window.location.search);
        const code = urlParams.get('code');
        if (code) {
            passport.handleCallback(code);
            displayUserInfo();
            // Redirect to remove the code from the URL
            window.history.replaceState({}, document.title, "/");
        }
    </script>
</body>
</html>
```



















