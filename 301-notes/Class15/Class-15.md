# Authentication

## Auth0 Defintion

OAuth is a system that allows you to access certain resources or information on one website or application using your existing credentials from another website or application. It's like having a special key that allows you to unlock specific doors without sharing your original master key.

Here's an example using a real-life scenario:

Imagine you want to sign up for a new website using your Google account. Instead of creating a new username and password, you can use the "Sign in with Google" option. When you click on it, you'll be redirected to Google's website to enter your Google credentials (email and password). Once you enter your credentials and give permission, Google will generate a special access token and send it back to the website you're signing up for. This access token acts as proof that you've successfully authenticated with Google.

Now, the website you're signing up for can use this access token to access some limited information from your Google account, such as your name and email address. This way, you don't have to share your actual Google credentials with the new website, ensuring your security and privacy.

Here's a simplified code snippet example for a Node.js Express server implementing an OAuth flow with the Passport.js library:

```javascript
const express = require('express');
const passport = require('passport');
const GoogleStrategy = require('passport-google-oauth20').Strategy;

const app = express();

// Configure Google OAuth strategy
passport.use(
  new GoogleStrategy(
    {
      clientID: 'your_client_id',
      clientSecret: 'your_client_secret',
      callbackURL: '/auth/google/callback' // URL to handle callback after authentication
    },
    (accessToken, refreshToken, profile, done) => {
      // Handle the authenticated user's profile data
      // This is where you can create or authenticate the user in your system
      // You can access user details from the 'profile' object
      // 'accessToken' is the token you can use to access Google APIs on behalf of the user
      // 'refreshToken' can be used to obtain a new access token when the current one expires
      // 'done' is a callback function to indicate the completion of the authentication process
    }
  )
);

// Create a route for initiating the Google OAuth flow
app.get('/auth/google', passport.authenticate('google', { scope: ['profile', 'email'] }));

// Create a route to handle the callback after successful authentication
app.get('/auth/google/callback', passport.authenticate('google'));

// Start the server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

Please note that this is a simplified example, and in a real-world scenario, you would need to handle error cases, store and manage user sessions, and implement proper security measures.

Remember to replace `'your_client_id'` and `'your_client_secret'` with the actual values obtained from the Google Developers Console when you create a project and enable the Google OAuth API.

## Authorization and Authentication flows

Sure! I'll explain each concept in a simplified manner and provide code snippet examples for Node.js with Express and Mongoose.

1. Authorization vs. Authentication:

   - Authentication: Imagine you have a secret club, and there's a bouncer at the entrance. To get inside, you need to prove who you are, such as showing your ID card or giving a secret password. In the digital world, authentication is the process of verifying the identity of a user, typically through credentials like usernames and passwords.

   - Authorization: Now, imagine that inside the secret club, there are different rooms with different access levels. Some rooms are only for members, while others are for VIPs. Authorization is the process of determining what resources or actions a user is allowed to access or perform once their identity has been authenticated.

2. Authorization Code Flow:
   - Authorization Code Flow is a secure way for users to authenticate and authorize third-party applications to access their data.

   - Example code snippet (Node.js with Express):

    ```javascript
    const express = require('express');
    const app = express();

    app.get('/login', (req, res) => {
      // Redirect the user to the authorization server
      res.redirect('https://authorization-server.com/authorize?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=YOUR_REDIRECT_URI');
    });

    app.get('/callback', (req, res) => {
      const authorizationCode = req.query.code;
      // Exchange the authorization code for an access token
      // Use the access token to make requests on behalf of the user
      // ...
      res.send('Authentication successful!');
    });

    app.listen(3000, () => {
      console.log('Server running on port 3000');
    });
    ```

3. Authorization Code Flow with Proof Key for Code Exchange (PKCE):
   - PKCE is an extension of the Authorization Code Flow, adding an extra layer of security to prevent authorization code interception attacks.

   - Example code snippet (Node.js with Express):

    ```javascript
    const crypto = require('crypto');

    // Generate a random code verifier
    const codeVerifier = crypto.randomBytes(32).toString('hex');

    // Calculate the code challenge from the code verifier
    const codeChallenge = crypto
      .createHash('sha256')
      .update(codeVerifier)
      .digest('base64')
      .replace(/\+/g, '-')
      .replace(/\//g, '_')
      .replace(/=+$/, '');

    // Include the code challenge in the authorization request
    const authorizationUrl = `https://authorization-server.com/authorize?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=YOUR_REDIRECT_URI&code_challenge=${codeChallenge}&code_challenge_method=S256`;
    ```

4. Implicit Flow with Form Post:
   - Implicit Flow is a simplified flow used for client-side applications where the access token is returned directly to the client.

   - Example code snippet (Node.js with Express):

    ```javascript
    const express = require('express');
    const app = express();

    app.get('/login', (req, res) => {
      // Redirect the user to the authorization server
      res.redirect('https://authorization-server.com/authorize?response_type=token&client_id=YOUR_CLIENT_ID&redirect_uri=YOUR_REDIRECT_URI');
    });

    app.post('/callback', (req, res) => {
      const accessToken = req.body.access_token;
      // Use the access token to make requests on behalf of the user
      // ...
      res.send('Authentication successful!');
    });

    app.listen(3000, () => {
      console.log('Server running on port 3000');
    });
    ```

5. Client Credentials Flow:
    - Client Credentials Flow is used when a client application needs to authenticate itself and directly access resources on behalf of itself, rather than a specific user.

    - Example code snippet (Node.js with Express):

    ```javascript
    const axios = require('axios');

    const clientId = 'YOUR_CLIENT_ID';
    const clientSecret = 'YOUR_CLIENT_SECRET';

    axios.post('https://authorization-server.com/token', {
        grant_type: 'client_credentials',
        client_id: clientId,
        client_secret: clientSecret
      })
      .then(response => {
        const accessToken = response.data.access_token;
        // Use the access token to access protected resources
        // ...
      })
      .catch(error => {
        console.error('Error:', error.message);
      });
    ```

6. Device Authorization Flow:
   - Device Authorization Flow is used for devices that have limited input capabilities and cannot interactively authenticate like a regular web application.
   - Example code snippet (Node.js with Express):

    ```javascript
    const axios = require('axios');

    axios.post('https://authorization-server.com/device/code', {
        client_id: 'YOUR_CLIENT_ID',
        scope: 'requested_scope'
      })
      .then(response => {
        const userCode = response.data.user_code;
        const verificationUri = response.data.verification_uri;
        console.log(`Please visit ${verificationUri} and enter the code ${userCode} to authenticate.`);
      })
      .catch(error => {
        console.error('Error:', error.message);
      });
    ```

7. Resource Owner Password Flow:
   - Resource Owner Password Flow allows clients to directly authenticate with the authorization server by sending the user's credentials.
   - Example code snippet (Node.js with Express):

```javascript
const axios = require('axios');

axios.post('<https://authorization-server.com/token>', {
    grant_type: 'password',
    client_id: 'YOUR_CLIENT_ID',
    client_secret: 'YOUR_CLIENT_SECRET',
    username: 'USER_USERNAME',
    password: 'USER_PASSWORD'
  })
  .then(response => {
    const accessToken = response.data.access_token;
    // Use the access token to access protected resources
    // ...
  })
  .catch(error => {
    console.error('Error:', error.message);
  });
 ```
