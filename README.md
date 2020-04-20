<div align="center"><img src="https://johnson-yi.github.io/images/logos/logos-scorpion.svg" height="128" /></div>

Samling
===

*(Note: This fork has additional features over the upstream project [capriza/samling](https://github.com/capriza/samling).)*

Serverless (as in "client side only") SAML IDP for testing SAML integrations.

## See it Live

Visit https://johnson-yi.github.io/samling/samling.html to see it in action.

## What is SAMLING

SAMLING is a Serverless (as-in client side only) SAML IdP for the purpose of testing SAML integrations.

It provides control over the SAML response properties to send back to the Service Provider in response to a SAML request,
including simulating errors and specifying session cookie duration to track the logged-in user.

If there is a <strong>SAMLRequest</strong> query parameter present with an `AuthnRequest`,
SAMLING will auto populate some of the fields in the `SAML Response Properties` section in preparation for creating the SAML response.

If there is a <strong>SAMLRequest</strong> query parameter present with a `LogoutRequest`,
SAMLING will log out the currently logged-in user.

Generating a SAML Response requires the use of a private key and certificate for signing the SAML Assertion.
SAMLING comes bundled with default keys, but also enables to generate a random private/public key and to save them in the local storage so they are used in
subsequent SAML responses.

## Installation

```bash
git clone https://github.com/johnson-yi/samling.git
cd samling
npm install
npm run build
```

You'll end up with a `public` directory with all the required assets for loading `samling.html`.

## Docker

Note: Docker 17.05 or higher is required.

```bash
git clone https://github.com/johnson-yi/samling.git
cd samling
docker build -t johnson-yi/samling .
docker run -d -p 8080:80 johnson-yi/samling
```
You can now access samling at http://localhost:8080

## How to Use

### SAMLRequest with AuthnRequest

Use `https://johnson-yi.github.io/samling/samling.html?SAMLRequest=<SAML_REQUEST>` to initiate a login request via samling.
Specifying `ForceAuthn="true"` in the request will force Samling to land on the properties page instead of auto submitting the SAML response
in case the user is already logged-in.

### SAMLRequest with LogoutRequest

Use `https://johnson-yi.github.io/samling/samling.html?SAMLRequest=<SAML_REQUEST>` to initiate a logout request.
If there is an active user session, the SAML Response will be automatically posted back.

Add `manual=1` query parameters to the url to logout manually instead of the response being automatically posted back.

### IdP Metadata

Use `https://johnson-yi.github.io/samling/public/metadata.xml` to obtain the _default_ IdP metadata of Samling. Note that the downloadable metadata contains the default public certificate of samling - it is not suitable for generated keys. If you generate a new key pair you can obtain the metadata with the correct certificate from the "IdP Metadata" view.

### Manual Usage

1. Open up `https://johnson-yi.github.io/samling/samling.html`. You'll land on the **SAML Response Properties** section.
2. Fill in the required properties fields. Required fields are marked with an asterisks (*).
   * `Name Identifier` - the user name
   * `Assertion Consumer URL` - where to send the SAML response
3. Click on **Create Response**. You will be be taken the **SAML Response** section.
4. Review the SAML response and set the session duration, then click on **Post Response**. At this point a session cookie
   is created for the logged in user.
5. You can reload the samling page and go to the **User Details** page to verify the session cookie was created.

## License

The MIT License (MIT)

Copyright (c) 2016 Capriza Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

