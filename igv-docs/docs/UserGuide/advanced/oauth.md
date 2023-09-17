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

... some words on customization

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

**Microsoft**
```json
{
"client_id": "YOUR_CLIENT_ID",
"client_secret": "YOUR_CLIENT_SECRET",
"authorization_endpoint": "https://login.microsoftonline.com/.../oauth2/authorize",
"token_endpoint": "https://login.microsoftonline.com/.../oauth2/token",
"auth_provider": "YOUR PROVIDER",
"app_id_uri": "https://orgtools.onmicrosoft.com/...",
"scope": "openid"
"hosts": ["prod_host.myorg.edu", "dev_host.myorg.edu", "int_host.myorg.edu"],
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