<p class="page-title">Authentication with oAuth 2 </p>

IGV supports [oAuth 2](https://oauth.net/2/) protocol for authenticated access to protected resources.  Authentication
for Google Cloud Storage is provided out-of-the-box through an IGV project, however users may configure IGV to use
another project for authentication as described below.  For Amazon authentication with Cognito see the UMCCR
step-by-step documentation for [backend](https://umccr.org/blog/igv-amazon-backend-setup/)
and [frontend](https://umccr.org/blog/igv-amazon-frontend-setup/).

IGV uses the [Authorization Code Flow with Proof Key for Code Exchange (PKCE).](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce)
This flow requires a redirect URI to receive an authorization code after user authenticat.  This redirect URI is

```
http://localhost:port/oauthCallback
```

where `port` is the IGV listener port, 60151 by default.  If the port is disabled IGV will attempt to open it during
the authorization code flow.  If the port cannot be opened oAuth authorization will fail.


Customization
Configuring an OAuth provider

**Required**

* client_id
* authorization_endpoint
* token_endpoint

**Optional** - may be required by some providers

* client_secret
* auth_provider - Used to name a menu to provide a logout option.
* app_id_uri - Sometimes required by Microsoft Azure.   Passed to the authorization_endpoint as parameter "resource".
* scope - Scope of the authorization request.

**Optional** - 

* hosts - Array of host strings for this authorization provider.  URLs with these hosts will require authentication.

##Examples

Note all keys, secrets, etc are random strings and presented for illustration only.


**Google** 
```json
{
"client_id": "YOUR_CLIENT_ID",
"client_secret": "YOUR_CLIENT_SECRET",
"authorization_endpoint": "https://accounts.google.com/o/oauth2/auth",
"token_endpoint": "https://accounts.google.com/o/oauth2/token",
"auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
"hosts": ["www.googleapis.com", "storage.cloud.google.com", "storage.googleapis.com"]
}
```

**Amazon Cognito**
```json
{
"apiKey": "",
"project_id": "igv",
"auth_provider": "Amazon",
"auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
"aws_region": "ap-southeast-2",
"scope": "email%20openid%20profile",
"client_id": "3f4ujenfmr77tg12iofbebpkoh",
"client_secret": "en1q6638m4dogrr6erhosetim67sjilc6htjnfmf6ljk2q3j9og",
"authorization_endpoint": "https://igv-demo.auth.ap-southeast-2.amazoncognito.com/login",
"token_endpoint": "https://igv-demo.auth.ap-southeast-2.amazoncognito.com/token",
"aws_cognito_fed_pool_id": "ap-southeast-2:15b7bf93-18ca-40d5-99e9-38b4eb69363e",
"aws_cognito_pool_id": "ap-southeast-2_IYMvlZzmv",
"aws_cognito_role_arn": "arn:aws:iam::YOUR_AWS_ACCOUNT:role/YOUR_Cognito_igvAuth_Role"
}
```

**Microsoft**
```json
{
  "client_id": "hbq82djj-wxky-7iub-j7zq-7i8nv72n48nq",
  "client_secret": "cVAX64fXRikCLmtLEb/cktrAtaHz/tmB3WegtnbXN2Gq",
  "authorization_endpoint": "https://login.microsoftonline.com/77nwe2q2-e11k-uq2p-7vdh-9z7px83zmtiv/oauth2/authorize",
  "token_endpoint": "https://login.microsoftonline.com/77nwe2q2-e53r-lk5z-7vdh-9z7px83zmtiv/oauth2/token",
  "hosts": ["prod.mayo.edu", "dev.mayo.edu", "int.mayo.edu"],
  "auth_provider": "Mayo Clinic",
  "app_id_uri": "https://orgtools.onmicrosoft.com/6q9qk3mr-tw99-eu73-rt3k-nqw2aqidutm9",
  "scope": "openid",
  "find_string": "dept",
  "replace_string": "dept-oauth2"
}
```
