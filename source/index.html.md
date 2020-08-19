---
title: PEX API Reference v2020.6.17.3
language_tabs:
  - http: HTTP
  - javascript: JavaScript
language_clients:
  - http: ""
  - javascript: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="pex-api-reference">PEX API Reference v2020.6.17.3</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

# Introduction
PEX is a commercial prepaid card that helps your company control employee spending. You can issue cards, add funds to cards, and apply spend controls (including restricting specific merchant categories) through our web or mobile applications which includes 24/7 access to your PEX account. The PEX platform is also available through a complete set of JSON-based APIs which can be used to duplicate every feature available in our Admin portal, and to support a few features that aren’t. The PEX platform can be used to power any proprietary expense management or business payment application to create a seamless payment experience for your users.

Base URLs:

* <a href="https://coreapi.pexcard.com/v4">https://coreapi.pexcard.com/v4</a>

<h1 id="pex-api-reference-get-started">Get Started</h1>

## Generate a new access token

<a id="opIdToken_PostByuserRequestAuthorizationPOSTToken"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Token HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: basic 

```

```javascript
const inputBody = '{
  "Username": "",
  "Password": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'basic '
};

fetch('https://coreapi.pexcard.com/v4/Token',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Token`

Create a token.<br/>
<br/>
A token is required to make all API calls. The life of a token is six (6) months.<br/>
<br/>
Tokens are the equivalent of a username/password combination and must not be shared or distributed to untrusted parties.<br/>
<br/>
Token authentication is only secure if SSL is used. Therefore, all requests (both to obtain and use the tokens) must use HTTPS endpoints. Please follow the best practices using SSL - peers should always be verified. To find our latest VeriSign certificate, please go to <A href="https://coreapi.pexcard.com" target="_blank">https://coreapi.pexcard.com</A>.<br/>
<br/>
If you are a partner (API user), your customer will provide a PEX administrator or cardholder username/password that you (partner) will generate the token from. You (partner) then use that token to authenticate.<br/>
<br/>
If you are a customer, you received your API username/password from PEX Operations.<br/>  
<br/>
Before creating your first token the following pre-steps are required:<br/>
<list type="number">
<item>1. On developer.pexcard.com, select Dashboard in the blue menu bar.</item><br/>
<item>2. In the API Keys section, click on the lock and key icons to show the values on the screen. If you have access to both Beta and Production, each will be listed separately.</item><br/>
<item>3. From the returned (beta or production) values, create a Base64 encoded value for authorization. To do this you can use a simple tool like the one found here <A href="https://www.base64encode.org" target="_blank">https://www.base64encode.org</A>.
The input should be in the following format: ClientID:ClientSecret. (HELPFUL TIP: If you copy the copy and paste the ClientId and ClientSecret please be sure that no extra characters or spaces are included. Correct: <b>ClientID:ClientSecret</b> Incorrect: <b>ClientID: ClientSecret</b>)</item></br>
<item>4. The returned encoded value should be used in all API calls.</item><br/>
</list>
Note: To see the Curl example -  in the Authorization field, prepend the word basic to the Base64 encoded value, for example,<br/>
<b>basic MmRlMWZjZgq6OTU0MzQwYmY3OGIwNjFjnJcxIIY0MWM2NWE4NWIxPPO=</b><br/>

> Body parameter

```json
{
  "Username": "",
  "Password": ""
}
```

<h3 id="generate-a-new-access-token-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|basic {Base64Encoded appId:appSecret}|
|body|body|[PostTokenRequest](#schemaposttokenrequest)|true|Username and password|

> Example responses

> 201 Response

```json
{
  "Token": ""
}
```

<h3 id="generate-a-new-access-token-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[PostTokenResponse](#schemaposttokenresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|<list type="number">
  <item>
    <description>- Invalid authorization parameter (appId:appSecret as base64)<br /></description>
  </item>
  <item>
    <description>- Invalid username or password</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-token-manage-authentication-for-the-pex-api-">Token : 
                Manage authentication for the PEX API.
            </h1>

## Return details associated with the token or return list of tokens details for basic auth

<a id="opIdToken_GetByAuthorizationGETToken"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Token HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Token',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Token`

Determine which API user a token belongs to, as well as the token expiration date.<br/>
<br/>
Once the token expires, it cannot be retrieved, renewed or deleted.<br/>
<br/>
The following error responses will result in PEX deleting the token (after the first error):<br/>
‘401: Password has changed’ (API user has changed the password)<br/>
‘403: User is not active’ (API user is terminated/closed)<br/>
‘403: Token expired or does not exist’.<br/> 
<br/> 
If you receive any of the above errors, you will need to contact the API user for further instructions.

<h3 id="return-details-associated-with-the-token-or-return-list-of-tokens-details-for-basic-auth-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|basic {Base64Encoded appId:appSecret} / token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Tokens": [
    {
      "Username": "",
      "AppId": "",
      "Token": "",
      "TokenExpiration": ""
    }
  ]
}
```

<h3 id="return-details-associated-with-the-token-or-return-list-of-tokens-details-for-basic-auth-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetTokenResponse](#schemagettokenresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Revoke access for the authenticated user

<a id="opIdToken_DeleteByAuthorizationDELETEToken"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Token HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript

const headers = {
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Token',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Token`

To revoke API access, delete the token.<br/>
<br/>
The following error responses will result in PEX deleting the token (after the first error):<br/>
‘401: Password has changed’ (Administrator has changed the password)<br/>
‘403: User is not active’ (Administrator is terminated/closed)<br/>
‘403: Token expired or does not exist’.<br/> 
<br/>  
If the token will expire in one month or less, use POST /Token/Renew.

<h3 id="revoke-access-for-the-authenticated-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

<h3 id="revoke-access-for-the-authenticated-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Password has changed’ (Administrator has changed the password)|None|
|402|[Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2)|User is not active’ (Administrator is terminated/closed)|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Token expired or does not exist|None|

<aside class="success">
This operation does not require authentication
</aside>

## Reissue token prior to expiration

<a id="opIdToken_RenewByAuthorizationPOSTToken/Renew"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Token/Renew HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Token/Renew',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Token/Renew`

Reissue an existing token. A new token will be generated based on your existing valid token.  This end-point does not extend the expiration date of an existing token.<br/>
<br/>
All tokens expire 6 months after creation. You can reissue the token one (1) month prior to its expiration date. Once the token is expired, it cannot be renewed and you will need to generate a new one.<br/>
<br/>
If you know a token has been compromised, please delete it and generate a new one.<br/>
<br/>
To get the expiration date of a token, use GET /Token.

<h3 id="reissue-token-prior-to-expiration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Username": "",
  "Token": "",
  "AppId": "",
  "TokenExpiration": ""
}
```

<h3 id="reissue-token-prior-to-expiration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[RenewTokenResponse](#schemarenewtokenresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Cannot renew token|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return all tokens for the business

<a id="opIdToken_GetAuthTokensByAuthorizationGETToken/GetAuthTokens"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Token/GetAuthTokens HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Token/GetAuthTokens',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Token/GetAuthTokens`

List all tokens for the business, including the expiration date/time.

<h3 id="return-all-tokens-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|basic {Base64Encoded appId:appSecret} / token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Tokens": [
    {
      "Token": "",
      "SecondsUntilExpire": 0,
      "ExpirationTime": ""
    }
  ]
}
```

<h3 id="return-all-tokens-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetAllTokensResponse](#schemagetalltokensresponse)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-card-create-activate-and-fund-cards-setup-rules-for-spending-and-scheduled-funding-">Card : 
             Create, activate, and fund cards. Setup rules for spending and scheduled funding.
            </h1>

## Return all advanced spend rules for a specified card accountID

<a id="opIdCard_AdvancedSpendRulesByIdAuthorizationGETCard/SpendRules/{id}/Advanced"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Card/SpendRules/{id}/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SpendRules/{id}/Advanced',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Card/SpendRules/{id}/Advanced`

Return all advanced spend rules for a specified card accountID.<br/>
<br/>
Advanced spend rules dictate where a card can be used to make purchases.<br/>
<br/>
Cardholders using PEX card do not have cash access. ATMs, Money Orders, Money Remittance (e.g. MoneyGram) and other cash transactions, such as purchasing casino chips, will be declined at all times.<br/>
<br/>
At card creation, the advanced spend rule defaults are:<br/>
<list type="number">
<item><description>- Daily spend limit NONE<br/></description></item>
<item><description>- Weekly spend limit NONE<br/></description></item>
<item><description>- Monthly spend limit NONE<br/></description></item>
<item><description>- Yearly spend limit NONE<br/></description></item>
<item><description>- Lifetime spend limit NONE<br/></description></item>
<item><description>- International spending is OFF<br/></description></item>
<item><description>- All merchant categories are ON.<br/></description></item>
</list>
<br/>
CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone. 
True - Can use when card is not present. 
False - Cannot use when card is not present.
<br/>
PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):<br/>
<list type="number">
<item><description>- Associations &amp; organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
<item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
<item><description>- Educational services: Schools, training programs<br/></description></item>
<item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
<item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets<br/></description></item>
<item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
<item><description>- Healthcare &amp; Childcare services: Medical services, hospitals, daycare<br/></description></item>
<item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
<item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
<item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
<item><description>- Travel &amp; transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
<item><description>- Fuel Pump Only: Outdoor fuel pumps(i.e. Pay at the Pump).</description></item>
</list>

<h3 id="return-all-advanced-spend-rules-for-a-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AdvancedSpendRules": {
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ],
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}
```

<h3 id="return-all-advanced-spend-rules-for-a-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetAdvancedSpendRulesResponse](#schemagetadvancedspendrulesresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type='number'><item><description>- Invalid card account ID<br/></description></item><item><description>- Must be card account ID<br/></description></item></list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create advanced spend rules for a specified card accountID

<a id="opIdCard_AdvancedSpendRulesByidUserRequestAuthorizationPUTCard/SpendRules/{id}/Advanced"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/SpendRules/{id}/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json

Authorization: string

```

```javascript
const inputBody = '{
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalSpendEnabled": false,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SpendRules/{id}/Advanced',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/SpendRules/{id}/Advanced`

Create advanced spend rules for a specified card accountID.<br/>
<br/>
Advanced spend rules dictate where a card can be used to make purchases and can be used to set a per day spending limit. Changes to spend rules happen in real-time. Be sure the cardholder is aware of the limitations being set.<br/>
<br/>
If your business allows cardholders to "Use your PEX Account balance" for transactions, you must set a value for "DailySpendLimit" for those cardholders. The "DailySpendLimit" value must be less than or equal to the PEX assigned daily spend limit for your business (typically $5,000 USD).<br/>
<br/>
Cardholders using PEX do not have cash access. ATMs, Money Orders, Money Remittance (e.g. MoneyGram) and other cash transactions, such as purchasing casino chips, will be declined at all times.<br/>
<br/>
CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone.<br/>
True - Can use when card is not present.<br/>
False - Cannot use when card is not present. <br/>
<br/>
International spending is turned OFF by default. To keep fraud to a minimum, we suggest you leave ‘InternationalSpendEnabled’ = false. If a cardholder is traveling internationally, or needs to make purchases from international websites/merchants, change ‘InternationalSpendEnabled’ = true. US sanctioned countries will always be declined, see list of sanctioned countries on dashboard.pexcard.com in FAQ (found in the footer).<br/>
<br/>
Padding for Restaurant: At non-fast food locations, card authorization is (typically) for total plus 20&#37; of total (ex. bill total $56.00 + $11.20 (20&#37;) = $67.20 authorization amount). If the cardholder spends at restaurants, please be sure to allow for the additional 20&#37;.<br/>
<br/>
Gas Purchases at Automated Fuel Dispensers (AFDs): AFDs  will authorize for a minimum $50.00 and settle for the amount of gas pumped (whether the purchase is above or below $50.00). So setting a daily spend limit of $30.00 means a cardholder cannot purchase fuel at the gas pump.<br/>
<br/>
PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):
<list type="number">
<item><description>- Associations &amp; organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
<item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
<item><description>- Educational services: Schools, training programs<br/></description></item>
<item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
<item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets<br/></description></item>
<item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
<item><description>- Healthcare &amp; Childcare services: Medical services, hospitals, daycare<br/></description></item>
<item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
<item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
<item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
<item><description>- Travel &amp; transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
<item><description>- Fuel Pump Only: Outdoor fuel pumps(i.e. Pay at the Pump).</description></item>
</list>

> Body parameter

```json
{
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalSpendEnabled": false,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

<h3 id="create-advanced-spend-rules-for-a-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SetAdvancedSpendRulesRequest](#schemasetadvancedspendrulesrequest)|true|Advacne spend rule data|

<h3 id="create-advanced-spend-rules-for-a-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|<list type='number'><item><description>- Invalid card account ID<br/></description></item><item><description>- Invalid merchant category<br/></description></item><item><description>- Merchant categories duplicated<br/></description></item><item><description>- Merchant spend limit exceeds overall spend limit<br/></description></item></list>|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type='number'><item><description>- Account closed<br/></description></item><item><description>- Invalid card account ID<br/></description></item><item><description>- Must be card account ID<br/></description></item><item><description>- This business does not support the Customer Authorization Decision<br/></description></item><item><description>- This business does not support the PEX Account balance instead of card balance<br/></description></item></list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a 4-digit PIN and associate it with a card accountID

<a id="opIdCard_SetPinByIdUserRequestAuthorizationPUTCard/SetPin/{Id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/SetPin/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Pin": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SetPin/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/SetPin/{Id}`

Create a 4-digit PIN and associate it with a card accountID.<br/>
<br/>
There is no cash access and a PEX card cannot be used to obtain cash from an ATM, POS or by any other means.<br/>
<br/>
You can set a PIN to allow your cardholder to shop at some stores that require PINs, e.g. Sam's Club and Costco.<br/>
<br/>
The PIN is secure and cannot be viewed online or by customer service. If the cardholder forgets the PIN, a new PIN must be created.<br/>
<br/>
If the cardholder uses an incorrect PIN five (5) times, the system will block the card for fraud. To remove the block, call customer service (1-866-685-1898) or create a new PIN - SetPIN will unblock the card and set the failure count to 0.<br/>
<br/>
A PIN must:<br/>
<list type="number">
<item><description>- be four (4) digits<br/></description></item>
<item><description>- not be all the same digit, ex. 1111<br/></description></item>
<item><description>- not be digits in sequence, ex. 1234<br/></description></item>
<item><description>- not match the last four (4) digits of the card number.<br/></description></item>
</list>
<br/>

> Body parameter

```json
{
  "Pin": ""
}
```

<h3 id="create-a-4-digit-pin-and-associate-it-with-a-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SetCardholderPinRequest](#schemasetcardholderpinrequest)|true|4 digit PIN|

> Example responses

> 200 Response

```json
{}
```

<h3 id="create-a-4-digit-pin-and-associate-it-with-a-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
</list>|None|

<h3 id="create-a-4-digit-pin-and-associate-it-with-a-card-accountid-responseschema">Response Schema</h3>

Status Code **200**

*IHttpActionResult*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Set a group for the card account

<a id="opIdCard_SetGroupByGroupRequestAuthorizationPUTCard/SetGroup"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/SetGroup HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "GroupId": 0,
  "AcctId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SetGroup',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/SetGroup`

Insert a card accountID into a specified group.<br/>
<br/>
For a definition of group see POST /Group/Group.

> Body parameter

```json
{
  "GroupId": 0,
  "AcctId": 0
}
```

<h3 id="set-a-group-for-the-card-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SetCardholderGroupRequest](#schemasetcardholdergrouprequest)|true|Group ID and Account ID|

> Example responses

> 200 Response

```json
{}
```

<h3 id="set-a-group-for-the-card-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Invalid group ID</description>
  </item>
</list>|None|

<h3 id="set-a-group-for-the-card-account-responseschema">Response Schema</h3>

Status Code **200**

*HttpResponseMessage*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Fund a specified card accountID to zero ($0)

<a id="opIdCard_ZeroByidAuthorizationPOSTCard/Zero/{id}"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Card/Zero/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Zero/{id}',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Card/Zero/{id}`

Fund a specified card accountID to zero ($0).<br/>
<br/>
Specify a card accountID and funds from the business account will be added/removed so that the card account (available) balance = $0.00.

<h3 id="fund-a-specified-card-accountid-to-zero-($0)-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "AvailableBalance": 0,
  "LedgerBalance": 0
}
```

<h3 id="fund-a-specified-card-accountid-to-zero-($0)-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[FundResponse](#schemafundresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Card Account ID does not exist<br /></description>
  </item>
  <item>
    <description>- Must be card account ID<br /></description>
  </item>
  <item>
    <description>- Insufficient funds on business<br /></description>
  </item>
  <item>
    <description>- Invalid amount</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return all cards for a CardOrderId

<a id="opIdCard_CardOrderByIdAuthorizationGETCard/CardOrder/{id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Card/CardOrder/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/CardOrder/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Card/CardOrder/{id}`

After using POST /Card/CreateAsync to create one or more cards, you can retrieve the card information, including the card AccountId, by using this call.

<h3 id="return-all-cards-for-a-cardorderid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card order ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "BusinessAccountId": 0,
  "Cards": [
    {
      "AcctId": 0,
      "Status": "",
      "FirstName": "",
      "MiddleName": "",
      "LastName": "",
      "DateOfBirth": "",
      "HomePhone": "",
      "MobilePhone": "",
      "Email": "",
      "HomeAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "ShippingAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "Recipient": "",
      "ShipToShippingAddress": false,
      "ShippingContactNumber": "",
      "BundleCards": false,
      "ShippingMethod": "",
      "ShippingDate": "",
      "Errors": [
        {
          "Code": "",
          "Message": ""
        }
      ],
      "FailReason": "",
      "AccountNumber": "",
      "SpendingRulesetId": 0,
      "GroupId": 0,
      "CustomId": ""
    }
  ]
}
```

<h3 id="return-all-cards-for-a-cardorderid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[CardOrderResponse](#schemacardorderresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Order belongs to another business|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get general information about card orders

<a id="opIdCard_CardOrderByStartDateEndDateAuthorizationGETCard/CardOrder?StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Card/CardOrder HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/CardOrder',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Card/CardOrder`

This endpoint returns all the card order Ids those were created in the duration specified by Start date and End date. <br/>
With the CardOrderId from response you can use GET/Card/CardOrder/{Id} to get more information about the cards created within that CardOrder. <br/>
Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
CardOrderId: Order ID returned as a response to POST/Card/CreateAsync, when you submit card creation request. <br/>
OrderDateTime: Date time when the card order was placed. <br/>
UserName: Username of the user who placed the order <br/>
BusinessAdminId: Unique identifier for the business admin who placed the card order. More information about admin can be obtained by GET/Business/Admin/{Id}. It can have null value in some cases. <br/>
BusinessAccountId: Account Id to which card order belongs to. <br/>
NumberofCards: Total count of number of cards successfully created in the card order. <br/>

<h3 id="get-general-information-about-card-orders-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|StartDate|query|string(date-time)|false|Start date (format - YYYY-MM-DDThh:mm:ss)|
|EndDate|query|string(date-time)|false|End date (format - YYYY-MM-DDThh:mm:ss)|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "CardOrders": [
    {
      "CardOrderId": 0,
      "OrderDateTime": "",
      "UserName": "",
      "BusinessAdminId": 0,
      "BusinessAccountId": 0,
      "NumberOfCards": 0
    }
  ]
}
```

<h3 id="get-general-information-about-card-orders-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetCardOrderResponse](#schemagetcardorderresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return profile data associated with a single card accountID

<a id="opIdCard_ProfileByIdAuthorizationGETCard/Profile/{id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Card/Profile/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Profile/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Card/Profile/{id}`

Return profile data associated with a single card accountID.<br/>
<br/>
Definition of some of the returned fields and how the PEX system uses them:<br/>
<list type="number">
<item><description>- AccountId: Card account ID. 0 will be returned as the Account ID for cards that are pending.<br/></description></item>
<item><description>- CardholderGroupID: Unique identifier for the group (for a definition of group see POST /Group/Group.)<br/></description></item>
<item><description>- Profile address: The cardholder billing address.<br/></description></item>
<item><description>- Shipping address: Used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/></description></item>
<item><description>- SpendRulestId in the response lets user know the associated SpendingRuleset with the card account specified in the request.<br/></description></item>
<item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
<item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field.<br/></description></item>
</list>
<br/>
To retrieve all information stored against a card accountID, including spend and funding rules, use GET /Details/AccountDetails/{Id}.

<h3 id="return-profile-data-associated-with-a-single-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "AccountStatus": "",
  "FirstName": "",
  "LastName": "",
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CustomId": ""
}
```

<h3 id="return-profile-data-associated-with-a-single-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[GetProfileResponse](#schemagetprofileresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Must be card account ID|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Invalid card account ID|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update profile data for a specified card accountID.

<a id="opIdCard_ProfileByidUserRequestAuthorizationPUTCard/Profile/{id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/Profile/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "Phone": "",
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "CustomId": "",
  "FirstName": "",
  "LastName": "",
  "NormalizeProfileAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "NormalizeShippingAddress": false,
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Profile/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/Profile/{id}`

All fields are optional for update, however, some profile fields are required in the system and cannot be replaced by null or empty strings. The API user must have AddEditTerminateCard = true.<br/>
<br/>
Required profile fields:<br/>
<list type="number">
<item><description>- First Name<br/></description></item>
<item><description>- Last Name<br/></description></item>
<item><description>- Profile Address Line 1<br/></description></item>
<item><description>- Profile City<br/></description></item>
<item><description>- Profile State<br/></description></item>
<item><description>- Profile Zip<br/></description></item>
<item><description>- Shipping Address Line 1<br/></description></item>
<item><description>- Shipping City<br/></description></item>
<item><description>- Shipping Status<br/></description></item>
<item><description>- Shipping Zip<br/></description></item>
<item><description>- Phone<br/></description></item>
<item><description>- Email<br/></description></item>
<item><description>- Date of Birth.<br/></description></item>
</list>
<br/>
To find the group name associated with a ‘CardholderGroupId’, use GET /Details/AccountDetails.<br/>
CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/>
<br/>
User can specify SpendRulesetId in the request to associate an account with SpendingRuleset. <br/>
If SpendRulesetId value in request is null, account will be disassociated from a SpendingRuleset.<br/>
<br/>
If PEX card is used for fuel authorizations, transit passes or online purchases, there will be times where the cardholder will have to key in the billing zip code as it appears on the cardholder profile. To avoid issues at the time of purchase, let the cardholder know what their billing (i.e. profile) address is.<br/>
<br/>
If the cardholder enters an invalid Zip Code 2 times, the merchant may refuse to accept additional card swipes. If this occurs, cardholders will have to see the attendant to complete a gas transaction, or use another form of payment.<br/>
<br/>
If the cardholder should have access to dashboard.pexcard.com to review their transaction history, etc., they will need the four (4) digit year of birth from their profile. If you are using a generic value, you will need to convey that to the cardholder.

> Body parameter

```json
{
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "Phone": "",
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "CustomId": "",
  "FirstName": "",
  "LastName": "",
  "NormalizeProfileAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "NormalizeShippingAddress": false,
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  }
}
```

<h3 id="update-profile-data-for-a-specified-card-accountid.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateProfileRequest](#schemaupdateprofilerequest)|true|Profile data|

> Example responses

> 200 Response

```json
{}
```

<h3 id="update-profile-data-for-a-specified-card-accountid.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID<br /></description>
  </item>
  <item>
    <description>- Card group not found</description>
  </item>
</list>|None|

<h3 id="update-profile-data-for-a-specified-card-accountid.-responseschema">Response Schema</h3>

Status Code **200**

*HttpResponseMessage*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Create cards for the business

<a id="opIdCard_CreateAsyncByUserRequestAuthorizationPOSTCard/CreateAsync"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Card/CreateAsync HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Cards": [
    {
      "Phone": "",
      "ShippingPhone": "",
      "ShippingMethod": "",
      "DateOfBirth": "",
      "Email": "",
      "GroupId": 0,
      "RulesetId": 0,
      "CustomId": "",
      "FirstName": "",
      "LastName": "",
      "NormalizeProfileAddress": false,
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "NormalizeShippingAddress": false,
      "ShippingAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      }
    }
  ],
  "NormalizeHomeAddress": false,
  "NormalizeShippingAddress": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/CreateAsync',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Card/CreateAsync`

Create cards for the business. The response to this call is a CardOrderId.<br/>
<br/>
To retrieve card details, including the card AccountId, use GET /Card/CardOrder/{Id}<br/>
<br/>
Cards have an expiration date of 3 years and will renew automatically 60 days prior to expiration. If the card expiration is 01/17, the card will expire on the last day of the month, January 31, 2017.<br/>
<br/>
ShippingMethod is a required field and maps to the same choices available on the admin website:<br/>
<list type="number">
<item><description>ShippingMethod = 0  i.e 'FirstClassMail' (10-15 business days) Free<br/></description></item>
<item><description>ShippingMethod = 1  i.e 'Expedited' (up to 4 business days) $35<br/></description></item>
<item><description>ShippingMethod = 2  i.e 'Rush' (up to 3 business days) $45.<br/></description></item>
</list>
<br/>
non-ASCII characters. Ex: "ñ" not allowed<br/>
Cardholder name may only include letters, numbers and the following punctuation symbols: , . - & '<br/>
Cardholder first + last names must be no more than 23 characters<br/>
Email format: name@domain.com<br/>
Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
Phone format: 2125551212 or 212-555-1212<br/>
Zip Code should be 5 digits: 10018.<br/>
Address format: letters, numbers and the following punctuation symbols: . ' () , # - /<br/>
City format: letters, numbers and the following punctuation symbols: . ' () , # - /<br/>
State format:  two letter format ex. "CA" <br/>
Max AddressLine1 field length: 26 characters<br/>
Max AddressLine2 field length: 26 characters<br/>
Max City field length: 25 characters<br/>
Country: US<br/>
CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/>
<br/>
Shipping address is used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/> 
Valid Shipping address need to be populated as part of request while creating new cards.<br/>
<br/> 
If PEX card is used for fuel authorizations, transit passes or online purchases, there will be times where the cardholder will have to key in the billing zip code as it appears on the cardholder profile. To avoid issues at the time of purchase, let the cardholder know what their billing (i.e. profile) address is.<br/>
<br/>
If the cardholder enters an invalid Zip Code 2 times, the merchant may refuse to accept additional card swipes. If this occurs, cardholders will have to see the attendant to complete a gas transaction, or use another form of payment.<br/> 
<br/>
If the cardholder should have access to dashboard.pexcard.com to review their transaction history, etc., they will need the four (4) digit year of birth from their profile. If you are using a generic value, you will need to convey that to the cardholder.<br/>
<br/>
At card creation, the spend rule defaults are:<br/>
<list type="number">
<item><description>- Daily spend limit is NONE<br/></description></item>
<item><description>- International spending is OFF<br/></description></item>
<item><description>- Card-not-present spending is ON<br/></description></item>
<item><description>- All merchant categories are ON.<br/></description></item>
</list>
<br/>
To add a card account to a group, use GET /Group to retrieve GroupIds <br/>
To add spend rules to a card account, use GET /SpendingRuleset to retrieve all the Spend rule sets for your business. <br/>

> Body parameter

```json
{
  "Cards": [
    {
      "Phone": "",
      "ShippingPhone": "",
      "ShippingMethod": "",
      "DateOfBirth": "",
      "Email": "",
      "GroupId": 0,
      "RulesetId": 0,
      "CustomId": "",
      "FirstName": "",
      "LastName": "",
      "NormalizeProfileAddress": false,
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "NormalizeShippingAddress": false,
      "ShippingAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      }
    }
  ],
  "NormalizeHomeAddress": false,
  "NormalizeShippingAddress": false
}
```

<h3 id="create-cards-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateCardAsyncRequest](#schemacreatecardasyncrequest)|true|Profile and shipping data|

> Example responses

> 201 Response

```json
{
  "CardOrderId": 0
}
```

<h3 id="create-cards-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[CreateCardAsyncResponse](#schemacreatecardasyncresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid shipping method|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Admin does not have permission|None|

<aside class="success">
This operation does not require authentication
</aside>

## Add or remove funds to/from a card accountID

<a id="opIdCard_FundByidUserRequestAuthorizationPOSTCard/Fund/{id}"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Card/Fund/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Fund/{id}',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Card/Fund/{id}`

Add or remove funds to/from a card accountID.<br/>
<br/>
Card funding is in real-time and will change the cardholder's available balance immediately.<br/>  
<br/> 
To remove funds from the card balance, enter a negative number, for example: -10.00 will remove $10.00 from the card available balance.<br/> 
<br/>
Padding for Restaurant: At non-fast food locations, card authorization is (typically) for total plus 20&#37; of total (ex. bill total $56.00 + $11.20 (20&#37;) = $67.20 authorization amount). If the cardholder spends at restaurants, please be sure to allow for the additional 20&#37;.<br/>
<br/>
Gas Purchases at Automated Fuel Dispensers (AFDs): AFDs  will authorize for a minimum $50.00 and settle for the amount of gas pumped (whether the purchase is above or below $50.00).<br/>
<br/>
To retrieve the card accountID, use GET /Details/AccountDetails.

> Body parameter

```json
{
  "Amount": 0
}
```

<h3 id="add-or-remove-funds-to/from-a-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[FundRequest](#schemafundrequest)|true|Details required for funding a card|

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "AvailableBalance": 0,
  "LedgerBalance": 0
}
```

<h3 id="add-or-remove-funds-to/from-a-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[FundResponse](#schemafundresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID<br /></description>
  </item>
  <item>
    <description>- Insufficient funds on business<br /></description>
  </item>
  <item>
    <description>- Insufficient funds on card account<br /></description>
  </item>
  <item>
    <description>- Card available balance will exceed card limit<br /></description>
  </item>
  <item>
    <description>- Use Business Balance is enabled for card account</description>
  </item>
  <item>
    <description>- Invalid amount</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Activate a card

<a id="opIdCard_ActivateByidAuthorizationPOSTCard/Activate/{id}"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Card/Activate/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Activate/{id}',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Card/Activate/{id}`

Activate a card using the card accountID.<br/>
<br/>
A card must be activated before the cardholder can spend. For security reasons, you should not activate a card until it is received by the cardholder.<br/>
<br/>
The PEX system will prevent you from activating a card within 24 hours of creation.<br/>
<br/>
If the card is a replacement for an existing, damaged or expiring card, make sure the cardholder has the new card prior to activating it. Card activation immediately terminates all other cards on the account, including the one the cardholder is currently using. The card termination process is immediate and NOT reversible.

<h3 id="activate-a-card-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{}
```

<h3 id="activate-a-card-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Cannot change status</description>
  </item>
</list>|None|

<h3 id="activate-a-card-responseschema">Response Schema</h3>

Status Code **200**

*IHttpActionResult*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Close a specified card accountId

<a id="opIdCard_TerminateByidAuthorizationPOSTCard/Terminate/{id}"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Card/Terminate/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Terminate/{id}',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Card/Terminate/{id}`

Close a specified card accountId.<br/>
<br/>
Card/Terminate completely closes the card account. Any remaining funds on the card account are returned to the main PEX business account. This action is immediate and NOT reversible.<br/>

<h3 id="close-a-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{}
```

<h3 id="close-a-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID<br /></description>
  </item>
  <item>
    <description>- Cannot change status</description>
  </item>
</list>|None|

<h3 id="close-a-specified-card-accountid-responseschema">Response Schema</h3>

Status Code **200**

*IHttpActionResult*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## In real-time, change the card status for a specified card accountID.

<a id="opIdCard_StatusByidUserRequestAuthorizationPUTCard/Status/{id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/Status/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Status": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/Status/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/Status/{id}`

In real-time, change the card status for a specified card accountID.<br/>
<br/>
If you want to temporarily prevent a cardholder from using the card for purchases, you can change the card status from Active to Blocked. Changing card status occurs immediately on a PEX card and is reversible by using this call.<br/>
<br/>
You can either make card status Active or Blocked using this endpoint.<br/>
To change card status from Blocked to Active pass 0 in request. <br/>
To change card status from Active to Blocked pass 2 in request. <br/>
<br/>
If the card is inactive, you must activate it prior to changing the status to Blocked, use GET /Card/Activate/{Id}.<br/>
<br/>
To find current status of all cards, use GET /Details/AccountDetails/{Id}.

> Body parameter

```json
{
  "Status": ""
}
```

<h3 id="in-real-time,-change-the-card-status-for-a-specified-card-accountid.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateCardStatusRequest](#schemaupdatecardstatusrequest)|true|Status for card|

> Example responses

> 200 Response

```json
{}
```

<h3 id="in-real-time,-change-the-card-status-for-a-specified-card-accountid.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Cannot change status</description>
  </item>
</list>|None|

<h3 id="in-real-time,-change-the-card-status-for-a-specified-card-accountid.-responseschema">Response Schema</h3>

Status Code **200**

*IHttpActionResult*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Return all spend rules for a specified card accountID

<a id="opIdCard_SpendRulesByIdAuthorizationGETCard/SpendRules/{id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Card/SpendRules/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SpendRules/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Card/SpendRules/{id}`

Return all spend rules for a specified card accountID.<br/>
<br/>
Spend rules dictate where a card can be used to make purchases.<br/>
<br/>
Cardholders using PEX card do not have cash access. ATMs, Money Orders, Money Remittance (e.g. MoneyGram) and other cash transactions, such as purchasing casino chips, will be declined at all times.<br/>
<br/>
At card creation, the spend rule defaults are:<br/>
<list type="number">
<item><description>- Daily spend limit NONE<br/></description></item>
<item><description>- International spending is OFF<br/></description></item>
<item><description>- All merchant categories are ON.<br/></description></item>
</list>
<br/>
CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone. 
True - Can use when card is not present. 
False - Cannot use when card is not present.
<br/>
PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):<br/>
<list type="number">
<item><description>- Associations &amp; organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
<item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
<item><description>- Educational services: Schools, training programs<br/></description></item>
<item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
<item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets<br/></description></item>
<item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
<item><description>- Healthcare &amp; Childcare services: Medical services, hospitals, daycare<br/></description></item>
<item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
<item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
<item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
<item><description>- Travel &amp; transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
<item><description>- Fuel Pump Only: Outdoor fuel pumps(i.e. Pay at the Pump).</description></item>
</list>

<h3 id="return-all-spend-rules-for-a-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "SpendRules": {
    "UseMerchantCategory": false,
    "MerchantCategories": {
      "AssociationsAndOrganizations": false,
      "AutomotiveDealers": false,
      "EducationalServices": false,
      "Entertainment": false,
      "FuelAndConvenienceStores": false,
      "GroceryStores": false,
      "HealthcareAndChildcareServices": false,
      "ProfessionalServices": false,
      "Restaurants": false,
      "RetailStores": false,
      "TravelAndTransportation": false,
      "FuelPumpOnly": false,
      "HardwareStores": false
    },
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}
```

<h3 id="return-all-spend-rules-for-a-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[GetSpendRulesResponse](#schemagetspendrulesresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create spend rules for a specified card accountID

<a id="opIdCard_SpendRulesByidUserRequestAuthorizationPUTCard/SpendRules/{id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/SpendRules/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "MerchantCategories": {
    "AssociationsAndOrganizations": false,
    "AutomotiveDealers": false,
    "EducationalServices": false,
    "Entertainment": false,
    "FuelAndConvenienceStores": false,
    "GroceryStores": false,
    "HealthcareAndChildcareServices": false,
    "ProfessionalServices": false,
    "Restaurants": false,
    "RetailStores": false,
    "TravelAndTransportation": false,
    "FuelPumpOnly": false,
    "HardwareStores": false
  },
  "InternationalSpendEnabled": false,
  "DailySpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SpendRules/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/SpendRules/{id}`

Create spend rules for a specified card accountID.<br/>
<br/>
Spend rules dictate where a card can be used to make purchases and can be used to set a per day spending limit. Changes to spend rules happen in real-time. Be sure the cardholder is aware of the limitations being set.<br/>
<br/>
If your business allows cardholders to "Use your PEX Account balance" for transactions, you must set a value for "DailySpendLimit" for those cardholders. The "DailySpendLimit" value must be less than or equal to the PEX assigned daily spend limit for your business (typically $5,000 USD).<br/>
<br/>
Cardholders using PEX do not have cash access. ATMs, Money Orders, Money Remittance (e.g. MoneyGram) and other cash transactions, such as purchasing casino chips, will be declined at all times.<br/>
<br/>
CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone.<br/>
True - Can use when card is not present.<br/>
False - Cannot use when card is not present. <br/>
<br/>
International spending is turned OFF by default. To keep fraud to a minimum, we suggest you leave ‘InternationalSpendEnabled’ = false. If a cardholder is traveling internationally, or needs to make purchases from international websites/merchants, change ‘InternationalSpendEnabled’ = true. US sanctioned countries will always be declined, see list of sanctioned countries on dashboard.pexcard.com in FAQ (found in the footer).<br/>
<br/>
Padding for Restaurant: At non-fast food locations, card authorization is (typically) for total plus 20&#37; of total (ex. bill total $56.00 + $11.20 (20&#37;) = $67.20 authorization amount). If the cardholder spends at restaurants, please be sure to allow for the additional 20&#37;.<br/>
<br/>
Gas Purchases at Automated Fuel Dispensers (AFDs): AFDs  will authorize for a minimum $50.00 and settle for the amount of gas pumped (whether the purchase is above or below $50.00). So setting a daily spend limit of $30.00 means a cardholder cannot purchase fuel at the gas pump.<br/>
<br/>
PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):
<list type="number">
<item><description>- Associations &amp; organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
<item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
<item><description>- Educational services: Schools, training programs<br/></description></item>
<item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
<item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets<br/></description></item>
<item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
<item><description>- Healthcare &amp; Childcare services: Medical services, hospitals, daycare<br/></description></item>
<item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
<item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
<item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
<item><description>- Travel &amp; transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
<item><description>- Fuel Pump Only: Outdoor fuel pumps(i.e. Pay at the Pump).</description></item>
</list>

> Body parameter

```json
{
  "MerchantCategories": {
    "AssociationsAndOrganizations": false,
    "AutomotiveDealers": false,
    "EducationalServices": false,
    "Entertainment": false,
    "FuelAndConvenienceStores": false,
    "GroceryStores": false,
    "HealthcareAndChildcareServices": false,
    "ProfessionalServices": false,
    "Restaurants": false,
    "RetailStores": false,
    "TravelAndTransportation": false,
    "FuelPumpOnly": false,
    "HardwareStores": false
  },
  "InternationalSpendEnabled": false,
  "DailySpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

<h3 id="create-spend-rules-for-a-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SetSpendRulesRequest](#schemasetspendrulesrequest)|true|Spend rule data|

> Example responses

> 200 Response

```json
{}
```

<h3 id="create-spend-rules-for-a-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
  <item>
    <description>- Account closed</description>
  </item>
</list>|None|

<h3 id="create-spend-rules-for-a-specified-card-accountid-responseschema">Response Schema</h3>

Status Code **200**

*HttpResponseMessage*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Return scheduled funding rules for a specified card accountID

<a id="opIdCard_ScheduledFundingRulesByIdAuthorizationGETCard/ScheduledFundingRules/{id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Card/ScheduledFundingRules/{id}`

Return scheduled funding rules for a specified card accountID.<br/>
<br/>
If no funding rule is set, PEX system will return a null response.<br/>
<br/>
To retrieve the card accountID, use GET /Details/AccountDetails.

<h3 id="return-scheduled-funding-rules-for-a-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": ""
  }
}
```

<h3 id="return-scheduled-funding-rules-for-a-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[GetScheduledFundingRulesResponse](#schemagetscheduledfundingrulesresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a scheduled funding rule for the specified card accountID

<a id="opIdCard_ScheduledFundingRulesByidUserRequestAuthorizationPUTCard/ScheduledFundingRules/{id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Amount": 0,
  "Frequency": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/ScheduledFundingRules/{id}`

Create a scheduled funding rule for the specified card accountID.<br/>
<br/>
Example of a scheduled funding rule logic: I would like this card balance to equal $500.00 every Monday.<br/>
<br/>
You may have cardholders who should have a set balance every day or once a week. For those employees, set a funding rule on the card.<br/>
The scheduled rule is time based. At midnight ET, the system checks to see if the card balance should be changed. If the balance is below the threshold, the system will add funds to equal the amount specified in the rule.<br/>
<br/>
To change the existing rule, post new values in the input fields.<br/>
<br/>
To retrieve the card accountID, use GET /Details/AccountDetails.

> Body parameter

```json
{
  "Amount": 0,
  "Frequency": ""
}
```

<h3 id="create-a-scheduled-funding-rule-for-the-specified-card-accountid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SetScheduledFundingRulesRequest](#schemasetscheduledfundingrulesrequest)|true|Rule parameters|

> Example responses

> 200 Response

```json
{}
```

<h3 id="create-a-scheduled-funding-rule-for-the-specified-card-accountid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID<br /></description>
  </item>
  <item>
    <description>- Invalid amount</description>
  </item>
</list>|None|

<h3 id="create-a-scheduled-funding-rule-for-the-specified-card-accountid-responseschema">Response Schema</h3>

Status Code **200**

*HttpResponseMessage*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a funding rule for the card account

<a id="opIdCard_ScheduledFundingRulesByidAuthorizationDELETECard/ScheduledFundingRules/{id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{id} HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript

const headers = {
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Card/ScheduledFundingRules/{id}`

Once the rule is deleted, the system will no longer add funds to the card balance.<br/>
<br/>
To file the card account ID, call GET /Details/AccountDetails.<br/>

<h3 id="delete-a-funding-rule-for-the-card-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

<h3 id="delete-a-funding-rule-for-the-card-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Set a spending ruleset for the card account

<a id="opIdCard_SetSpendingRulesetByrulesetRequestAuthorizationPUTCard/SetSpendingRuleset"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Card/SetSpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "RulesetId": 0,
  "AccountId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Card/SetSpendingRuleset',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Card/SetSpendingRuleset`

What it does:<br/>
Assign a card account ID to an existing spending ruleset.<br/>
To remove the card from a ruleset and leave them unassigned, use a zero (0) in the SpendingRulesetId field.<br/>

> Body parameter

```json
{
  "RulesetId": 0,
  "AccountId": 0
}
```

<h3 id="set-a-spending-ruleset-for-the-card-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SetCardholderRulesetRequest](#schemasetcardholderrulesetrequest)|true|Ruleset ID and Account ID|

> Example responses

> 200 Response

```json
{
  "AccountId": 0
}
```

<h3 id="set-a-spending-ruleset-for-the-card-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[CardholderSpendRulesetResponse](#schemacardholderspendrulesetresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Invalid ruleset ID<br /></description>
  </item>
  <item>
    <description>- Account closed</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-details-deep-dive-into-your-business-card-accounts-and-transactions-">Details : 
            Deep-dive into your business, card accounts, and transactions.
            </h1>

## Ping the PEX server

<a id="opIdDetails_PingByGETDetails/Ping"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/Ping HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json

```

```javascript

const headers = {
  'Accept':'application/json'
};

fetch('https://coreapi.pexcard.com/v4/Details/Ping',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/Ping`

Verify connection to the PEX system with a ping test.

> Example responses

> 200 Response

```json
"2019-08-24T14:15:22Z"
```

<h3 id="ping-the-pex-server-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|string|

<aside class="success">
This operation does not require authentication
</aside>

## Return all data associated with a single card account

<a id="opIdDetails_AccountDetailsByIdAuthorizationGETDetails/AccountDetails/{Id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/AccountDetails/{Id}`

Return all data associated with a single card account.<br/>
<br/>
Definition of some of the returned fields and how the PEX system uses them:<br/>
<list type="number">
<item><description>- Group: An administrator defined category that can be used for sorting and reporting.<br/> </description></item>
<item><description>- Account Status: Either open or closed. A closed account cannot be reopened.<br/></description></item>
<item><description>- Ledger balance: The total funds allocated to the card.<br/></description></item>
<item><description>- Available balance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
<item><description>- Profile address: The cardholder’S billing address. This address may be validated by merchants in a card not present transaction (online and phone) or at a fuel pump. It is important that your cardholders know what their billing address is.<br/></description></item>
<item><description>- Shipping address:  used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/></description></item>
<item><description>- Card list: Contains all card numbers that have been issued to this account.<br/></description></item>
<item><description>- Spend rules: Controls where and how much a card can be used. You can set limitations on international spending, merchant categories (MCCs) and the dollar amount spent per day. A definition of spend rules can be found under GET /Card/SpendRules/{Id}.<br/></description></item>
<item><description>- Funding rules allow you to systematically add funds to a card balance.<br/></description></item>
<item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
<item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/></description></item>
</list>

<h3 id="return-all-data-associated-with-a-single-card-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "AccountStatus": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CardList": [
    {
      "CardId": 0,
      "IssuedDate": "",
      "ExpirationDate": "",
      "Last4CardNumber": "",
      "CardStatus": ""
    }
  ],
  "SpendingRulesetId": 0,
  "SpendRules": {
    "UseMerchantCategory": false,
    "MerchantCategories": {
      "AssociationsAndOrganizations": false,
      "AutomotiveDealers": false,
      "EducationalServices": false,
      "Entertainment": false,
      "FuelAndConvenienceStores": false,
      "GroceryStores": false,
      "HealthcareAndChildcareServices": false,
      "ProfessionalServices": false,
      "Restaurants": false,
      "RetailStores": false,
      "TravelAndTransportation": false,
      "FuelPumpOnly": false,
      "HardwareStores": false
    },
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  },
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": ""
  },
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  },
  "CustomId": ""
}
```

<h3 id="return-all-data-associated-with-a-single-card-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[CardholderDetailsResponse](#schemacardholderdetailsresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return remaining limits allowed by spend rules placed on a single card account

<a id="opIdDetails_RemainingLimitsAccountDetailsByIdAuthorizationGETDetails/AccountDetails/{Id}/RemainingLimits"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/RemainingLimits HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/RemainingLimits',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/AccountDetails/{Id}/RemainingLimits`

Return remaining limits allowed by spend rules placed on a single card account.<br/>
<br/>
Definition of some of the returned fields and how the PEX system uses them:<br/>
<list type="number">
<item><description>- GlobalLimits: A collection of spending limits placed upon all categories of purchases.<br/> </description></item>
<item><description>- MerchantCategoryLimits: A collection of spending limits placed upon purchases which fall under a predefined merchant category.<br/></description></item>
</list>

<h3 id="return-remaining-limits-allowed-by-spend-rules-placed-on-a-single-card-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Card account ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "GlobalLimits": [
    {
      "Type": "",
      "EnforcedLimit": 0,
      "RemainingSpend": 0
    }
  ],
  "MerchantCategoryLimits": [
    {
      "MerchantCategoryId": 0,
      "Category": "",
      "Type": "",
      "EnforcedLimit": 0,
      "RemainingSpend": 0
    }
  ]
}
```

<h3 id="return-remaining-limits-allowed-by-spend-rules-placed-on-a-single-card-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[AccountRemainingLimitsResponse](#schemaaccountremaininglimitsresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid card account ID<br /></description>
  </item>
  <item>
    <description>- Must be card account ID</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Returns all network transaction for specified card account ID. Examples: Authorization, Settlement, Reversal, PIN transaction, Decline.

<a id="opIdDetails_NetworkTransactionsByIdStartDateEndDateAuthorizationGETDetails/{Id}/NetworkTransactions?StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/{Id}/NetworkTransactions`

This call is only for network transactions. Card funding transactions are not included. In case you miss webhook call  for any reason, you can use this endpoint to retrieve same information.<br/>
<br/>
Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
Return a list of network transaction details, within a specified start and end date, for the given card account ID.<br/>
<br/>
Definition of some of the network transaction detail fields:<br/>
<list type="number">
<item><description>- NetworkTransactionId: Unique Id for all the related network transactions (e.g. chain of authorization, settlement, etc).<br/></description></item>
<item><description>- TransactionId: Unique Id for transaction.<br/></description></item>
<item><description>- AcctId: Unique Id for cardholder account Id.<br/></description></item>
<item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
<item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
<item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
<item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
<item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
<item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
<item><description>- PaddingAmount: Added to restaurant (20%) and fuel ($49.00) purchases.<br/></description></item>
<item><description>- AvailableBalance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
<item><description>- LedgerBalance: The total funds allocated to the card.<br/></description></item>
<item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
<item><description>- Description: More information about the transaction.<br/></description></item>
<item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
<item><description>- ReferencedTranId: Unique Id which refers back to network transaction that precedes to the current one (e.g. ReferenceTranId on Settlement transaction refers to id on predecessor network transaction i.e. Authorization transaction).<br/></description></item>
<item><description>- ReferencedTransactionTime: The date/time when referenced transaction was received from the Network. Eastern Standard time.<br/></description></item>
<item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantCity: The merchant city provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantState: The merchant state provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantZip: The merchant address zip code provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantCountry: The merchant country provided in the Visa transaction.<br/></description></item>
<item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
<item><description>- AuthIdentityResponseCode: Authorization Identification Response code from Star data element 38 in Auth Response message.<br/></description></item>
<item><description>- MerchantId: Unique Id for merchant provided in Visa transaction.<br/></description></item>
<item><description>- TerminalId: Unique Id for POS terminal.<br/></description></item>
<item><description>- NetworkType: Specify the type of event.<br/></description></item>
<item><description>- NetworkStatus: Specify the status of the network event, Approved/Declined.<br/></description></item>
<item><description>- IsCardPresent: Boolean parameter, indicates if card was actually physically swiped at POS or used other way e.g over internet or phone etc.<br/></description></item>
<item><description>- Message: In case of declined transaction, Transaction Decline reason can be found here.<br/></description></item>
<item><description>- MessageCode: Codes for decline reason.<br/></description></item>
<item><description>- MerchantRequestedAmount: The amount which merchant requests at the POS to complete the transaction.<br/></description></item>
</list>
<br/>
Details about why a transaction was declined is provided in the "Message" field.<br/>
You can find list of message codes and corresponding messages <a href="https://developer.pexcard.com/documentation/web-hooks/message-codes" target="_blank">here</a>

<h3 id="returns-all-network-transaction-for-specified-card-account-id.-examples:-authorization,-settlement,-reversal,-pin-transaction,-decline.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Unique Id for cardholder account Id|
|StartDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|EndDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "NetworkTransactionId": 0,
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "MerchantLocalTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "AvailableBalance": 0,
      "LedgerBalance": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "ReferencedTranId": 0,
      "ReferencedTransactionTime": "",
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkType": "",
      "NetworkStatus": "",
      "IsCardPresent": false,
      "Message": "",
      "MessageCode": "",
      "MerchantRequestedAmount": 0
    }
  ]
}
```

<h3 id="returns-all-network-transaction-for-specified-card-account-id.-examples:-authorization,-settlement,-reversal,-pin-transaction,-decline.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[NetworkTransactionDetailsResponse](#schemanetworktransactiondetailsresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Invalid card account ID|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return version of the API

<a id="opIdDetails_VersionByGETDetails/Version"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/Version HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json

```

```javascript

const headers = {
  'Accept':'application/json'
};

fetch('https://coreapi.pexcard.com/v4/Details/Version',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/Version`

Return version of the API.

> Example responses

> 200 Response

```json
"string"
```

<h3 id="return-version-of-the-api-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|string|

<aside class="success">
This operation does not require authentication
</aside>

## Return all accounts associated with your business

<a id="opIdDetails_AccountDetailsByAuthorizationGETDetails/AccountDetails"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/AccountDetails HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/AccountDetails',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/AccountDetails`

Return all accounts associated with your business, including registered external business checking accounts and all PEX business accounts.<br/>
<br/>
Reasons you will use this call:<br/>
<list type="number">
<item><description>- One-time transfer: To retrieve or create a one-time transfer requires an ‘ExternalBankAcctId’<br/></description></item>
<item><description>- Business: Use field  ‘BusinessAccountBalance’ to monitor the available balance in your PEX business account for fund disbursement. You must have a minimum of $50.00 in your PEX Card business account at all times. The system will not allow you to allocate the last $50.00 to cards.<br/></description></item>
<item><description>- Cards: To edit, fund, delete or create funding and spend rules, you will need the AccountID for the card. Also, this call will give you the available balance and status on all card accounts.<br/></description></item>
<item><description>- Groups: To find the group name associated with each unique GroupID.<br/></description></item>
<item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
<item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/></description></item>
</list>

<h3 id="return-all-accounts-associated-with-your-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "BusinessAccountId": 0,
  "BusinessName": "",
  "BusinessAccountStatus": "",
  "BusinessAccountBalance": 0,
  "PendingTransferAmount": 0,
  "BankAccountList": [
    {
      "ExternalBankAcctId": 0,
      "RoutingNumber": "",
      "BankAccountNumber": "",
      "BankName": "",
      "BankAccountType": "",
      "IsActive": false
    }
  ],
  "CHAccountList": [
    {
      "AccountId": 0,
      "FirstName": "",
      "LastName": "",
      "LedgerBalance": 0,
      "AvailableBalance": 0,
      "AccountStatus": "",
      "IsVirtual": false,
      "CustomId": ""
    }
  ],
  "CardholderGroups": [
    {
      "Id": 0,
      "Name": ""
    }
  ]
}
```

<h3 id="return-all-accounts-associated-with-your-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[BusinessDetailsResponse](#schemabusinessdetailsresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return a list of transaction details for the account

<a id="opIdDetails_TransactionDetailsByIdIncludePendingsIncludeDeclinesStartDateEndDateAuthorizationGETDetails/TransactionDetails/{Id}?IncludePendings={IncludePendings}&IncludeDeclines={IncludeDeclines}&StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/TransactionDetails/{Id}`

Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
Return a list of transaction details for PEX business account ID or card account ID provided.<br/>
<br/>
If a business account ID is provided, the transactions returned will be for the PEX business account. (Note: input fields ‘IsPending’ and ‘IsDecline’ should be false, as they don't apply to transactions on the business account.)<br/>
<br/>
If a card account ID is provided (and you are a partner), the transactions returned will be for that card account. Fields ‘IsPending’ and ‘IsDecline’ can be set to true or false as required.<br/>
<br/>
If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the ‘LastTimeRetrieved’ field returned in the StartDate parameter and repeat the call until the ‘NumberOfPages’ field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
<br/>
Definition of some of the transaction detail fields:<br/>
<list type="number">
<item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
<item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
<item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
<item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
<item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
<item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
<item><description>- PaddingAmount: Added to fuel purchases ($49.00).<br/></description></item>
<item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
<item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
<item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
<item><description>- IsDecline: The authorization was not successful.<br/></description></item>
<item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
<item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
<item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
<item><description>- PageSize: Total page size, 30,000.<br/></description></item>
<item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
<item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
<item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
<item><description>- TransactionTags: Transaction tags.<br/></description></item>
<item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
<item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
<item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
<item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
<item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
</list>
<br/>
Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
<list type="number">
<item><description>- Transaction exceeded current card balance<br/></description></item>
<item><description>- Transaction exceeded daily spend limit<br/></description></item>
<item><description>- International transactions not allowed<br/></description></item>
<item><description>- Expired card<br/></description></item>
<item><description>- Address does not match<br/></description></item>
<item><description>- Unauthorized merchant<br/></description></item>
<item><description>- Card not present<br/></description></item>
<item><description>- Unauthorized geographic location<br/></description></item>
<item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
<item><description>- Insufficient balance in PEX Account<br/></description></item>
<item><description>- Remote service decline<br/></description></item>
<item><description>- Do not honor<br/></description></item>
</list>

<h3 id="return-a-list-of-transaction-details-for-the-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Card account ID or Business account ID|
|IncludePendings|query|boolean|false|1 to include pending transactions and 0 to exclude|
|IncludeDeclines|query|boolean|false|1 to include decline transactions and 0 to exclude|
|StartDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|EndDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": "",
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```

<h3 id="return-a-list-of-transaction-details-for-the-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[TransactionDetailsResponse](#schematransactiondetailsresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Invalid card account ID|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return a list of transaction details for the authenticated user

<a id="opIdDetails_TransactionDetailsByIncludePendingsIncludeDeclinesStartDateEndDateAuthorizationGETDetails/TransactionDetails?IncludePendings={IncludePendings}&IncludeDeclines={IncludeDeclines}&StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/TransactionDetails?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/TransactionDetails?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/TransactionDetails`

Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
Return a list of transaction details, within a specified start and end date, for the authenticated user.<br/>
<br/>
If the token user is a PEX administrator, the transactions returned will be for the PEX business account. (Note: input fields ‘IsPending’ and ‘IsDecline’ should be false, as they don't apply to transactions on the business account.)<br/>
<br/>
If the token user is a cardholder (and you are a partner), the transactions returned will be for that card account. Fields ‘IsPending’ and ‘IsDecline’ can be set to true or false as required.<br/>
<br/>
If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the ‘LastTimeRetrieved’ field returned in the StartDate parameter and repeat the call until the ‘NumberOfPages’ field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
<br/>
Definition of some of the transaction detail fields:<br/>
<list type="number">
<item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
<item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
<item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
<item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
<item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
<item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
<item><description>- PaddingAmount: Added to restaurant (20&#37;) and fuel ($49.00) purchases.<br/></description></item>
<item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
<item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
<item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
<item><description>- IsDecline: The authorization was not successful.<br/></description></item>
<item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
<item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
<item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
<item><description>- PageSize: Total page size, 30,000.<br/></description></item>
<item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
<item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
<item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
<item><description>- TransactionTags: Transaction tags.<br/></description></item>
<item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
<item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
<item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
<item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
<item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
</list>
<br/>
Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
<list type="number">
<item><description>- Transaction exceeded current card balance<br/></description></item>
<item><description>- Transaction exceeded daily spend limit<br/></description></item>
<item><description>- International transactions not allowed<br/></description></item>
<item><description>- Expired card<br/></description></item>
<item><description>- Address does not match<br/></description></item>
<item><description>- Unauthorized merchant<br/></description></item>
<item><description>- Card not present<br/></description></item>
<item><description>- Unauthorized geographic location<br/></description></item>
<item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
<item><description>- Insufficient balance in PEX Account<br/></description></item>
<item><description>- Remote service decline<br/></description></item>
<item><description>- Do not honor<br/></description></item>
</list>

<h3 id="return-a-list-of-transaction-details-for-the-authenticated-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|IncludePendings|query|boolean|false|1 to include pending transactions and 0 to exclude|
|IncludeDeclines|query|boolean|false|1 to include decline transactions and 0 to exclude|
|StartDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|EndDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": "",
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```

<h3 id="return-a-list-of-transaction-details-for-the-authenticated-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[TransactionDetailsResponse](#schematransactiondetailsresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Returns all network transaction. Examples: Authorization, Settlement, Reversal, PIN transaction, Decline.

<a id="opIdDetails_NetworkTransactionsByStartDateEndDateAuthorizationGETDetails/NetworkTransactions?StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/NetworkTransactions?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/NetworkTransactions?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/NetworkTransactions`

This call is only for network transactions. Card funding transactions are not included. In case you miss webhook call  for any reason, you can use this endpoint to retrieve same information.<br/>
<br/>
Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
Return a list of transaction details, within a specified start and end date, for the authenticated user.<br/>
<br/>
Definition of some of the network transaction detail fields:<br/>
<list type="number">
<item><description>- NetworkTransactionId: Unique Id for all the related network transactions (e.g. chain of authorization, settlement, etc).<br/></description></item>
<item><description>- TransactionId: Unique Id for transaction.<br/></description></item>
<item><description>- AcctId: Unique Id for cardholder account Id.<br/></description></item>
<item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
<item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
<item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
<item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
<item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
<item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
<item><description>- PaddingAmount: Added to restaurant (20%) and fuel ($49.00) purchases.<br/></description></item>
<item><description>- AvailableBalance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
<item><description>- LedgerBalance: The total funds allocated to the card.<br/></description></item>
<item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
<item><description>- Description: More information about the transaction.<br/></description></item>
<item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
<item><description>- ReferencedTranId: Unique Id which refers back to network transaction that precedes to the current one (e.g. ReferenceTranId on Settlement transaction refers to id on predecessor network transaction i.e. Authorization transaction).<br/></description></item>
<item><description>- ReferencedTransactionTime: The date/time when referenced transaction was received from the Network. Eastern Standard time.<br/></description></item>
<item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantCity: The merchant city provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantState: The merchant state provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantZip: The merchant address zip code provided in the Visa transaction.<br/></description></item>
<item><description>- MerchantCountry: The merchant country provided in the Visa transaction.<br/></description></item>
<item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
<item><description>- AuthIdentityResponseCode: Authorization Identification Response code from Star data element 38 in Auth Response message.<br/></description></item>
<item><description>- MerchantId: Unique Id for merchant provided in Visa transaction.<br/></description></item>
<item><description>- TerminalId: Unique Id for POS terminal.<br/></description></item>
<item><description>- NetworkType: Specify the type of event.<br/></description></item>
<item><description>- NetworkStatus: Specify the status of the network event, Approved/Declined.<br/></description></item>
<item><description>- IsCardPresent: Boolean parameter, indicates if card was actually physically swiped at POS or used other way e.g over internet or phone etc.<br/></description></item>
<item><description>- Message: In case of declined transaction, Transaction Decline reason can be found here.<br/></description></item>
<item><description>- MessageCode: Codes for decline reason.<br/></description></item>
<item><description>- MerchantRequestedAmount: The amount which merchant requests at the POS to complete the transaction.<br/></description></item>
</list>
<br/>
Details about why a transaction was declined is provided in the "Message" field.<br/>
You can find list of message codes and corresponding messages <a href="https://developer.pexcard.com/documentation/web-hooks/message-codes" target="_blank">here</a>

<h3 id="returns-all-network-transaction.-examples:-authorization,-settlement,-reversal,-pin-transaction,-decline.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|StartDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|EndDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "NetworkTransactionId": 0,
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "MerchantLocalTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "AvailableBalance": 0,
      "LedgerBalance": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "ReferencedTranId": 0,
      "ReferencedTransactionTime": "",
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkType": "",
      "NetworkStatus": "",
      "IsCardPresent": false,
      "Message": "",
      "MessageCode": "",
      "MerchantRequestedAmount": 0
    }
  ]
}
```

<h3 id="returns-all-network-transaction.-examples:-authorization,-settlement,-reversal,-pin-transaction,-decline.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[NetworkTransactionDetailsResponse](#schemanetworktransactiondetailsresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return a list of all card transactions for the business

<a id="opIdDetails_AllCardholderTransactionsByIncludePendingsIncludeDeclinesStartDateEndDateAuthorizationGETDetails/AllCardholderTransactions?IncludePendings={IncludePendings}&IncludeDeclines={IncludeDeclines}&StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/AllCardholderTransactions`

Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
Return a list of transaction details, within a specified start and end date, for all card accounts associated with the business of the authenticated user. Fields ‘IsPending’ and ‘IsDecline’ can be set to true or false as required.<br/>
<br/>
If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the ‘LastTimeRetrieved’ field returned in the StartDate parameter and repeat the call until the ‘NumberOfPages’ field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
<br/>
Definition of some of the transaction detail fields:<br/>
<list type="number">
<item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
<item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
<item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
<item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
<item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
<item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
<item><description>- PaddingAmount: Added to fuel purchases ($49.00).<br/></description></item>
<item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
<item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
<item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
<item><description>- IsDecline: The authorization was not successful.<br/></description></item>
<item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
<item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
<item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
<item><description>- PageSize: Total page size, 30,000.<br/></description></item>
<item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
<item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
<item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
<item><description>- TransactionTags: Transaction tags.<br/></description></item>
<item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
<item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
<item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
<item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
<item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
</list>
<br/>
Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
<list type="number">
<item><description>- Transaction exceeded current card balance<br/></description></item>
<item><description>- Transaction exceeded daily spend limit<br/></description></item>
<item><description>- International transactions not allowed<br/></description></item>
<item><description>- Expired card<br/></description></item>
<item><description>- Address does not match<br/></description></item>
<item><description>- Unauthorized merchant<br/></description></item>
<item><description>- Card not present<br/></description></item>
<item><description>- Unauthorized geographic location<br/></description></item>
<item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
<item><description>- Insufficient balance in PEX Account<br/></description></item>
<item><description>- Remote service decline<br/></description></item>
<item><description>- Do not honor<br/></description></item>
</list>

<h3 id="return-a-list-of-all-card-transactions-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|IncludePendings|query|boolean|false|1 to include pending transactions and 0 to exclude|
|IncludeDeclines|query|boolean|false|1 to include decline transactions and 0 to exclude|
|StartDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|EndDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": "",
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```

<h3 id="return-a-list-of-all-card-transactions-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[TransactionDetailsResponse](#schematransactiondetailsresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return a count of transactions for the authenticated user

<a id="opIdDetails_AllCardholderTransactionCountByIncludePendingsIncludeDeclinesStartDateEndDateAuthorizationGETDetails/AllCardholderTransactionCount?IncludePendings={IncludePendings}&IncludeDeclines={IncludeDeclines}&StartDate={StartDate}&EndDate={EndDate}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount?StartDate=2019-08-24T14%3A15%3A22Z&EndDate=2019-08-24T14%3A15%3A22Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Details/AllCardholderTransactionCount`

Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
<br/>
Return a count of transactions, within a specified start and end date, for all card accounts associated with the business of the authenticated user. Fields ‘IsPending’ and ‘IsDecline’ can be set to true or false as required.

<h3 id="return-a-count-of-transactions-for-the-authenticated-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|IncludePendings|query|boolean|false|1 to include pending transactions and 0 to exclude|
|IncludeDeclines|query|boolean|false|1 to include decline transactions and 0 to exclude|
|StartDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|EndDate|query|string(date-time)|true|YYYY-MM-DDThh:mm:ss|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
0
```

<h3 id="return-a-count-of-transactions-for-the-authenticated-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|integer|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-transactions-attach-receipts-and-tags-to-transactions-">Transactions : 
            Attach receipts and tags to transactions.
            </h1>

## Retrieve the attachment for a transaction.

<a id="opIdTransactions_AttachmentsByIdAuthorizationGETTransactions/{id}/Attachments"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Transactions/{id}/Attachments HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{id}/Attachments',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Transactions/{id}/Attachments`

Read the attachments for a particular transaction:
<list type="number">
<item><description>- Attachment Id - unique identifier of the attachment.</item>
<item><description>- Type - specifies the type of attachment Image/PDF.</item>
<item><description>- Size - size of the attachment.</item>
<item><description>- Link - provides a link to /AttachmentId resource which contains the encoded image details. 
<item><description>- UploadStatus - the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.</item>
<item><description>- Approval Status - approval status is on the transaction level and not only for attachment. If the transaction is approved, all related data i.e Attachments, Tags etc are approved.</item>
</list>

<h3 id="retrieve-the-attachment-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Attachments": [
    {
      "AttachmentId": "",
      "Type": "",
      "Size": 0,
      "Link": {
        "related": ""
      },
      "UploadStatus": "",
      "CreatedDateUtc": "",
      "CreatedBy": {
        "AdminId": 0,
        "UserId": 0
      },
      "UpdatedDateUtc": "",
      "UpdatedBy": {
        "AdminId": 0,
        "UserId": 0
      }
    }
  ],
  "ApprovalStatus": ""
}
```

<h3 id="retrieve-the-attachment-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetAttachments](#schemagetattachments)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete attachment, attached to a transaction.

<a id="opIdTransactions_DeleteAttachmentsByidAuthorizationDELETETransactions/{id}/Attachments"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Transactions/{id}/Attachments HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{id}/Attachments',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Transactions/{id}/Attachments`

This endpoint can be used to delete the attachment attached to a transaction. All the attachments attached to the transaction will be deleted.
<list type="number">
<item><description>- Attachment Id - unique identifier of the attachment.</item>
<item><description>- Type - specifies the type of attachment Image/PDF.</item>
<item><description>- Size - size of the attachment.</item>
<item><description>- UploadStatus - the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.</item>
</list>

<h3 id="delete-attachment,-attached-to-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="delete-attachment,-attached-to-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DeleteAttachment](#schemadeleteattachment)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## An attachment can be read by providing specific attachment id along with the transaction Id.

<a id="opIdTransactions_AttachmentByIdAttachmentIdAuthorizationGETTransactions/{id}/Attachment/{attachmentId}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment/{attachmentId} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment/{attachmentId}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Transactions/{id}/Attachment/{attachmentId}`

<list type="number">
<item><description>- Attachment Id - unique identifier of the attachment.</item>
<item><description>- Type - specifies the type of attachment Image/PDF.</item>
<item><description>- Size - size of the attachment.</item>
<item><description>- Content - base 64 encoded data of the attachment.
<item><description>- UploadStatus - the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.</item>
</list>

<h3 id="an-attachment-can-be-read-by-providing-specific-attachment-id-along-with-the-transaction-id.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Transaction Id|
|AttachmentId|path|string|true|Attachment Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "Content": "",
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "ApprovalStatus": ""
}
```

<h3 id="an-attachment-can-be-read-by-providing-specific-attachment-id-along-with-the-transaction-id.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Attachment](#schemaattachment)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update an existing attachment of a transaction.

<a id="opIdTransactions_PutAttachmentByidattachmentIdattachmentRequestAuthorizationPUTTransactions/{id}/Attachment/{attachmentId}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment/{attachmentId} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Content": "",
  "Type": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment/{attachmentId}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Transactions/{id}/Attachment/{attachmentId}`

Use this endpoint to Update the already attached attachment to a transaction.
Attachment can be specified in the form of base 64 encoded data to be attached to the specified PEX transaction. 
https://www.base64encode.org/ can be used for encoding the image files. This encoded image format can be used in the request property 'Content'. 
All the attachments will be scanned for malware threats.
<list type="number">
<item><description>- Attachment Id - unique identifier of the attachment.</item>
<item><description>- Type - specifies the type of attachment Image/PDF.</item>
<item><description>- Size - size of the attachment.</item>
<item><description>- Link - provides a link to /AttachmentId resource which contains the encoded image details. 
<item><description>- UploadStatus - the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.</item>
<item><description>- Approval Status - approval status is on the transaction level and not only for attachment. If the transaction is approved, all related data i.e Attachments, Tags etc are approved.</item>
</list>

> Body parameter

```json
{
  "Content": "",
  "Type": ""
}
```

<h3 id="update-an-existing-attachment-of-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Transaction Id|
|attachmentId|path|string|true|Attachment Id|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateOrUpdateAttachmentRequest](#schemacreateorupdateattachmentrequest)|true|Attachment request|

> Example responses

> 200 Response

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "Link": {
    "self": ""
  },
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="update-an-existing-attachment-of-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[AttachmentWithSelfLink](#schemaattachmentwithselflink)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|BadRequest|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a specific attachment, attached to a transaction.

<a id="opIdTransactions_DeleteAttachmentByidattachmentIdAuthorizationDELETETransactions/{id}/Attachment/{attachmentId}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment/{attachmentId} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment/{attachmentId}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Transactions/{id}/Attachment/{attachmentId}`

You can delete a specific attachment by specifying transaction id and attachment Id.

<h3 id="delete-a-specific-attachment,-attached-to-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Transaction Id|
|attachmentId|path|string|true|Attachment Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="delete-a-specific-attachment,-attached-to-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DeleteAttachment](#schemadeleteattachment)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Attach an attachment to a transaction

<a id="opIdTransactions_PostAttachmentByidattachmentRequestAuthorizationPOSTTransactions/{id}/Attachment"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Content": "",
  "Type": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{id}/Attachment',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Transactions/{id}/Attachment`

Attachments can be specified in the form of base 64 encoded data to be attached to the specified PEX transaction. 
https://www.base64encode.org/ can be used for encoding the image files. This encoded image format can be used in the request property 'Content'. 
All the attachments will be scanned for malware threats.
<list type="number">
<item><description>- Attachment Id - unique identifier of the attachment.</item>
<item><description>- Type - specifies the type of attachment Image/PDF.</item>
<item><description>- Size - size of the attachment.</item>
<item><description>- Link - provides a link to /AttachmentId resource which contains the encoded image details. 
<item><description>- UploadStatus - the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.</item>
<item><description>- Approval Status: - approval status is on the transaction level and not only for attachment. If the transaction is approved, all related data i.e Attachments, Tags etc are approved.</item>
</list>

> Body parameter

```json
{
  "Content": "",
  "Type": ""
}
```

<h3 id="attach-an-attachment-to-a-transaction-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateOrUpdateAttachmentRequest](#schemacreateorupdateattachmentrequest)|true|Attachment request|

> Example responses

> 200 Response

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "Link": {
    "self": ""
  },
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="attach-an-attachment-to-a-transaction-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[AttachmentWithSelfLink](#schemaattachmentwithselflink)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|BadRequest|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return tag values for a transaction.

<a id="opIdTransactions_GetTagsByIdAuthorizationGETTransactions/{Id}/Tags"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Transactions/{Id}/Tags`

Return tag values and associated tag definitions for a transaction.  Use to also return _allocation_ tag values.
<list type="number">
<item><description>- Id - Unique identifier for tag values for a transaction.</description></item>
<item><description>- ConcurrencyKey - Most recent value, used to prevent conflicts when multiple users update tag values at the same time.</description></item>
<item><description>- State - Transaction review state. Possible values are: NotReviewed (default), Approved, Reject, Ignore.</description></item>
<item><description>- Values - List of tag values.</item>
</list>

<h3 id="return-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="return-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tags](#schematags)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update tag values for a transaction.

<a id="opIdTransactions_PutTagValuesByIdrequestAuthorizationPUTTransactions/{Id}/Tags"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Value": {}
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Transactions/{Id}/Tags`

 Use this endpoint to update existing tag values associated with a transaction.

 To view a list of tag definitions configured for your business, use `GET /Business/Configuration/Tags`.

 To change a tag definition, use `PUT /Business/Configuration/Tag/{tag-type}`.

 Tag values are passed as arrays of TagId and Value property pairs.
 ```
 {
     "ConcurrencyKey": "string",
     "Values": [{
         "TagId" : string,
         "Value" : object
     }]
 }
```
 #### Value Object Examples ####
 Text Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : "Some new text"
 }]
 ```
 Dropdown Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : "Engineering"
 }]
 ```
 Decimal Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : 10.15
 }]
 ```
 Yes/No Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : true
 }]
 ```
 <list type="number">
 <item><description>- Id - Unique identifier for tag values for a transaction.</description></item>
 <item><description>- ConcurrencyKey - Most recent value, used to prevent conflicts when multiple users update tag values at the same time.</description></item>
 <item><description>- State - Transaction review state. Possible values are: NotReviewed(default value), Approved, Reject, Ignore.</description></item>
 <item><description>- Values - List of tag values.</item>
 </list>

> Body parameter

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Value": {}
    }
  ]
}
```

<h3 id="update-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateTagValuesRequest](#schemaupdatetagvaluesrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="update-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tags](#schematags)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Please update your outdated ConcurrencyKey value.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create tag values for a transaction.

<a id="opIdTransactions_PostTagValuesByIdrequestAuthorizationPOSTTransactions/{Id}/Tags"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Value": {}
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Transactions/{Id}/Tags`

 Create tag values for a transaction using predefined tag definitions. 
 
 To view a list of tag definitions configured for your business, use `GET /Business/Configuration/Tags`.

 To create a tag definition, use `POST /Business/Configuration/Tag/{tag-type}`.

 Tag values are passed as arrays of TagId and Value property pairs.
 ```
 {
     "ConcurrencyKey": "string",
     "Values": [{
         "TagId" : string,
         "Value" : object
     }]
 }
```
 #### Value Object Examples ####
 Text Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : "Some new text"
 }]
 ```
 Dropdown Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : "Engineering"
 }]
 ```
 Decimal Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : 10.15
 }]
 ```
 Yes/No Value
 ```
 "Values": [{
     "TagId" : "5dbaed52f7c5d7997ce43e0b",
     "Value" : true
 }]
 ```
 <list type="number">
 <item><description>- Id - Unique identifier for tag values for a transaction.</description></item>
 <item><description>- ConcurrencyKey - Most recent value, used to prevent conflicts when multiple users update tag values at the same time.</description></item>
 <item><description>- State - Transaction review state. Possible values are: NotReviewed(default value), Approved, Reject, Ignore.</description></item>
 <item><description>- Values - List of tag values.</item>
 </list>

> Body parameter

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Value": {}
    }
  ]
}
```

<h3 id="create-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateTagValuesRequest](#schemacreatetagvaluesrequest)|true|CreateTagValuesRequest object|

> Example responses

> 201 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="create-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[Tags](#schematags)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|The request is invalid because the item already exists.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|url||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Delete all tag values for a transaction.

<a id="opIdTransactions_DeleteTagValuesByIdConcurrencyKeyAuthorizationDELETETransactions/{Id}/Tags?ConcurrencyKey={ConcurrencyKey}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags?ConcurrencyKey=string HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags?ConcurrencyKey=string',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Transactions/{Id}/Tags`

Use this endpoint to delete all standards tag values for a transaction.  This call does not delete allocation tag values.
### Response ###
<list type="number">
<item><description>- Id - Unique identifier for tag values.</item>
<item><description>- ConcurrencyKey - Most recently updated concurrency key.</description></item>
<item><description>- State - Transaction review state. Possible values are: NotReviewed (default), Approved, Reject, Ignore.</description></item>
</list>

<h3 id="delete-all-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|Transaction Id|
|ConcurrencyKey|query|string|true|Concurrency Key|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="delete-all-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tags](#schematags)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update Allocation tag values for a transaction.

<a id="opIdTransactions_PutAllocationTagValuesByIdrequestAuthorizationPUTTransactions/{Id}/Tags/Allocations"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags/Allocations HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Allocation": [
        {
          "TagId": "",
          "Value": {}
        }
      ],
      "Amount": 0
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags/Allocations',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Transactions/{Id}/Tags/Allocations`

 Allocations allow you to associate a transaction with multiple expense categories or accounts. 
 
 ### Request ###
 Settled PEX transactions may be divided into multiple allocation sets.  Each set references one or more tag values and an allocation amount.

 The sum total of all allocation amounts must be equal to the transaction settlement amount.

 A transaction with allocations is required to contain a minimum of two sets of Allocation tag values.  Otherwise, for a single allocation use standard tag values.
 ```
"Values": [
{
    "TagId": "5e1d88aa46af0d1748afd808",
    "Allocation": [
    {
        "TagId": "5e1c721601680617242a1152",
        "Value": "Marketing"
    }
    ],
    "Amount": "3.08"
},
{
    "TagId": "5e1d88aa46af0d1748afd808",
    "Allocation": [
    {
        "TagId": "5e1c721601680617242a1152",
        "Value": "Sales"
    }
    ],
    "Amount": "5.00"
}]
 ```
 <list type="number">
 <item><description>- ConcurrencyKey - Provide the more recent value to prevent conflicts when multiple users update tag values at the same time.</description></item>
 <item><description>- TagId (Values array) - Unique identifier of the Tag definition. Refer to the allocation TagId when you create an allocation tag via `POST /Business/Configuration/Tag/Allocation`.</description></item>
 <item><description>- TagId (Allocation array) - Unique identifier of the Tag definition. Refer to Id when you create a tag definition via `POST /Business/Configuration/Tag/{tag-type}`.</description></item>
 <item><description>- Values - Values for the tag definition (for allocation TagId).</description></item>
 <item><description>- Amount - A portion of the transaction settlement amount alloted to each allocation.</description></item>
 </list>
 ### Response ###
 <list type="number">
 <item><description>- Id - Unique identifier for allocation tag values.</description></item>
 <item><description>- ConcurrencyKey - Most recently updated concurrency key.</description></item>
 <item><description>- State - Transaction review state. Possible values are: NotReviewed (default), Approved, Reject, Ignore.</description></item>
 </list>

> Body parameter

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Allocation": [
        {
          "TagId": "",
          "Value": {}
        }
      ],
      "Amount": 0
    }
  ]
}
```

<h3 id="update-allocation-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateAllocationTagValuesRequest](#schemaupdateallocationtagvaluesrequest)|true|UpdateAllocationTagValuesRequest object|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="update-allocation-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tags](#schematags)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create Allocation tag values for a transaction.

<a id="opIdTransactions_PostAllocationTagValuesByIdrequestAuthorizationPOSTTransactions/{Id}/Tags/Allocations"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags/Allocations HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Allocation": [
        {
          "TagId": "",
          "Value": {}
        }
      ],
      "Amount": 0
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags/Allocations',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Transactions/{Id}/Tags/Allocations`

 Allocations allow you to associate a transaction with multiple expense categories or accounts.  Allocation tags are arrays of other tag values.  An allocation tag cannot contain a reference to another allocation tag as only one may exist per business.
 
 ### Request ###
 Settled PEX transactions may be divided into multiple allocation sets.  Each set references one or more tag values and an allocation amount.

 The sum total of all allocation amounts must be equal to the transaction settlement amount.

 Transaction allocation values are required to contain a minimum of two sets of tag values.  Otherwise, for a single allocation use standard tag values. 
 ```
"Values": [
{
    "TagId": "5e1d88aa46af0d1748afd808",
    "Allocation": [
    {
        "TagId": "5e1c721601680617242a1152",
        "Value": "Marketing"
    }
    ],
    "Amount": "3.08"
},
{
    "TagId": "5e1d88aa46af0d1748afd808",
    "Allocation": [
    {
        "TagId": "5e1c721601680617242a1152",
        "Value": "Sales"
    }
    ],
    "Amount": "5.00"
}]
 ```
 <list type="number">
 <item><description>- ConcurrencyKey - Provide the more recent value to prevent conflicts when multiple users update tag values at the same time.</description></item>
 <item><description>- TagId(Values array) - Unique identifier of the Tag definition. Refer to the allocation TagId when you create an allocation tag via `POST /Business/Configuration/Tag/Allocation`.</description></item>
 <item><description>- TagId(Allocation array) - Unique identifier of the Tag definition. Refer to Id when you create a tag definition via `POST /Business/Configuration/Tag/{tag-type}`.</description></item>
 <item><description>- Values - Values for the tag definition (for allocation TagId).</description></item>
 <item><description>- Amount - A portion of the transaction settlement amount alloted to each allocation.</description></item>
 </list>
 ### Response ###
 <list type="number">
 <item><description>- Id - Unique identifier for allocation tag values.</description></item>
 <item><description>- ConcurrencyKey - Most recently updated concurrency key.</description></item>
 <item><description>- State - Transaction review state. Possible values are: NotReviewed (default), Approved, Reject, Ignore.</description></item>
 </list>

> Body parameter

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Allocation": [
        {
          "TagId": "",
          "Value": {}
        }
      ],
      "Amount": 0
    }
  ]
}
```

<h3 id="create-allocation-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|Transaction Id|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateAllocationTagValuesRequest](#schemacreateallocationtagvaluesrequest)|true|Create allocation tag value request|

> Example responses

> 201 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="create-allocation-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[Tags](#schematags)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Please update your outdated ConcurrencyKey value.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|url||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Delete Allocation tag values for a transaction.

<a id="opIdTransactions_DeleteAllocationTagValuesByIdConcurrencyKeyAuthorizationDELETETransactions/{Id}/Tags/Allocations?ConcurrencyKey={ConcurrencyKey}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags/Allocations?ConcurrencyKey=string HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Transactions/{Id}/Tags/Allocations?ConcurrencyKey=string',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Transactions/{Id}/Tags/Allocations`

Use this endpoint to delete all allocation values for a transaction.
### Response ###
<list type="number">
<item><description>- Id - Unique identifier for allocation tag values.</description></item>
<item><description>- ConcurrencyKey - Most recently updated concurrency key.</description></item>
<item><description>- State - Transaction review state. Possible values are: NotReviewed (default), Approved, Reject, Ignore.</description></item>
</list>

<h3 id="delete-allocation-tag-values-for-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int64)|true|Transaction Id|
|ConcurrencyKey|query|string|true|Concurrency Key|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="delete-allocation-tag-values-for-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tags](#schematags)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-virtualcard-create-and-review-virtual-card-orders-">VirtualCard : 
            Create and review virtual card orders.
            </h1>

## Create virtual cards for the business

<a id="opIdVirtualCard_OrderByorderRequestAuthorizationPOSTVirtualCard/Order"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/VirtualCard/Order HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "VirtualCards": [
    {
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "GroupId": 0,
      "RulesetId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": ""
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/VirtualCard/Order',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /VirtualCard/Order`

Create virtual cards for the business. The response to this call is a VirtualCardOrderId and NumberOfCardsRequested. <br/>
<br/>
To retrieve card order details (without sensitive data), including the card AcctId, use GET /VirtualCard/Order/{Id} <br/>
<br/>
Cards have an expiration date of 3 years and will renew automatically 60 days prior to expiration. 
If the card expiration is 01/20, the card will expire on the last day of the month, January 31, 2020. <br/>
<br/>
non-ASCII characters. Ex: "ñ" not allowed <br/>
Cardholder name may only include letters, numbers and the following punctuation symbols: , . - & ' <br/>
Cardholder first + last names must be no more than 23 characters <br/>
Email format: name@domain.com <br/>
Date format: MM-DD-YYYY, ex. 01-31-1970 <br/>
Phone format: 2125551212 or 212-555-1212, 10 digits can not begin with 1 <br/>
Zip Code should be 5 digits: 10018 <br/>
Country is always "US" <br/>
Address format: letters, numbers and the following punctuation symbols: . ' () , # - / <br/>
City format: letters, numbers and the following punctuation symbols: . ' () , # - / <br/>
State format: two letter format ex. "CA" <br/>
Max AddressLine1 field length: 26 characters <br/>
Max AddressLine2 field length: 26 characters <br/>
Max City field length: 25 characters <br/>
<br/>
To add a card to a group, use GroupId, otherwise there will be no group applied. 
To add a card to a group after the card order has been created, use PUT/Card/SetGroup. <br/>
To add spend rules to a card accountID, use RulesetId, otherwise there will be no spend rulesets applied. 
To add spend rules to a card after the card order has been created, use PUT/Card/SpendRules/{Id} <br/>
AutoActivation by default is set to true, if you want to activate your card(s) later it can be set to false. <br/>
FundCardAmount is optional from 0 - 50,000 (if $50,000 that is the maximum card balance). 
We allow for up to 2 decimal places, so 40.55. <br/>
CardDataWebhookURL requires https and the max length is 500 characters, so "https://myapp.awesome.pexcustomer.com" will suffice. 
You can add your own custom parameters in your webhook i.e. "https://myapp.awesome.pexcustomer.com?id=123&orderid=1234". <br/>
<br/>
If PEX is used for fuel authorizations, transit passes or online purchases, 
there will be times where the cardholder will have to key in the billing zip code as it appears on the cardholder profile. 
To avoid issues at the time of purchase, let the cardholder know what their billing (i.e. profile) address is. <br/>
<br/>
If the cardholder enters an invalid Zip Code 2 times, the merchant may refuse to accept additional card swipes. 
If this occurs, cardholders will have to see the attendant to complete a gas transaction, or use another form of payment. <br/>
<br/>
If the cardholder should have access to dashboard.pexcard.com to review their transaction history, etc., 
they will need the four (4) digit year of birth from their profile. 
If you are using a generic value, you will need to convey that to the cardholder. <br/>
<br/>
At card creation, the spend rule defaults are: <br/>
<list type="number">
  <item><description> - Daily spend limit is NONE <br/></description></item>
  <item><description> - International spending is OFF <br/></description></item>
  <item><description> - Card-not-present spending is ON <br/></description></item>
  <item><description> - All merchant categories are ON <br/></description></item>
</list>

> Body parameter

```json
{
  "VirtualCards": [
    {
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "GroupId": 0,
      "RulesetId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": ""
    }
  ]
}
```

<h3 id="create-virtual-cards-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[VirtualCardsOrderRequest](#schemavirtualcardsorderrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "VirtualCardOrderId": 0,
  "NumberOfCardsRequested": 0
}
```

<h3 id="create-virtual-cards-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[VirtualCardsOrderResponse](#schemavirtualcardsorderresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|<list type="number">
  <item>
    <description> - The GroupId does not exist <br /></description>
  </item>
  <item>
    <description> - The RulesetId does not exist <br /></description>
  </item>
  <item>
    <description> - Funding Card Amount you entered (X) is greater than the Maximum Card Balance (Y) <br /></description>
  </item>
  <item>
    <description> - Webhook host request is different than one registered with PEX </description>
  </item>
</list>|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description> - The business does not support Virtual Card feature <br /></description>
  </item>
  <item>
    <description> - Administrator lacking proper permissions to 'Add/Edit/Terminate Card' <br /></description>
  </item>
  <item>
    <description> - Administrator lacking proper permissions for 'Funding' of Card <br /></description>
  </item>
  <item>
    <description> - Card limit exceeded <br /></description>
  </item>
  <item>
    <description> - Balance on cards greater than business balance <br /></description>
  </item>
  <item>
    <description> - Webhook is not properly registered with PEX </description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return details for all virtual cards included in a virtual card order (note: will not return sensitive card data)

<a id="opIdVirtualCard_GetOrderByIdAuthorizationGETVirtualCard/Order/{id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/VirtualCard/Order/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /VirtualCard/Order/{id}`

After using POST /VirtualCard/Order to create one or more cards, you can use this call to retrieve the card order information, 
including the virtual card Account Id ("AcctId"). 
Note the response will not include any sensitive card data.

<h3 id="return-details-for-all-virtual-cards-included-in-a-virtual-card-order-(note:-will-not-return-sensitive-card-data)-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Virtual Card Order Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "Cards": [
    {
      "RequestId": 0,
      "AcctId": 0,
      "AccountNumber": "",
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "HomeAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "GroupId": 0,
      "SpendingRulesetsId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": "",
      "Status": "",
      "Errors": [
        "string"
      ],
      "ErrorMessage": ""
    }
  ]
}
```

<h3 id="return-details-for-all-virtual-cards-included-in-a-virtual-card-order-(note:-will-not-return-sensitive-card-data)-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[VirtualCardsGetOrderResponse](#schemavirtualcardsgetorderresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Virtual Card Order is not available (may belong to another business)|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Virtual Card Order does not exist|None|

<aside class="success">
This operation does not require authentication
</aside>

## Request to resend callback with sensitive card data

<a id="opIdVirtualCard_DataBydataRequestAuthorizationPOSTVirtualCard/Data"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/VirtualCard/Data HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "AcctId": 0,
  "CardDataWebhookURL": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/VirtualCard/Data',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /VirtualCard/Data`

Request to resend webhook/callback with sensitive card data for a single AcctId. 
This should only be used if the webhook from POST/VirtualCard/Order is not delivered. 
If successful, you receive no response, just the webhook. <br/>
<br/>
To retrieve card order details (without sensitive data), including the card AcctId, use GET /VirtualCard/Order/{Id}.

> Body parameter

```json
{
  "AcctId": 0,
  "CardDataWebhookURL": ""
}
```

<h3 id="request-to-resend-callback-with-sensitive-card-data-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[VirtualCardDataRequest](#schemavirtualcarddatarequest)|true|Account ID and webhook URL|

> Example responses

> 200 Response

```json
{}
```

<h3 id="request-to-resend-callback-with-sensitive-card-data-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|<list type="number">
  <item>
    <description> - AccountId is not found or is not associated with a Virtual Card Order<br /></description>
  </item>
  <item>
    <description> - Webhook host request is different than one registered with PEX</description>
  </item>
</list>|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description> - Cardholder does not belong to this business<br /></description>
  </item>
  <item>
    <description> - Webhook is not properly registered with PEX</description>
  </item>
</list>|None|

<h3 id="request-to-resend-callback-with-sensitive-card-data-responseschema">Response Schema</h3>

Status Code **200**

*IHttpActionResult*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-business-check-balances-and-transfers-manage-administrators-and-configure-business-settings-">Business : 
            Check balances and transfers, manage administrators, and configure business settings.
            </h1>

## Return details of all the available Tag definitions configured for the business

<a id="opIdBusiness_ConfigurationTagsByAuthorizationGETBusiness/Configuration/Tags"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/Configuration/Tags HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tags',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/Configuration/Tags`

Type - It defines the type of the tag on PEX platform. Valid values are: 
1. Dropdown
2. Text
3. Yes/No
4. Decimal

<h3 id="return-details-of-all-the-available-tag-definitions-configured-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
[
  {
    "Id": "",
    "Type": "",
    "Name": "",
    "Description": "",
    "IsEnabled": false,
    "IsDeleted": false,
    "IsRequired": false,
    "Order": 0,
    "ConcurrencyKey": "",
    "CreatedDateUtc": "",
    "CreatedBy": {
      "AdminId": 0,
      "UserId": 0
    },
    "UpdatedDateUtc": "",
    "UpdatedBy": {
      "AdminId": 0,
      "UserId": 0
    },
    "DeletedDateUtc": "",
    "DeletedBy": {
      "AdminId": 0,
      "UserId": 0
    }
  }
]
```

<h3 id="return-details-of-all-the-available-tag-definitions-configured-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

<h3 id="return-details-of-all-the-available-tag-definitions-configured-for-the-business-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Tag](#schematag)]|false|none|[Tag configuration]|
|» Tag|[Tag](#schematag)|false|none|Tag configuration|
|»» Id|string|false|none|Unique Identifier of the tag definition|
|»» Type|string|false|none|Type of the tag definition {Dropdown, Text, Decimal, Yes/No}|
|»» Name|string|false|none|Name of the tag definition|
|»» Description|string|false|none|Descriptive information about the tag definition|
|»» IsEnabled|boolean|false|none|This flag determines if the tag definition is visible to the card holder|
|»» IsDeleted|boolean|false|none|If set to true, the tag is deleted|
|»» IsRequired|boolean|false|none|If set to true, tag is not required|
|»» Order|integer(int32)|false|none|Determines the position where tag appears. It is a 0 based index|
|»» ConcurrencyKey|string|false|none|Concurrent editing token|
|»» CreatedDateUtc|string(date-time)|false|none|Date when the tag definition was created|
|»» CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|»»» AdminId|integer(int32)|false|none|Admin Id of the user who created, updated, or deleted the tag definition|
|»»» UserId|integer(int32)|false|none|User Id of the user who created, updated, or deleted the tag definition|
|»» UpdatedDateUtc|string(date-time)|false|none|Date when the tag definition was last updated|
|»» UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|»» DeletedDateUtc|string(date-time)|false|none|Date when the tag definition was deleted|
|»» DeletedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Text|
|Type|YesNo|
|Type|Dropdown|
|Type|Decimal|
|Type|Allocation|

<aside class="success">
This operation does not require authentication
</aside>

## Return details of single tag definition (specified by the {Id})

<a id="opIdBusiness_ConfigurationTagByIdAuthorizationGETBusiness/Configuration/Tag/{Id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/Configuration/Tag/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/Configuration/Tag/{Id}`

To get the Id of the specific tag definition please use GET /Business/Configuration/Tags<br/>
Type - It defines the type of the tag on PEX platform. Valid values are:
1. Dropdown
2. Text
3. Yes/No
4. Decimal

<h3 id="return-details-of-single-tag-definition-(specified-by-the-{id})-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|Tag Id|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="return-details-of-single-tag-definition-(specified-by-the-{id})-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tag](#schematag)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Updates a tag definition for Type = Dropdown

<a id="opIdBusiness_ConfigurationTagByIdrequestAuthorizationPUTBusiness/Configuration/Tag/Dropdown/{Id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ],
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Configuration/Tag/Dropdown/{Id}`

Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.

> Body parameter

```json
{
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ],
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="updates-a-tag-definition-for-type-=-dropdown-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateDropdownTagRequest](#schemaupdatedropdowntagrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}
```

<h3 id="updates-a-tag-definition-for-type-=-dropdown-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DropdownTag](#schemadropdowntag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a tag definition for Type = Dropdown

<a id="opIdBusiness_ConfigurationTagDropdownByIdAuthorizationDELETEBusiness/Configuration/Tag/Dropdown/{Id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Business/Configuration/Tag/Dropdown/{Id}`

To get the Id of the tag definition, please use GET /Business/Configuration/Tags.

<h3 id="delete-a-tag-definition-for-type-=-dropdown-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}
```

<h3 id="delete-a-tag-definition-for-type-=-dropdown-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DropdownTag](#schemadropdowntag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a tag definition for Type = Dropdown

<a id="opIdBusiness_ConfigurationTagDropdownByrequestAuthorizationPOSTBusiness/Configuration/Tag/Dropdown"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false,
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Configuration/Tag/Dropdown`

IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag. <br/>
Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e.Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.<br/>

> Body parameter

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false,
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}
```

<h3 id="create-a-tag-definition-for-type-=-dropdown-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateDropdownTagRequest](#schemacreatedropdowntagrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}
```

<h3 id="create-a-tag-definition-for-type-=-dropdown-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[DropdownTag](#schemadropdowntag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|string||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Create option(s) for the Type = Dropdown.

<a id="opIdBusiness_ConfigurationTagOptionsByIdrequestAuthorizationPOSTBusiness/Configuration/Tag/Dropdown/{Id}/Options"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id}/Options HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id}/Options',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Configuration/Tag/Dropdown/{Id}/Options`

IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag.<br/>
Order - Determines the position where Tag appears on UI. It is a 0 based index i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.<br/>

> Body parameter

```json
{
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}
```

<h3 id="create-option(s)-for-the-type-=-dropdown.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[TagOptionsRequest](#schematagoptionsrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}
```

<h3 id="create-option(s)-for-the-type-=-dropdown.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DropdownTag](#schemadropdowntag)|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[DropdownTag](#schemadropdowntag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Tag is not dropdown type.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|string||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Create a tag definition for Type = Text

<a id="opIdBusiness_ConfigurationTagTextByrequestAuthorizationPOSTBusiness/Configuration/Tag/Text"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Text HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Length": 0,
  "ValidationType": "",
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Text',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Configuration/Tag/Text`

ValidationType - Determines the kind of values this tag is allowed to have. Valid values are:
1. None
2. Numeric
3. Alphabetic
4. Alphanumeric

Length - Defines the number of characters allowed for this tag. It takes numeric values E.g. Length: 5 means the tag can have up to 5 characters.<br/>
IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag.<br/>
Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field. <br/>

> Body parameter

```json
{
  "Length": 0,
  "ValidationType": "",
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="create-a-tag-definition-for-type-=-text-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateTextTagRequest](#schemacreatetexttagrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "Length": 0,
  "ValidationType": "",
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="create-a-tag-definition-for-type-=-text-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[TextTag](#schematexttag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|url||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Updates a tag definition for Type = Text

<a id="opIdBusiness_ConfigurationTagTextByIdrequestAuthorizationPUTBusiness/Configuration/Tag/Text/{Id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Text/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Length": 0,
  "ValidationType": "",
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Text/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Configuration/Tag/Text/{Id}`

ValidationType - Determines the kind of values this tag is allowed to have.
Valid values are:
1. None
2. Numeric
3. Alphabetic
4. Alphanumeric

Length - Defines the number of characters allowed for this tag.It takes numeric values E.g.Length: 5 means the tag can have up to 5 characters.
Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.

> Body parameter

```json
{
  "Length": 0,
  "ValidationType": "",
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="updates-a-tag-definition-for-type-=-text-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateTextTagRequest](#schemaupdatetexttagrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Length": 0,
  "ValidationType": "",
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="updates-a-tag-definition-for-type-=-text-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[TextTag](#schematexttag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Deletes a tag definition for Type = Text.

<a id="opIdBusiness_ConfigurationTagTextByIdAuthorizationDELETEBusiness/Configuration/Tag/Text/{Id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Text/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Text/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Business/Configuration/Tag/Text/{Id}`

To get the Id of the tag definition, please use GET /Business/Configuration/Tags.

<h3 id="deletes-a-tag-definition-for-type-=-text.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Length": 0,
  "ValidationType": "",
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="deletes-a-tag-definition-for-type-=-text.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[TextTag](#schematexttag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a tag definition for Type = Decimal

<a id="opIdBusiness_ConfigurationTagDecimalByrequestAuthorizationPOSTBusiness/Configuration/Tag/Decimal"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Decimal HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Decimal',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Configuration/Tag/Decimal`

IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag.<br/>
Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field. <br/>

> Body parameter

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="create-a-tag-definition-for-type-=-decimal-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateTagRequest](#schemacreatetagrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="create-a-tag-definition-for-type-=-decimal-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|url||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Updates a tag definition for Type = Decimal.

<a id="opIdBusiness_ConfigurationTagDecimalByIdrequestAuthorizationPUTBusiness/Configuration/Tag/Decimal/{Id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Decimal/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Decimal/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Configuration/Tag/Decimal/{Id}`

Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.

> Body parameter

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="updates-a-tag-definition-for-type-=-decimal.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateTagRequest](#schemaupdatetagrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Length": 0,
  "ValidationType": "",
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="updates-a-tag-definition-for-type-=-decimal.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[TextTag](#schematexttag)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Deletes a tag definition for Type = Decimal

<a id="opIdBusiness_ConfigurationTagDecimalByIdAuthorizationDELETEBusiness/Configuration/Tag/Decimal/{Id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Decimal/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Decimal/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Business/Configuration/Tag/Decimal/{Id}`

To get the Id of the tag definition, please use GET /Business/Configuration/Tags.

<h3 id="deletes-a-tag-definition-for-type-=-decimal-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="deletes-a-tag-definition-for-type-=-decimal-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a tag definition for Type = Yes/No

<a id="opIdBusiness_ConfigurationTagYesNoByrequestAuthorizationPOSTBusiness/Configuration/Tag/YesNo"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Configuration/Tag/YesNo HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/YesNo',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Configuration/Tag/YesNo`

IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag.
Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.

> Body parameter

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="create-a-tag-definition-for-type-=-yes/no-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateTagRequest](#schemacreatetagrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="create-a-tag-definition-for-type-=-yes/no-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|url||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Update a tag definition for Type = Yes/No

<a id="opIdBusiness_ConfigurationTagYesNoByIdrequestAuthorizationPUTBusiness/Configuration/Tag/YesNo/{Id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Configuration/Tag/YesNo/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/YesNo/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Configuration/Tag/YesNo/{Id}`

Order - Determines the position where Tag appears on UI. It is 0 based index i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.

> Body parameter

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}
```

<h3 id="update-a-tag-definition-for-type-=-yes/no-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateTagRequest](#schemaupdatetagrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="update-a-tag-definition-for-type-=-yes/no-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tag](#schematag)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a tag definition for Type = Yes/No

<a id="opIdBusiness_ConfigurationTagYesNoByIdAuthorizationDELETEBusiness/Configuration/Tag/YesNo/{Id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Business/Configuration/Tag/YesNo/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/YesNo/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Business/Configuration/Tag/YesNo/{Id}`

To get the Id of the tag definition, please use GET /Business/Configuration/Tags.

<h3 id="delete-a-tag-definition-for-type-=-yes/no-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="delete-a-tag-definition-for-type-=-yes/no-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update a tag definition for Type = Allocation

<a id="opIdBusiness_ConfigurationTagAllocationPutByAuthorizationPUTBusiness/Configuration/Tag/Allocation"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Allocation HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Allocation',
{
  method: 'PUT',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Configuration/Tag/Allocation`

Allocations allow you to associate a transaction with multiple expense categories or accounts.

Settled PEX transactions may be divided into multiple allocation sets.  Each set references one or more tag values and an allocation amount.
            
The sum total of all allocation amounts must be equal to the transaction settlement amount.
            
A transaction with allocations is required to contain a minimum of two sets of Allocation tag values.  Otherwise, for a single allocation use standard tag values.
<list type = "number" >
<item><description>- ConcurrencyKey - Provide the more recent value to prevent conflicts when multiple users update tag values at the same time.</description></item>
<item><description>- IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag.</description></item>
<item><description>- Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.</description></item>
<item><description>- Tags - Array of TagId and Value property pairs.</description></item>
</list>

<h3 id="update-a-tag-definition-for-type-=-allocation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Tags": [
    {
      "TagId": "",
      "Order": ""
    }
  ]
}
```

<h3 id="update-a-tag-definition-for-type-=-allocation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[AllocationTag](#schemaallocationtag)|

<aside class="success">
This operation does not require authentication
</aside>

## Create a tag definition for Type = Allocation

<a id="opIdBusiness_ConfigurationTagAllocationPostByAuthorizationPOSTBusiness/Configuration/Tag/Allocation"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Allocation HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Allocation',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Configuration/Tag/Allocation`

Allocations allow you to associate a transaction with multiple expense categories or accounts.

Settled PEX transactions may be divided into multiple allocation sets.  Each set references one or more tag values and an allocation amount.
            
The sum total of all allocation amounts must be equal to the transaction settlement amount.
            
A transaction with allocations is required to contain a minimum of two sets of Allocation tag values.  Otherwise, for a single allocation use standard tag values.
<list type = "number" >
<item><description>- ConcurrencyKey - Provide the more recent value to prevent conflicts when multiple users update tag values at the same time.</description></item>
<item><description>- IsRequired - If set to true, the User can not save the tag selection without selecting a value for this tag.</description></item>
<item><description>- Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e. Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.</description></item>
<item><description>- Tags - Array of TagId and Value property pairs.</description></item>
</list>

<h3 id="create-a-tag-definition-for-type-=-allocation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 201 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Tags": [
    {
      "TagId": "",
      "Order": ""
    }
  ]
}
```

<h3 id="create-a-tag-definition-for-type-=-allocation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[AllocationTag](#schemaallocationtag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request is invalid.|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|url||URL to the newly created resource.|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a tag definition for Type = Allocation

<a id="opIdBusiness_ConfigurationTagAllocationByIdAuthorizationDELETEBusiness/Configuration/Tag/Allocation/{Id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Allocation/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Allocation/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Business/Configuration/Tag/Allocation/{Id}`

Delete one of the tag type = allocations. Once the allocation tag definition is deleted transaction split is not possible going forward. 
To get the Id of the tag definition, please use GET /Business/Configuration/Tags.

<h3 id="delete-a-tag-definition-for-type-=-allocation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}
```

<h3 id="delete-a-tag-definition-for-type-=-allocation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request.|None|

<aside class="success">
This operation does not require authentication
</aside>

## Updates a tag option definition for Type = Dropdown

<a id="opIdBusiness_ConfigurationTagOptionByIdrequestAuthorizationPUTBusiness/Configuration/Tag/Dropdown/{Id}/Option"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id}/Option HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Configuration/Tag/Dropdown/{Id}/Option',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Configuration/Tag/Dropdown/{Id}/Option`

To get the Id of the specific tag please use GET /Business/Configuration/Tags
Order - Determines the position where Tag appears on UI. It is a 0 based index, i.e.Order = 0 corresponds to 1st position of the tag in the list of tags. The default value is 0. It is a required field.

> Body parameter

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}
```

<h3 id="updates-a-tag-option-definition-for-type-=-dropdown-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|string|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateTagOptionRequest](#schemaupdatetagoptionrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}
```

<h3 id="updates-a-tag-option-definition-for-type-=-dropdown-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[TagOption](#schematagoption)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return list of PEX initiated ACH transfer requests for the business

<a id="opIdBusiness_OneTimeTransferByAuthorizationGETBusiness/OneTimeTransfer"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/OneTimeTransfer HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/OneTimeTransfer`

Return all one-time transfers for the business.<br/>
<br/>
One-time transfers are PEX initiated debit or credit ACH requests to/from your external business checking account-on-file to/from your PEXCard business account.<br/>
<br/>
One-time transfer Status definitions:<br/>
<list type="number">
<item><description>- Request: Not sent to bank yet, can be deleted up to 9:00pm ET on the day the request is made.<br/></description></item>
<item><description>- Pending: Sent to bank and will take up to four (4) business days to complete.<br/></description></item>
<item><description>- Complete: Funds were posted to the PEX account.<br/></description></item>
<item><description>- Rejected: Your bank refused the transaction. Most likely cause? Insufficient funds.<br/></description></item>
<item><description>- Deleted: Canceled by a PEX administrator.<br/></description></item>
<item><description>- Canceled: Bank Inactive, canceled by PEX due to external bank account status.<br/></description></item>
<item><description>- Cancel: Older transfers canceled by a PEX administrator.</description></item>
</list>

<h3 id="return-list-of-pex-initiated-ach-transfer-requests-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "OneTimeTransferDetails": [
    {
      "TransferRequestId": 0,
      "BankInformation": {
        "ExternalBankAcctId": 0,
        "RoutingNumber": "",
        "BankAccountNumber": "",
        "BankName": "",
        "BankAccountType": "",
        "IsActive": false
      },
      "Amount": 0,
      "Status": "",
      "RequestedDate": "",
      "FundAvailableDate": ""
    }
  ]
}
```

<h3 id="return-list-of-pex-initiated-ach-transfer-requests-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetOneTimeTransferResponse](#schemagetonetimetransferresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return the PEX business profile information

<a id="opIdBusiness_ProfileByAuthorizationGETBusiness/Profile"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/Profile HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript

const headers = {
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Profile',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/Profile`

Return the PEX business profile information including address, phone and initial contact information.

<h3 id="return-the-pex-business-profile-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

<h3 id="return-the-pex-business-profile-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Business is not open|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update the PEX business profile

<a id="opIdBusiness_ProfileByUserRequestAuthorizationPOSTBusiness/Profile"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Business/Profile HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json

Authorization: string

```

```javascript
const inputBody = '{
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "NormalizeAddress": false
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Profile',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Business/Profile`

Update the PEX business profile with the specified information.<br/>
<br/>
All fields are optional for update, however, some profile fields are required in the system and cannot be replaced by null or empty strings. Required system profile fields are:<br/>
<list type="number">
<item><description>- First Name<br/></description></item>
<item><description>- Last Name<br/></description></item>
<item><description>- Profile Address<br/></description></item>
<item><description>- Contact Name<br/></description></item>
<item><description>- Mobile Phone<br/></description></item>
<item><description>- Country<br/></description></item>
<item><description>- Date of Birth<br/></description></item>
<item><description>- Email.<br/></description></item>
</list> 
<br/>
Email format: name@domain.com<br/>
Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
Phone format: 2125551212<br/>
Zip code should be 5 digits: 10018.<br/>
<br/>
The API user must have EditBusinessProfile = true.

> Body parameter

```json
{
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "NormalizeAddress": false
}
```

<h3 id="update-the-pex-business-profile-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateBusinessProfileRequest](#schemaupdatebusinessprofilerequest)|true|Profile data|

<h3 id="update-the-pex-business-profile-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>Business is not open<br /></description>
  </item>
  <item>
    <description>Admin does not have permission</description>
  </item>
</list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return administrator profile and permissions

<a id="opIdBusiness_AdminByIdAuthorizationGETBusiness/Admin/{Id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/Admin/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/Admin/{Id}`

Return the profile and permissions for a specific active PEX administrator. A deleted or terminated administrator will not be returned.<br/>
<br/>
To obtain the administrator ID, use GET /Business/Admin.

<h3 id="return-administrator-profile-and-permissions-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Business admin ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}
```

<h3 id="return-administrator-profile-and-permissions-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[GetAdminResponse](#schemagetadminresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Invalid business admin ID<br /></description>
  </item>
  <item>
    <description>- Business is not open<br /></description>
  </item>
  <item>
    <description>- Admin does not have permission</description>
  </item>
</list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update an existing business administrator

<a id="opIdBusiness_AdminByEditRequestIdAuthorizationPUTBusiness/Admin/{Id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Business/Admin/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Business/Admin/{Id}`

Edit an active PEX administrator’s profile address or permissions.<br/>
<br/>
Email format: name@domain.com<br/>
Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
Phone format: 2125551212<br/>
Zip code should be 5 digits: 10018<br/>
<br/>
To retrieve a list of all active PEX administrators, use GET /Business/Admin.

> Body parameter

```json
{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}
```

<h3 id="update-an-existing-business-administrator-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|The business admin id to edit|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[EditAdminRequest](#schemaeditadminrequest)|true|Profile and permission data|

> Example responses

> 200 Response

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}
```

<h3 id="update-an-existing-business-administrator-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[EditAdminResponse](#schemaeditadminresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|<list type="number">
  <item>
    <description>Invalid address<br /></description>
  </item>
  <item>
    <description>Invalid name</description>
  </item>
</list>|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>Invalid business admin ID<br /></description>
  </item>
  <item>
    <description>Business is not open<br /></description>
  </item>
  <item>
    <description>Admin does not have permission</description>
  </item>
</list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a PEX administrator account

<a id="opIdBusiness_AdminByIdAuthorizationDELETEBusiness/Admin/{Id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Business/Admin/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript

const headers = {
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Business/Admin/{Id}`

Delete a PEX administrator account.<br/>
<br/>
Once an administrator account is deleted, it cannot be turned on again. Use POST /Business/Admin to create a new administrator record.<br/>
<br/>
To obtain the administrator ID, use GET /Business/Admin.
<br/>

<h3 id="delete-a-pex-administrator-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|Business admin ID|
|Authorization|header|string|true|token {USERTOKEN}|

<h3 id="delete-a-pex-administrator-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Invalid business admin ID|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

## List all administrator details for the business

<a id="opIdBusiness_AdminByAuthorizationGETBusiness/Admin"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/Admin HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Admin',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/Admin`

Return all active PEX administrator details, including administrator website permissions.  Any deleted or terminated administrators will not be returned.

<h3 id="list-all-administrator-details-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "BusinessAdmins": [
    {
      "BusinessAdminId": 0,
      "FirstName": "",
      "MiddleName": "",
      "LastName": "",
      "ProfileAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "Phone": "",
      "AltPhone": "",
      "DateOfBirth": "",
      "Email": "",
      "Permissions": {
        "ViewAdministration": false,
        "AddEditTerminateAdministrator": false,
        "RequestDeleteACHTransfer": false,
        "EditBusinessProfile": false,
        "AddEditTerminateCard": false,
        "RequestCardFunding": false,
        "ViewCardNumberReport": false,
        "ModifyTransactionNotes": false,
        "AdministerInstantIssueCards": false
      },
      "Status": ""
    }
  ]
}
```

<h3 id="list-all-administrator-details-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[GetAdminListResponse](#schemagetadminlistresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Business is not open<br /></description>
  </item>
  <item>
    <description>- Admin does not have permission</description>
  </item>
</list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return the balance of the business account

<a id="opIdBusiness_BalanceByAuthorizationGETBusiness/Balance"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Business/Balance HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Business/Balance',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Business/Balance`

Returns the current balance of your PEX business account.
<br/>
Please note that you will not be able to use your entire business balance to fund cards if you are required to maintain a minimum level of funds (typically $50) in your business account.

<h3 id="return-the-balance-of-the-business-account-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "BusinessAccountId": 0,
  "BusinessAccountBalance": 0
}
```

<h3 id="return-the-balance-of-the-business-account-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[GetBusinessBalanceResponse](#schemagetbusinessbalanceresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Standard security response if token is invalid|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|System error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-spendingruleset-build-policies-which-limit-card-spending-">SpendingRuleset : 
            Build policies which limit card spending.
            </h1>

## Return all cards with the advanced spending rulesets

<a id="opIdSpendingRuleset_AdvancedSpendingRulesetCardsByIdAuthorizationGETSpendingRuleset/{Id}/Advanced/Cards"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /SpendingRuleset/{Id}/Advanced/Cards`

What it does:<br/>
Retrieve all cards assigned to a particular spending ruleset.  The response includes all card details. <br/>

<h3 id="return-all-cards-with-the-advanced-spending-rulesets-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
[
  {
    "AccountId": 0,
    "Group": {
      "Id": 0,
      "GroupName": ""
    },
    "AccountStatus": "",
    "LedgerBalance": 0,
    "AvailableBalance": 0,
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "ShippingAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "ShippingPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "CardList": [
      {
        "CardId": 0,
        "IssuedDate": "",
        "ExpirationDate": "",
        "Last4CardNumber": "",
        "CardStatus": ""
      }
    ],
    "SpendingRulesetId": 0,
    "SpendRules": {
      "MerchantCategories": [
        {
          "Id": 0,
          "Name": "",
          "Description": "",
          "TransactionLimit": 0,
          "DailySpendLimit": 0,
          "WeeklySpendLimit": 0,
          "MonthlySpendLimit": 0,
          "YearlySpendLimit": 0,
          "LifetimeSpendLimit": 0
        }
      ],
      "InternationalSpendEnabled": false,
      "IsDailySpendLimitEnabled": false,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0,
      "CardNotPresentUse": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    },
    "ScheduledFunding": {
      "Amount": 0,
      "Frequency": ""
    },
    "LowBalanceFunding": {
      "ThresholdAmount": 0,
      "AmountToFund": 0
    },
    "CustomId": "",
    "IsVirtual": false
  }
]
```

<h3 id="return-all-cards-with-the-advanced-spending-rulesets-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid ruleset ID|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<h3 id="return-all-cards-with-the-advanced-spending-rulesets-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[AdvancedCardholderDetailsResponse](#schemaadvancedcardholderdetailsresponse)]|false|none|none|
|» AdvancedCardholderDetailsResponse|[AdvancedCardholderDetailsResponse](#schemaadvancedcardholderdetailsresponse)|false|none|none|
|»» AccountId|integer(int32)|false|none|Unique cardholder account id|
|»» Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|»»» Id|integer(int32)|true|none|Unique id of the cardholder group|
|»»» GroupName|string|true|none|Name of the cardholder group|
|»» AccountStatus|string|false|none|Cardholder account status (OPEN or CLOSED)|
|»» LedgerBalance|number(double)|false|none|Ledger balance for the card account, rounded to 2 decimal places|
|»» AvailableBalance|number(double)|false|none|Available balance for the card account, rounded to 2 decimal places|
|»» ProfileAddress|[AddressContact](#schemaaddresscontact)|false|none|none|
|»»» ContactName|string|false|none|none|
|»»» AddressLine1|string|true|none|none|
|»»» AddressLine2|string|false|none|none|
|»»» City|string|true|none|none|
|»»» State|string|true|none|none|
|»»» PostalCode|string|true|none|none|
|»»» Country|string|false|read-only|none|
|»» Phone|string|false|none|Phone number|
|»» ShippingAddress|[AddressContact](#schemaaddresscontact)|false|none|none|
|»» ShippingPhone|string|false|none|Shipping Phone number|
|»» DateOfBirth|string(date-time)|false|none|Cardholder date of birth|
|»» Email|string|false|none|Cardholder email address|
|»» CardList|[[CardDetail](#schemacarddetail)]|false|none|List of details about cards associated with the account|
|»»» CardDetail|[CardDetail](#schemacarddetail)|false|none|Details about a card|
|»»»» CardId|integer(int32)|true|none|Unique id for the card|
|»»»» IssuedDate|string(date-time)|true|none|Date card was issued|
|»»»» ExpirationDate|string(date-time)|true|none|Expiration date for the card|
|»»»» Last4CardNumber|string|true|none|Last four digits of card number|
|»»»» CardStatus|string|true|none|Card status<br /><br>            Possible string values for CardStatus parameter of card detail are: <br /><list type="enum"><item><description> - <i>Inactive</i>: All new Cards are Inactive, which means they can't be used to make purchases.<br /></description></item><item><description> - <i>Active</i>: Cards in this state can be used to make purchases when funded.<br /></description></item><item><description> - <i>Blocked</i>: In this state, cards cannot be used for purchases. It can be activated again for the use.<br /></description></item><item><description> - <i>Closed</i>: This Card account is closed. It can not be activated again for the purchase.<br /></description></item></list>|
|»» SpendingRulesetId|integer(int32)|false|none|SpendingRulesetId for the cardholder account|
|»» SpendRules|[AdvancedSpendRulesResponse](#schemaadvancedspendrulesresponse)|false|none|Advanced Spend Rules Response|
|»»» MerchantCategories|[[MerchantCategoryResponse](#schemamerchantcategoryresponse)]|false|none|List of merchant categories|
|»»»» MerchantCategoryResponse|[MerchantCategoryResponse](#schemamerchantcategoryresponse)|false|none|Merchant Category Response|
|»»»»» Id|integer(int32)|false|none|Merchant Category Id|
|»»»»» Name|string|false|none|Merchant Category Name|
|»»»»» Description|string|false|none|Merchant Category Description|
|»»»»» TransactionLimit|number(double)|false|none|Transaction limit, rounded to 2 decimal places|
|»»»»» DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|»»»»» WeeklySpendLimit|number(double)|false|none|Weekly spend limit, rounded to 2 decimal places|
|»»»»» MonthlySpendLimit|number(double)|false|none|Monthly spend limit, rounded to 2 decimal places|
|»»»»» YearlySpendLimit|number(double)|false|none|Yearly spend limit, rounded to 2 decimal places|
|»»»»» LifetimeSpendLimit|number(double)|false|none|Lifetime spend limit, rounded to 2 decimal places|
|»»» InternationalSpendEnabled|boolean|false|none|Whether or not international spend is enabled|
|»»» IsDailySpendLimitEnabled|boolean|false|none|Whether or not a daily spend limit is set|
|»»» DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|»»» WeeklySpendLimit|number(double)|false|none|Weekly spend limit, rounded to 2 decimal places|
|»»» MonthlySpendLimit|number(double)|false|none|Monthly spend limit, rounded to 2 decimal places|
|»»» YearlySpendLimit|number(double)|false|none|Yearly spend limit, rounded to 2 decimal places|
|»»» LifetimeSpendLimit|number(double)|false|none|Lifetime spend limit, rounded to 2 decimal places|
|»»» CardNotPresentUse|boolean|false|none|Whether or not card is present to use|
|»»» UsePexAccountBalanceForAuths|boolean|false|none|Whether or not auto business balance funding to use|
|»»» UseCustomerAuthDecision|boolean|false|none|Whether or not decision control allowed to use|
|»» ScheduledFunding|[ScheduledFunding](#schemascheduledfunding)|false|none|Details about scheduled funding|
|»»» Amount|number(double)|true|none|Amount of scheduled funding, rounded to 2 decimal places|
|»»» Frequency|string|true|none|Describes when scheduled funding should occur.<br /><br>            Possible string values for Frequency parameter of scheduled funding are: <br /><list type="enum"><item><description> - '0' or 'DAY' - every Day<br /></description></item><item><description> - '1' or 'MONDAY' - every Monday<br /></description></item><item><description> - '2' or 'TUESDAY' - every Tuesday<br /></description></item><item><description> - '3' or 'WEDNESDAY' - every Wednesday<br /></description></item><item><description> - '4' or 'THURSDAY' - every Thursday<br /></description></item><item><description> - '5' or 'FRIDAY' - every Friday<br /></description></item><item><description> - '6' or 'SATURDAY' - every Saturday<br /></description></item><item><description> - '7' or 'SUNDAY' - every Sunday<br /></description></item><item><description> - '8' or 'FIRSTOFMONTH' - every 1st of the Month<br /></description></item></list>|
|»» LowBalanceFunding|[LowBalanceFunding](#schemalowbalancefunding)|false|none|Details about low balance funding|
|»»» ThresholdAmount|number(double)|true|none|Threshold, rounded to 2 decimal places, to determine when funding should occur|
|»»» AmountToFund|number(double)|true|none|Amount, rounded to 2 decimal places, to fund when threshold is hit|
|»» CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|
|»» IsVirtual|boolean|false|none|Identifies virtual cardholder|

#### Enumerated Values

|Property|Value|
|---|---|
|Frequency|DAY|
|Frequency|MONDAY|
|Frequency|TUESDAY|
|Frequency|WEDNESDAY|
|Frequency|THURSDAY|
|Frequency|FRIDAY|
|Frequency|SATURDAY|
|Frequency|SUNDAY|
|Frequency|FIRSTOFMONTH|

<aside class="success">
This operation does not require authentication
</aside>

## Return all advanced spending rulesets for the business

<a id="opIdSpendingRuleset_AdvancedSpendingRulesetByAuthorizationGETSpendingRuleset/Advanced"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /SpendingRuleset/Advanced`

What it does:<br/>
Return details of all advanced spending rulesets for the business. <br/>

<h3 id="return-all-advanced-spending-rulesets-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
[
  {
    "Id": 0,
    "Name": "",
    "CardCount": 0,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false,
    "MccRestrictions": false,
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ]
  }
]
```

<h3 id="return-all-advanced-spending-rulesets-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<h3 id="return-all-advanced-spending-rulesets-for-the-business-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[AdvancedSpendingRulesetItemResponse](#schemaadvancedspendingrulesetitemresponse)]|false|none|[Advanced Spending Ruleset Item Response]|
|» AdvancedSpendingRulesetItemResponse|[AdvancedSpendingRulesetItemResponse](#schemaadvancedspendingrulesetitemresponse)|false|none|Advanced Spending Ruleset Item Response|
|»» Id|integer(int32)|false|none|Id|
|»» Name|string|false|none|Name|
|»» CardCount|integer(int32)|false|none|Card Count|
|»» DailySpendLimit|number(double)|false|none|Daily Spend Limit|
|»» WeeklySpendLimit|number(double)|false|none|Weekly Spend Limit|
|»» MonthlySpendLimit|number(double)|false|none|Monthly Spend Limit|
|»» YearlySpendLimit|number(double)|false|none|Yearly Spend Limit|
|»» LifetimeSpendLimit|number(double)|false|none|Lifetime Spend Limit|
|»» InternationalAllowed|boolean|false|none|International Allowed|
|»» CardNotPresentAllowed|boolean|false|none|Card Not Present Allowed|
|»» UsePexAccountBalanceForAuths|boolean|false|none|Use Pex Account Balance For Auths|
|»» UseCustomerAuthDecision|boolean|false|none|Use Customer Auth Decision|
|»» MccRestrictions|boolean|false|none|MCC Restrictions|
|»» MerchantCategories|[[AdvancedSpendingRulesetMerchantCategoryItemResponse](#schemaadvancedspendingrulesetmerchantcategoryitemresponse)]|false|none|Merchant Categories|
|»»» AdvancedSpendingRulesetMerchantCategoryItemResponse|[AdvancedSpendingRulesetMerchantCategoryItemResponse](#schemaadvancedspendingrulesetmerchantcategoryitemresponse)|false|none|Advanced Spending Ruleset Merchant Category Item Response|
|»»»» Id|integer(int32)|false|none|Id|
|»»»» Name|string|false|none|Name|
|»»»» Description|string|false|none|Description|
|»»»» TransactionLimit|number(double)|false|none|Transaction Limit|
|»»»» DailySpendLimit|number(double)|false|none|Daily Spend Limit|
|»»»» WeeklySpendLimit|number(double)|false|none|Weekly Spend Limit|
|»»»» MonthlySpendLimit|number(double)|false|none|Monthly Spend Limit|
|»»»» YearlySpendLimit|number(double)|false|none|Yearly Spend Limit|
|»»»» LifetimeSpendLimit|number(double)|false|none|Lifetime Spend Limit|

<aside class="success">
This operation does not require authentication
</aside>

## Update advanced spending ruleset for the business

<a id="opIdSpendingRuleset_AdvanceSpendingRulesetByreqAuthorizationPUTSpendingRuleset/Advanced"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Id": 0,
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /SpendingRuleset/Advanced`

What it does:<br/>
Modify an existing advanced spending ruleset.<br/>
<br/>
When you might use it.<br/>
<list type="number">
<item>1. Renaming the advanced spend ruleset.</item><br/>
<item>2. Resetting the daily spending limit (including the ability to assign no limit).</item><br/>
<item>3. Allowing or not allowing international use.</item><br/>
<item>4. Allowing or not allowing card not present use.</item><br/>
<item>5. Turning merchant categories on or off.</item><br/>
</list>

> Body parameter

```json
{
  "Id": 0,
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

<h3 id="update-advanced-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateAdvancedSpendingRulesetRequest](#schemaupdateadvancedspendingrulesetrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": 0,
  "Name": "",
  "CardCount": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false,
  "MccRestrictions": false,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "Description": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ]
}
```

<h3 id="update-advanced-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[AdvancedSpendingRulesetItemResponse](#schemaadvancedspendingrulesetitemresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|<list type='number'><item><description>- Invalid merchant category<br/></description></item><item><description>- Invalid ruleset ID<br/></description></item><item><description>- Merchant categories duplicated<br/></description></item><item><description>- Merchant spend limit exceeds overall spend limit<br/></description></item></list>|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type='number'><item><description>- Name already exists<br/></description></item><item><description>- This business does not support the Customer Authorization Decision<br/></description></item><item><description>- This business does not support the PEX Account balance instead of card balance<br/></description></item></list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create advanced spending ruleset for the business

<a id="opIdSpendingRuleset_AdvanceSpendingRulesetByreqAuthorizationPOSTSpendingRuleset/Advanced"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /SpendingRuleset/Advanced`

What it does:<br/>
Create a new advanced spending ruleset for the business.<br/>
Once the ruleset is created, it can be assigned to one or many cards.<br/>
<br/>
An advanced spending ruleset is a group of spend rules that can be applied to multiple card accounts. For example, if all cardholders should be allowed to spend at restaurants and fuel pumps, the administrator can create a spending ruleset that has only those merchant categories 'checked'. Every card with that ruleset applied can only spend at restaurants and fuel pumps.<br/>
<br/>
At card creation, the spend rule defaults are:<br/>
<list type="number">
<item><description>- Daily spend limit NONE<br/></description></item>
<item><description>- Weeklyly spend limit NONE<br/></description></item>
<item><description>- Monthly spend limit NONE<br/></description></item>
<item><description>- Yearly spend limit NONE<br/></description></item>
<item><description>- Lifetime spend limit NONE<br/></description></item>
<item><description>- International spending is OFF<br/></description></item>
<item><description>- All merchant categories are ON<br/></description></item>
</list>
<br/>
If your business allows cardholders to "Use your PEX Account balance" for transactions, you must set a value for "DailySpendLimit" for those cardholders. The "DailySpendLimit" value must be less than or equal to the PEX assigned daily spend limit for your business (typically $5,000 USD).<br/>
<br/>
CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone.<br/>
True - Can use when card is not present.<br/>
False - Cannot use when card is not present.<br/>
<br/>
PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):<br/>
<list type="number">
<item><description>- Associations & organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
<item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
<item><description>- Educational services: Schools, training programs<br/></description></item>
<item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
<item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets.<br/></description></item>
<item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
<item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
<item><description>- Healthcare & Childcare services: Medical services, hospitals, daycare<br/></description></item>
<item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
<item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
<item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
<item><description>- Travel & transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
<item><description>- Fuel Pump Only: Outdoor fuel pumps (i.e. Pay at the Pump)<br/></description></item>
<item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
</list>

> Body parameter

```json
{
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

<h3 id="create-advanced-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateAdvancedSpendingRulesetRequest](#schemacreateadvancedspendingrulesetrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```

<h3 id="create-advanced-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[CreateAdvancedSpendingRulesetResponse](#schemacreateadvancedspendingrulesetresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|<list type='number'><item><description>- Invalid merchant category<br/></description></item><item><description>- Merchant categories duplicated<br/></description></item><item><description>- Merchant spend limit exceeds overall spend limit<br/></description></item></list>|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type='number'><item><description>- Name already exists<br/></description></item><item><description>- This business does not support the Customer Authorization Decision<br/></description></item><item><description>- This business does not support the PEX Account balance instead of card balance<br/></description></item></list>|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete advanced spending ruleset for the business

<a id="opIdSpendingRuleset_AdvanceSpendingRulesetByreqAuthorizationDELETESpendingRuleset/Advanced"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json

Authorization: string

```

```javascript
const inputBody = '{
  "Id": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'DELETE',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /SpendingRuleset/Advanced`

What it does:<br/>
Delete an existing advanced spending ruleset for the business.<br/>
If one or more cards are assigned to a ruleset, that ruleset cannot be deleted.<br/>

> Body parameter

```json
{
  "Id": 0
}
```

<h3 id="delete-advanced-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[DeleteAdvancedSpendingRulesetRequest](#schemadeleteadvancedspendingrulesetrequest)|true|none|

<h3 id="delete-advanced-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid ruleset ID|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|This spending ruleset is currently assigned to one or more cards.|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return an advanced spending ruleset for the business

<a id="opIdSpendingRuleset_AdvancedSpendingRulesetByIdAuthorizationGETSpendingRuleset/{Id}/Advanced"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /SpendingRuleset/{Id}/Advanced`

What it does:<br/>
Retrieve details of a specific advanced spending ruleset.<br/>

<h3 id="return-an-advanced-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Id": 0,
  "Name": "",
  "CardCount": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false,
  "MccRestrictions": false,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "Description": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ]
}
```

<h3 id="return-an-advanced-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[AdvancedSpendingRulesetItemResponse](#schemaadvancedspendingrulesetitemresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid ruleset ID|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|NotFound|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|InternalServerError|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return all spending rulesets for the business

<a id="opIdSpendingRuleset_SpendingRulesetByAuthorizationGETSpendingRuleset"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /SpendingRuleset`

What it does:<br/>
Return details of all spending rulesets for the business. <br/>

<h3 id="return-all-spending-rulesets-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "SpendingRulesets": [
    {
      "RulesetId": 0,
      "SpendingRulesetCategories": {
        "CategoryId": 0,
        "AssociationsOrganizationsAllowed": false,
        "AutomotiveDealersAllowed": false,
        "EducationalServicesAllowed": false,
        "EntertainmentAllowed": false,
        "FuelPumpsAllowed": false,
        "GasStationsConvenienceStoresAllowed": false,
        "GroceryStoresAllowed": false,
        "HealthcareChildcareServicesAllowed": false,
        "ProfessionalServicesAllowed": false,
        "RestaurantsAllowed": false,
        "RetailStoresAllowed": false,
        "TravelTransportationAllowed": false,
        "HardwareStoresAllowed": false
      },
      "MccRestrictions": false,
      "BacctId": 0,
      "Name": "",
      "CountCardsPresent": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0,
      "InternationalAllowed": false,
      "CardNotPresentAllowed": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    }
  ]
}
```

<h3 id="return-all-spending-rulesets-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetSpendingRulesetsResponse](#schemagetspendingrulesetsresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Update spending ruleset for the business

<a id="opIdSpendingRuleset_SpendingRulesetByreqAuthorizationPUTSpendingRuleset"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "RulesetId": 0,
  "Name": "",
  "CountCardsPresent": 0,
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /SpendingRuleset`

What it does:<br/>
Modify an existing spending ruleset.<br/>
<br/>
When you might use it.<br/>
<list type="number">
<item>1. Renaming the spend ruleset.</item><br/>
<item>2. Resetting the daily spending limit (including the ability to assign no limit).</item><br/>
<item>3. Allowing or not allowing international use.</item><br/>
<item>4. Allowing or not allowing card not present use.</item><br/>
<item>5. Turning merchant categories on or off.</item><br/>
</list>

> Body parameter

```json
{
  "RulesetId": 0,
  "Name": "",
  "CountCardsPresent": 0,
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

<h3 id="update-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateSpendingRulesetRequest](#schemaupdatespendingrulesetrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```

<h3 id="update-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[SpendingRulesetResponse](#schemaspendingrulesetresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Create spending ruleset for the business

<a id="opIdSpendingRuleset_SpendingRulesetByreqAuthorizationPOSTSpendingRuleset"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": "",
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /SpendingRuleset`

What it does:<br/>
Create a new spending ruleset for the business.<br/>
Once the ruleset is created, it can be assigned to one or many cards.<br/>
<br/>
A spending ruleset is a group of spend rules that can be applied to multiple card accounts. For example, if all cardholders should be allowed to spend at restaurants and fuel pumps, the administrator can create a spending ruleset that has only those merchant categories 'checked'. Every card with that ruleset applied can only spend at restaurants and fuel pumps.<br/>
<br/>
At card creation, the spend rule defaults are:<br/>
<list type="number">
<item><description>- Daily spend limit NONE<br/></description></item>
<item><description>- International spending is OFF<br/></description></item>
<item><description>- All merchant categories are ON<br/></description></item>
</list>
<br/>
If your business allows cardholders to "Use your PEX Account balance" for transactions, you must set a value for "DailySpendLimit" for those cardholders. The "DailySpendLimit" value must be less than or equal to the PEX assigned daily spend limit for your business (typically $5,000 USD).<br/>
<br/>
CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone.<br/>
True - Can use when card is not present.<br/>
False - Cannot use when card is not present.<br/>
<br/>
PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):<br/>
<list type="number">
<item><description>- Associations & organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
<item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
<item><description>- Educational services: Schools, training programs<br/></description></item>
<item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
<item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets<br/></description></item>
<item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
<item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
<item><description>- Healthcare & Childcare services: Medical services, hospitals, daycare<br/></description></item>
<item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
<item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
<item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
<item><description>- Travel & transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
<item><description>- Fuel Pump Only: Outdoor fuel pumps (i.e. Pay at the Pump)<br/></description></item>
<item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
</list>

> Body parameter

```json
{
  "Name": "",
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

<h3 id="create-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateSpendingRulesetRequest](#schemacreatespendingrulesetrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```

<h3 id="create-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[CreateSpendingRulesetResponse](#schemacreatespendingrulesetresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete spending ruleset for the business

<a id="opIdSpendingRuleset_SpendingRulesetByreqAuthorizationDELETESpendingRuleset"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "RulesetId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'DELETE',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /SpendingRuleset`

What it does:<br/>
Delete an existing spending ruleset for the business.<br/>
If one or more cards are assigned to a ruleset, that ruleset cannot be deleted.<br/>

> Body parameter

```json
{
  "RulesetId": 0
}
```

<h3 id="delete-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[DeleteSpendingRulesetRequest](#schemadeletespendingrulesetrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```

<h3 id="delete-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[SpendingRulesetResponse](#schemaspendingrulesetresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return a spending ruleset for the business

<a id="opIdSpendingRuleset_SpendingRulesetByIdAuthorizationGETSpendingRuleset/{Id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /SpendingRuleset/{Id}`

What it does:<br/>
Retrieve details of a specific spending ruleset.<br/>

<h3 id="return-a-spending-ruleset-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "SpendingRuleset": {
    "RulesetId": 0,
    "Name": "",
    "DailySpendLimit": 0,
    "SpendingRulesetCategories": {
      "CategoryId": 0,
      "AssociationsOrganizationsAllowed": false,
      "AutomotiveDealersAllowed": false,
      "EducationalServicesAllowed": false,
      "EntertainmentAllowed": false,
      "FuelPumpsAllowed": false,
      "GasStationsConvenienceStoresAllowed": false,
      "GroceryStoresAllowed": false,
      "HealthcareChildcareServicesAllowed": false,
      "ProfessionalServicesAllowed": false,
      "RestaurantsAllowed": false,
      "RetailStoresAllowed": false,
      "TravelTransportationAllowed": false,
      "HardwareStoresAllowed": false
    },
    "MccRestrictions": false,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}
```

<h3 id="return-a-spending-ruleset-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetSpendingRulesetResponse](#schemagetspendingrulesetresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return all cards with the spending rulesets

<a id="opIdSpendingRuleset_SpendingRulesetCardsByIdAuthorizationGETSpendingRuleset/{Id}/Cards"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /SpendingRuleset/{Id}/Cards`

What it does:<br/>
Retrieve all cards assigned to a particular spending ruleset.  The response includes all card details. <br/>

<h3 id="return-all-cards-with-the-spending-rulesets-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Id|path|integer(int32)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
[
  {
    "AccountId": 0,
    "Group": {
      "Id": 0,
      "GroupName": ""
    },
    "AccountStatus": "",
    "LedgerBalance": 0,
    "AvailableBalance": 0,
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "ShippingAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "ShippingPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "IsVirtual": false,
    "CardList": [
      {
        "CardId": 0,
        "IssuedDate": "",
        "ExpirationDate": "",
        "Last4CardNumber": "",
        "CardStatus": ""
      }
    ],
    "SpendingRulesetId": 0,
    "SpendRules": {
      "UseMerchantCategory": false,
      "MerchantCategories": {
        "AssociationsAndOrganizations": false,
        "AutomotiveDealers": false,
        "EducationalServices": false,
        "Entertainment": false,
        "FuelAndConvenienceStores": false,
        "GroceryStores": false,
        "HealthcareAndChildcareServices": false,
        "ProfessionalServices": false,
        "Restaurants": false,
        "RetailStores": false,
        "TravelAndTransportation": false,
        "FuelPumpOnly": false,
        "HardwareStores": false
      },
      "InternationalSpendEnabled": false,
      "IsDailySpendLimitEnabled": false,
      "DailySpendLimit": 0,
      "CardNotPresentUse": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    },
    "ScheduledFunding": {
      "Amount": 0,
      "Frequency": ""
    },
    "LowBalanceFunding": {
      "ThresholdAmount": 0,
      "AmountToFund": 0
    },
    "CustomId": ""
  }
]
```

<h3 id="return-all-cards-with-the-spending-rulesets-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|No cards found.|Inline|

<h3 id="return-all-cards-with-the-spending-rulesets-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[CardholderDetailsResponse](#schemacardholderdetailsresponse)]|false|none|[Details about a cardholder account]|
|» CardholderDetailsResponse|[CardholderDetailsResponse](#schemacardholderdetailsresponse)|false|none|Details about a cardholder account|
|»» AccountId|integer(int32)|true|none|Unique cardholder account id|
|»» Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|»»» Id|integer(int32)|true|none|Unique id of the cardholder group|
|»»» GroupName|string|true|none|Name of the cardholder group|
|»» AccountStatus|string|true|none|Cardholder account status (OPEN or CLOSED)|
|»» LedgerBalance|number(double)|true|none|Ledger balance for the card account, rounded to 2 decimal places|
|»» AvailableBalance|number(double)|true|none|Available balance for the card account, rounded to 2 decimal places|
|»» ProfileAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|»»» ContactName|string|false|none|none|
|»»» AddressLine1|string|true|none|none|
|»»» AddressLine2|string|false|none|none|
|»»» City|string|true|none|none|
|»»» State|string|true|none|none|
|»»» PostalCode|string|true|none|none|
|»»» Country|string|false|read-only|none|
|»» Phone|string|false|none|Phone number|
|»» ShippingAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|»» ShippingPhone|string|false|none|Shipping Phone number|
|»» DateOfBirth|string(date-time)|true|none|Cardholder date of birth|
|»» Email|string|true|none|Cardholder email address|
|»» IsVirtual|boolean|false|none|Identifies virtual cardholder|
|»» CardList|[[CardDetail](#schemacarddetail)]|true|none|List of details about cards associated with the account|
|»»» CardDetail|[CardDetail](#schemacarddetail)|false|none|Details about a card|
|»»»» CardId|integer(int32)|true|none|Unique id for the card|
|»»»» IssuedDate|string(date-time)|true|none|Date card was issued|
|»»»» ExpirationDate|string(date-time)|true|none|Expiration date for the card|
|»»»» Last4CardNumber|string|true|none|Last four digits of card number|
|»»»» CardStatus|string|true|none|Card status<br /><br>            Possible string values for CardStatus parameter of card detail are: <br /><list type="enum"><item><description> - <i>Inactive</i>: All new Cards are Inactive, which means they can't be used to make purchases.<br /></description></item><item><description> - <i>Active</i>: Cards in this state can be used to make purchases when funded.<br /></description></item><item><description> - <i>Blocked</i>: In this state, cards cannot be used for purchases. It can be activated again for the use.<br /></description></item><item><description> - <i>Closed</i>: This Card account is closed. It can not be activated again for the purchase.<br /></description></item></list>|
|»» SpendingRulesetId|integer(int32)|true|none|SpendingRulesetId for the cardholder account|
|»» SpendRules|[SpendRules](#schemaspendrules)|true|none|none|
|»»» UseMerchantCategory|boolean|false|none|none|
|»»» MerchantCategories|[MerchantCategories](#schemamerchantcategories)|false|none|none|
|»»»» AssociationsAndOrganizations|boolean|false|none|none|
|»»»» AutomotiveDealers|boolean|false|none|none|
|»»»» EducationalServices|boolean|false|none|none|
|»»»» Entertainment|boolean|false|none|none|
|»»»» FuelAndConvenienceStores|boolean|false|none|none|
|»»»» GroceryStores|boolean|false|none|none|
|»»»» HealthcareAndChildcareServices|boolean|false|none|none|
|»»»» ProfessionalServices|boolean|false|none|none|
|»»»» Restaurants|boolean|false|none|none|
|»»»» RetailStores|boolean|false|none|none|
|»»»» TravelAndTransportation|boolean|false|none|none|
|»»»» FuelPumpOnly|boolean|false|none|none|
|»»»» HardwareStores|boolean|false|none|none|
|»»» InternationalSpendEnabled|boolean|false|none|none|
|»»» IsDailySpendLimitEnabled|boolean|false|none|none|
|»»» DailySpendLimit|number(double)|false|none|none|
|»»» CardNotPresentUse|boolean|false|none|none|
|»»» UsePexAccountBalanceForAuths|boolean|false|none|none|
|»»» UseCustomerAuthDecision|boolean|false|none|none|
|»» ScheduledFunding|[ScheduledFunding](#schemascheduledfunding)|false|none|Details about scheduled funding|
|»»» Amount|number(double)|true|none|Amount of scheduled funding, rounded to 2 decimal places|
|»»» Frequency|string|true|none|Describes when scheduled funding should occur.<br /><br>            Possible string values for Frequency parameter of scheduled funding are: <br /><list type="enum"><item><description> - '0' or 'DAY' - every Day<br /></description></item><item><description> - '1' or 'MONDAY' - every Monday<br /></description></item><item><description> - '2' or 'TUESDAY' - every Tuesday<br /></description></item><item><description> - '3' or 'WEDNESDAY' - every Wednesday<br /></description></item><item><description> - '4' or 'THURSDAY' - every Thursday<br /></description></item><item><description> - '5' or 'FRIDAY' - every Friday<br /></description></item><item><description> - '6' or 'SATURDAY' - every Saturday<br /></description></item><item><description> - '7' or 'SUNDAY' - every Sunday<br /></description></item><item><description> - '8' or 'FIRSTOFMONTH' - every 1st of the Month<br /></description></item></list>|
|»» LowBalanceFunding|[LowBalanceFunding](#schemalowbalancefunding)|false|none|Details about low balance funding|
|»»» ThresholdAmount|number(double)|true|none|Threshold, rounded to 2 decimal places, to determine when funding should occur|
|»»» AmountToFund|number(double)|true|none|Amount, rounded to 2 decimal places, to fund when threshold is hit|
|»» CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

#### Enumerated Values

|Property|Value|
|---|---|
|Frequency|DAY|
|Frequency|MONDAY|
|Frequency|TUESDAY|
|Frequency|WEDNESDAY|
|Frequency|THURSDAY|
|Frequency|FRIDAY|
|Frequency|SATURDAY|
|Frequency|SUNDAY|
|Frequency|FIRSTOFMONTH|

<aside class="success">
This operation does not require authentication
</aside>

## Send test message to remote authorization server

<a id="opIdSpendingRuleset_TestRemoteAuthEndpointByAuthorizationPOSTTestRemoteAuthEndpoint"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/TestRemoteAuthEndpoint HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/TestRemoteAuthEndpoint',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /TestRemoteAuthEndpoint`

What it does:<br/>
Send test message to remote authorization server.<br/>

<h3 id="send-test-message-to-remote-authorization-server-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "StatusCode": "",
  "Ticks": 0
}
```

<h3 id="send-test-message-to-remote-authorization-server-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[RemoteAuthorizationResponse](#schemaremoteauthorizationresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|BadRequest|None|
|408|[Request Timeout](https://tools.ietf.org/html/rfc7231#section-6.5.7)|RequestTimeout|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-note-create-and-attach-notes-to-transactions-">Note : 
            Create and attach notes to transactions.
            </h1>

## Create a network transaction note

<a id="opIdNote_NetworkTransactionNoteBycreateRequestAuthorizationPOSTNote/NetworkTransactionNote"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "NoteText": "",
  "NetworkTransactionId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Note/NetworkTransactionNote`

 You may want to add a network transaction note to track a PO or invoice number.<br/>
 <br/>
Network transaction notes are alpha/numeric and can be added to cardholder funding, pending and settlement transactions.  Notes can be viewed on the administration website in transaction details and on reports.<br/>
<br/>
To add a note to a funding or settlement transaction, set Pending to false.  For authorization/hold transactions, set Pending to true.<br/>
<br/>
To retrieve the TransactionId, get a card transaction list using <br/>
GET /Details/AllCardholderTransactions<br/>
GET /Details/TransactionDetails<br/>
GET /Details/TransactionDetails/{Id}

> Body parameter

```json
{
  "NoteText": "",
  "NetworkTransactionId": 0
}
```

<h3 id="create-a-network-transaction-note-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateNoteByNetworkTransactionIdRequest](#schemacreatenotebynetworktransactionidrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```

<h3 id="create-a-network-transaction-note-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[NoteResponse](#schemanoteresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Update a transaction note

<a id="opIdNote_PutByidupdateRequestAuthorizationPUTNote/{id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Note/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "NoteText": "",
  "Pending": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Note/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Note/{id}`

To retrieve the NoteId, get a card transaction list using <br/>
GET /Details/AllCardholderTransactions<br/>
GET /Details/TransactionDetails<br/>
GET /Details/TransactionDetails/{Id}<br/>
<br/>
To edit a note on a funding or settlement transaction, set Pending to false. For authorization/hold transactions, set Pending to true.<br/>
<br/>
Transaction notes can also be edited from the administration website in transaction detail.

> Body parameter

```json
{
  "NoteText": "",
  "Pending": false
}
```

<h3 id="update-a-transaction-note-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Note Ic|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[NoteRequest](#schemanoterequest)|true|Details required to update note|

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```

<h3 id="update-a-transaction-note-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[NoteResponse](#schemanoteresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Note not found|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a transaction note

<a id="opIdNote_PostBycreateRequestAuthorizationPOSTNote"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Note HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "TransactionId": 0,
  "NoteText": "",
  "Pending": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Note',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Note`

 You may want to add a transaction note to track a PO or invoice number.<br/>
 <br/>
Transaction notes are alpha/numeric and can be added to cardholder funding, pending and settlement transactions.  Notes can be viewed on the administration website in transaction details and on reports.<br/>
<br/>
To add a note to a funding or settlement transaction, set Pending to false.  For authorization/hold transactions, set Pending to true.<br/>
<br/>
To retrieve the TransactionId, get a card transaction list using <br/>
GET /Details/AllCardholderTransactions<br/>
GET /Details/TransactionDetails<br/>
GET /Details/TransactionDetails/{Id}

> Body parameter

```json
{
  "TransactionId": 0,
  "NoteText": "",
  "Pending": false
}
```

<h3 id="create-a-transaction-note-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateNoteRequest](#schemacreatenoterequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```

<h3 id="create-a-transaction-note-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[NoteResponse](#schemanoteresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a transaction note

<a id="opIdNote_DeleteByiddeleteRequestAuthorizationDELETENote/{id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Note/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Pending": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Note/{id}',
{
  method: 'DELETE',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Note/{id}`

To retrieve the NoteId, get a card transaction list using <br/>
GET /Details/AllCardholderTransactions<br/>
GET /Details/TransactionDetails<br/>
GET /Details/TransactionDetails/{Id}<br/>
<br/>
To delete a note on a funding or settlement transaction, set Pending to false. For authorization/hold transactions, set Pending to true.<br/>
<br/>
Transaction notes can also be deleted from the administration website in transaction detail.

> Body parameter

```json
{
  "Pending": false
}
```

<h3 id="delete-a-transaction-note-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[DeleteNoteRequest](#schemadeletenoterequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```

<h3 id="delete-a-transaction-note-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[NoteResponse](#schemanoteresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Note not found|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-group-manage-groups-and-assign-cards-">Group : 
            Manage groups and assign cards.
            </h1>

## Return a list of groups for the business

<a id="opIdGroup_GetByAuthorizationGETGroup"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Group HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Group',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Group`

Retrieve the list of groups for the business, including the Id and group name.<br/>
<br/>
Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the dashboard.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

<h3 id="return-a-list-of-groups-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "Groups": [
    {
      "Id": 0,
      "Name": ""
    }
  ]
}
```

<h3 id="return-a-list-of-groups-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[GetGroupsResponse](#schemagetgroupsresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Update the group name

<a id="opIdGroup_PutByidupdateRequestAuthorizationPUTGroup/{id}"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Group/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Group/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Group/{id}`

To retrieve the GroupID, use Get /Group<br/>
<br/>
Edit the group name. Cardholders assigned to the group will be updated with the new group name. The administrator website will display fourteen (14) characters of the group name in the cardlist.<br/>
<br/>
Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the dashboard.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

> Body parameter

```json
{
  "Name": ""
}
```

<h3 id="update-the-group-name-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[UpdateGroupRequest](#schemaupdategrouprequest)|true|Details required to update group name|

> Example responses

> 200 Response

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}
```

<h3 id="update-the-group-name-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[UpdateGroupResponse](#schemaupdategroupresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|<list type="number">
  <item>
    <description>- Group has already been added<br /></description>
  </item>
  <item>
    <description>- Group ID is invalid</description>
  </item>
</list>|None|

<aside class="success">
This operation does not require authentication
</aside>

## Create a group

<a id="opIdGroup_PostBycreateRequestAuthorizationPOSTGroup"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Group HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Name": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Group',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Group`

Add a group to the business. The administrator website will display fourteen (14) characters of the group name in the cardlist.<br/>
<br/>
Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the dashboard.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

> Body parameter

```json
{
  "Name": ""
}
```

<h3 id="create-a-group-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[CreateGroupRequest](#schemacreategrouprequest)|true|Group name|

> Example responses

> 200 Response

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}
```

<h3 id="create-a-group-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[CreateGroupResponse](#schemacreategroupresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Group has already been added|None|

<aside class="success">
This operation does not require authentication
</aside>

## Delete a group

<a id="opIdGroup_DeleteByidAuthorizationDELETEGroup/{id}"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Group/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Group/{id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Group/{id}`

Delete the group. If cardholders are assigned to a group that is deleted, the cardholders will no longer have a group set.<br/>
<br/>
Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the dashboard.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

<h3 id="delete-a-group-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|none|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "GroupId": 0
}
```

<h3 id="delete-a-group-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[RemoveGroupResponse](#schemaremovegroupresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Group ID is Invalid|None|

<aside class="success">
This operation does not require authentication
</aside>

## Return all cardholders in a group

<a id="opIdGroup_GetCardholdersForGroupByIdAuthorizationGETGroup/{id}"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Group/{id} HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Group/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Group/{id}`

To retrieve the GroupID, use Get /Group<br/>
<br/>
Return all cardholders assigned to a group.<br/>
<br/>
Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City. By creating and assigning cards to those groups, you can sort cards on the admin website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by group to roll up total spending for each office location.<br/>

<h3 id="return-all-cardholders-in-a-group-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int32)|true|Group ID|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
[
  {
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "AccountId": 0,
    "AccountNumber": "",
    "AvailableBalance": 0,
    "LedgerBalance": 0,
    "SpendRules": false,
    "AccountCreationTime": "",
    "ManualStatus": "",
    "SystemStatus": "",
    "PinSet": false,
    "BSAcctId": 0,
    "IsVirtual": false,
    "Group": {
      "Id": 0,
      "GroupName": ""
    },
    "SpendingRulesetModel": {
      "RulesetId": 0,
      "Name": ""
    },
    "EmbossingDetails": [
      {
        "AccountId": 0,
        "CardNumber": "",
        "ManualStatus": "",
        "SystemStatus": "",
        "CreatedDate": "",
        "PlasticDetails": [
          {
            "PlasticSequence": "",
            "ManualStatus": "",
            "IssuedDate": "",
            "ExpirationDate": ""
          }
        ]
      }
    ],
    "CustomId": ""
  }
]
```

<h3 id="return-all-cardholders-in-a-group-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

<h3 id="return-all-cardholders-in-a-group-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[CardHolderDetailsResponse](#schemacardholderdetailsresponse)]|false|none|[Card Holder Details Response]|
|» CardHolderDetailsResponse|[CardHolderDetailsResponse](#schemacardholderdetailsresponse)|false|none|Card Holder Details Response|
|»» FirstName|string|false|none|Firs tName|
|»» MiddleName|string|false|none|Middle Name|
|»» LastName|string|false|none|Last Name|
|»» AccountId|integer(int32)|false|none|Account Id|
|»» AccountNumber|string|false|none|Account Number|
|»» AvailableBalance|number(double)|false|none|Available Balance|
|»» LedgerBalance|number(double)|false|none|Ledger Balance|
|»» SpendRules|boolean|false|none|Spend Rules|
|»» AccountCreationTime|string(date-time)|false|none|Account Creation Time|
|»» ManualStatus|string|false|none|Manual Status|
|»» SystemStatus|string|false|none|System Status|
|»» PinSet|boolean|false|none|Pin Set|
|»» BSAcctId|integer(int32)|false|none|Business Account Id|
|»» IsVirtual|boolean|false|none|Identifies virtual cardholder|
|»» Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|»»» Id|integer(int32)|true|none|Unique id of the cardholder group|
|»»» GroupName|string|true|none|Name of the cardholder group|
|»» SpendingRulesetModel|[SpendingRulesetModel](#schemaspendingrulesetmodel)|false|none|Spending Ruleset Model|
|»»» RulesetId|integer(int32)|false|none|Rulese tId|
|»»» Name|string|false|none|Name|
|»» EmbossingDetails|[[EmbossingDetails](#schemaembossingdetails)]|false|none|Embossing Details|
|»»» EmbossingDetails|[EmbossingDetails](#schemaembossingdetails)|false|none|Embossing Details|
|»»»» AccountId|integer(int32)|false|none|Account Id|
|»»»» CardNumber|string|false|none|Card Number|
|»»»» ManualStatus|string|false|none|Manual Status|
|»»»» SystemStatus|string|false|none|System Status|
|»»»» CreatedDate|string(date-time)|false|none|Created Date|
|»»»» PlasticDetails|[[PlasticDetials](#schemaplasticdetials)]|false|none|Plastic Details|
|»»»»» PlasticDetials|[PlasticDetials](#schemaplasticdetials)|false|none|Plastic Detials|
|»»»»»» PlasticSequence|string|false|none|Plastic Sequence|
|»»»»»» ManualStatus|string|false|none|Manual Status|
|»»»»»» IssuedDate|string(date-time)|false|none|Issued Date|
|»»»»»» ExpirationDate|string(date-time)|false|none|Expiration Date|
|»» CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pex-api-reference-bulk-perform-bulk-operations-on-card-accounts-">Bulk : 
            Perform bulk operations on card accounts.
            </h1>

## Adjust all card available balances to $0.00 for the business

<a id="opIdBulk_ZeroByAuthorizationPOSTBulk/Zero"></a>

> Code samples

```http
POST https://coreapi.pexcard.com/v4/Bulk/Zero HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/Zero',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /Bulk/Zero`

This is an offline process to add or remove available funds from every card account for the business. The system will query all card available balances and add or remove that dollar value so that the available balance is $0.00.<br/>
<br/>
This call can take the place of individually retrieving all card balances and calling card fund for each account individually.<br/>
<br/>
If you fund the card account while this job is running, those funds will be reflected in the available balance. However, the job will not drive the account negative if funds are no longer in the account.<br/>

<h3 id="adjust-all-card-available-balances-to-$0.00-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

<h3 id="adjust-all-card-available-balances-to-$0.00-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[BulkResponse](#schemabulkresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Fund all cards for the business

<a id="opIdBulk_FundAllCardsByreqAuthorizationPUTBulk/FundAllCards"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Bulk/FundAllCards HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/FundAllCards',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Bulk/FundAllCards`

This is an offline process to add funds to all cards in the business for a specified amount.<br/>
<br/>
Cards with status Inactive, Active and Blocked will be funded. Cards with status Closed will not be funded.

> Body parameter

```json
{
  "Amount": 0
}
```

<h3 id="fund-all-cards-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[FundingRequest](#schemafundingrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

<h3 id="fund-all-cards-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[BulkResponse](#schemabulkresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid request|None|

<aside class="success">
This operation does not require authentication
</aside>

## Bulk fund on batches of cards in the business.

<a id="opIdBulk_FundMultipleCardsByreqAuthorizationPUTBulk/FundMultipleCards"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Cards": [
    {
      "AccountId": 0,
      "Amount": 0
    }
  ],
  "TransferType": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Bulk/FundMultipleCards`

<b>This endpoint is not part of our standard API offering. To access the FundMultipleCards endpoint please send an email with your request to apisupport@pexcard.com.</b>  This is a bulk process to execute balance adjustments on multiple cards in the business.<br/>
<br/>
Funding of up to 25 cards per batch are allowed.  Cards with status of Active, Inactive and Blocked will be funded. Cards with status Closed will not be funded.

> Body parameter

```json
{
  "Cards": [
    {
      "AccountId": 0,
      "Amount": 0
    }
  ],
  "TransferType": ""
}
```

<h3 id="bulk-fund-on-batches-of-cards-in-the-business.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[FundMultipleCardsRequest](#schemafundmultiplecardsrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "Success": false,
  "Results": [
    {
      "BusinessTransactionId": 0,
      "BusinessCurrentBalance": 0,
      "AccountId": 0,
      "TransactionId": 0,
      "CurrentBalance": 0,
      "ResponseCode": 0,
      "Message": ""
    }
  ],
  "Errors": [
    {
      "AccountId": 0,
      "ResponseCode": 0,
      "Message": ""
    }
  ]
}
```

<h3 id="bulk-fund-on-batches-of-cards-in-the-business.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[FundMultipleCardsResponse](#schemafundmultiplecardsresponse)|
|206|[Partial Content](https://tools.ietf.org/html/rfc7233#section-4.1)|Partial Success|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Failed Request|None|

<aside class="success">
This operation does not require authentication
</aside>

## Update scheduled funding rule for all cards in the business

<a id="opIdBulk_SetAllCardsScheduledFundingByreqAuthorizationPUTBulk/SetAllCardsScheduledFunding"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "Frequency": "",
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Bulk/SetAllCardsScheduledFunding`

Update a scheduled funding rule for all cards in the business to the Amount and Frequency values specified.<br/>
<br/>
Valid scheduled funding frequencies are:<br/>
<list type="number">
<item><description>0 - Daily<br/></description></item>
<item><description>1 - Monday<br/></description></item>
<item><description>2 - Tuesday<br/></description></item>
<item><description>3 - Wednesday<br/></description></item>
<item><description>4 - Thursday<br/></description></item>
<item><description>5 - Friday<br/></description></item>
<item><description>6 - Saturday<br/></description></item>
<item><description>7 - Sunday<br/></description></item>
<item><description>8 - First of each month<br/></description></item>
</list>

> Body parameter

```json
{
  "Frequency": "",
  "Amount": 0
}
```

<h3 id="update-scheduled-funding-rule-for-all-cards-in-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[ScheduledFundingRequest](#schemascheduledfundingrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

<h3 id="update-scheduled-funding-rule-for-all-cards-in-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[BulkResponse](#schemabulkresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid request|None|

<aside class="success">
This operation does not require authentication
</aside>

## Remove scheduled funding rule for all cards in the business

<a id="opIdBulk_RemoveAllCardsScheduledFundingByAuthorizationDELETEBulk/RemoveAllCardsScheduledFunding"></a>

> Code samples

```http
DELETE https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`DELETE /Bulk/RemoveAllCardsScheduledFunding`

Remove a scheduled funding rule for all cards in the business. Once the funding rule is deleted, the system will no longer add funds to any card balance.

<h3 id="remove-scheduled-funding-rule-for-all-cards-in-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

<h3 id="remove-scheduled-funding-rule-for-all-cards-in-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[BulkResponse](#schemabulkresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Return all spending rulesets for the business

<a id="opIdBulk_GetSpendingRulesetsByAuthorizationGETBulk/GetSpendingRulesets"></a>

> Code samples

```http
GET https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets HTTP/1.1
Host: coreapi.pexcard.com
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /Bulk/GetSpendingRulesets`

Return all spending rulesets for the business.<br/>
<br/>
A spending ruleset is a group of spend rules that can be applied to multiple card accounts. For example, if all cardholders should be allowed to spend funds at restaurants and fuel pumps, the administrator can create a spending ruleset that has only those merchant categories 'checked'. Every card with that ruleset applied can only spend at restaurants and fuel pumps.<br/>
<br/>
Spending rulesets must be created in the administration website.

<h3 id="return-all-spending-rulesets-for-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|

> Example responses

> 200 Response

```json
[
  {
    "RulesetId": 0,
    "SpendingRulesetCategories": {
      "CategoryId": 0,
      "AssociationsOrganizationsAllowed": false,
      "AutomotiveDealersAllowed": false,
      "EducationalServicesAllowed": false,
      "EntertainmentAllowed": false,
      "FuelPumpsAllowed": false,
      "GasStationsConvenienceStoresAllowed": false,
      "GroceryStoresAllowed": false,
      "HealthcareChildcareServicesAllowed": false,
      "ProfessionalServicesAllowed": false,
      "RestaurantsAllowed": false,
      "RetailStoresAllowed": false,
      "TravelTransportationAllowed": false,
      "HardwareStoresAllowed": false
    },
    "MccRestrictions": false,
    "BacctId": 0,
    "Name": "",
    "CountCardsPresent": 0,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
]
```

<h3 id="return-all-spending-rulesets-for-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

<h3 id="return-all-spending-rulesets-for-the-business-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[SpendingRuleset](#schemaspendingruleset)]|false|none|none|
|» SpendingRuleset|[SpendingRuleset](#schemaspendingruleset)|false|none|none|
|»» RulesetId|integer(int32)|false|none|none|
|»» SpendingRulesetCategories|[SpendingRulesetCategories](#schemaspendingrulesetcategories)|false|none|none|
|»»» CategoryId|integer(int32)|false|none|none|
|»»» AssociationsOrganizationsAllowed|boolean|false|none|none|
|»»» AutomotiveDealersAllowed|boolean|false|none|none|
|»»» EducationalServicesAllowed|boolean|false|none|none|
|»»» EntertainmentAllowed|boolean|false|none|none|
|»»» FuelPumpsAllowed|boolean|false|none|none|
|»»» GasStationsConvenienceStoresAllowed|boolean|false|none|none|
|»»» GroceryStoresAllowed|boolean|false|none|none|
|»»» HealthcareChildcareServicesAllowed|boolean|false|none|none|
|»»» ProfessionalServicesAllowed|boolean|false|none|none|
|»»» RestaurantsAllowed|boolean|false|none|none|
|»»» RetailStoresAllowed|boolean|false|none|none|
|»»» TravelTransportationAllowed|boolean|false|none|none|
|»»» HardwareStoresAllowed|boolean|false|none|none|
|»» MccRestrictions|boolean|false|read-only|none|
|»» BacctId|integer(int32)|false|none|none|
|»» Name|string|true|none|none|
|»» CountCardsPresent|integer(int32)|false|none|none|
|»» DailySpendLimit|number(double)|false|none|none|
|»» WeeklySpendLimit|number(double)|false|none|none|
|»» MonthlySpendLimit|number(double)|false|none|none|
|»» YearlySpendLimit|number(double)|false|none|none|
|»» LifetimeSpendLimit|number(double)|false|none|none|
|»» InternationalAllowed|boolean|false|none|none|
|»» CardNotPresentAllowed|boolean|false|none|none|
|»» UsePexAccountBalanceForAuths|boolean|false|none|none|
|»» UseCustomerAuthDecision|boolean|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Update spend rules for all cards in the business

<a id="opIdBulk_SetAllCardsSpendingRulesetByreqAuthorizationPUTBulk/SetAllCardsSpendingRuleset"></a>

> Code samples

```http
PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
const inputBody = '{
  "RulesetId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'
};

fetch('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`PUT /Bulk/SetAllCardsSpendingRuleset`

To retrieve the RulesetId, use Get /Bulk/GetSpendingRulesets and apply that RulesetId to all cards.<br/>
<br/>
Changes to spend rules happen in real-time. Be sure the cardholder is aware of the limitations being set.<br/>
<br/>
Cardholders using PEX card do not have cash access. ATMs, Money Orders, Money Remittance (e.g. MoneyGram) and other cash transactions, such as purchasing casino chips, will be declined at all times.<br/>
<br/>
Spending rulesets must be created in the administration website.

> Body parameter

```json
{
  "RulesetId": 0
}
```

<h3 id="update-spend-rules-for-all-cards-in-the-business-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string|true|token {USERTOKEN}|
|body|body|[SpendingRulesetRequest](#schemaspendingrulesetrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

<h3 id="update-spend-rules-for-all-cards-in-the-business-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[BulkResponse](#schemabulkresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid request|None|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_RenewTokenResponse">RenewTokenResponse</h2>
<!-- backwards compatibility -->
<a id="schemarenewtokenresponse"></a>
<a id="schema_RenewTokenResponse"></a>
<a id="tocSrenewtokenresponse"></a>
<a id="tocsrenewtokenresponse"></a>

```json
{
  "Username": "",
  "Token": "",
  "AppId": "",
  "TokenExpiration": ""
}

```

RenewTokenResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Username|string|true|none|Username associated with the token|
|Token|string|true|none|The new token that has been generated|
|AppId|string|true|none|AppId associated with the token|
|TokenExpiration|string(date-time)|true|none|Time token will expire|

<h2 id="tocS_GetAllTokensResponse">GetAllTokensResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetalltokensresponse"></a>
<a id="schema_GetAllTokensResponse"></a>
<a id="tocSgetalltokensresponse"></a>
<a id="tocsgetalltokensresponse"></a>

```json
{
  "Tokens": [
    {
      "Token": "",
      "SecondsUntilExpire": 0,
      "ExpirationTime": ""
    }
  ]
}

```

GetAllTokensResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Tokens|[[AccessToken](#schemaaccesstoken)]|false|none|List of three scale tokens|

<h2 id="tocS_AccessToken">AccessToken</h2>
<!-- backwards compatibility -->
<a id="schemaaccesstoken"></a>
<a id="schema_AccessToken"></a>
<a id="tocSaccesstoken"></a>
<a id="tocsaccesstoken"></a>

```json
{
  "Token": "",
  "SecondsUntilExpire": 0,
  "ExpirationTime": ""
}

```

AccessToken

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Token|string|false|none|3scale access token|
|SecondsUntilExpire|integer(int32)|false|none|Seconds until token expires|
|ExpirationTime|string(date-time)|false|none|Time token will expire|

<h2 id="tocS_GetTokenResponse">GetTokenResponse</h2>
<!-- backwards compatibility -->
<a id="schemagettokenresponse"></a>
<a id="schema_GetTokenResponse"></a>
<a id="tocSgettokenresponse"></a>
<a id="tocsgettokenresponse"></a>

```json
{
  "Tokens": [
    {
      "Username": "",
      "AppId": "",
      "Token": "",
      "TokenExpiration": ""
    }
  ]
}

```

GetTokenResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Tokens|[[TokenData](#schematokendata)]|false|none|List of three scale tokens|

<h2 id="tocS_TokenData">TokenData</h2>
<!-- backwards compatibility -->
<a id="schematokendata"></a>
<a id="schema_TokenData"></a>
<a id="tocStokendata"></a>
<a id="tocstokendata"></a>

```json
{
  "Username": "",
  "AppId": "",
  "Token": "",
  "TokenExpiration": ""
}

```

TokenData

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Username|string|true|none|Username associated with the token|
|AppId|string|true|none|AppId associated with the token|
|Token|string|true|none|3scale access token|
|TokenExpiration|string(date-time)|true|none|Time token will expire|

<h2 id="tocS_PostTokenRequest">PostTokenRequest</h2>
<!-- backwards compatibility -->
<a id="schemaposttokenrequest"></a>
<a id="schema_PostTokenRequest"></a>
<a id="tocSposttokenrequest"></a>
<a id="tocsposttokenrequest"></a>

```json
{
  "Username": "",
  "Password": ""
}

```

PostTokenRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Username|string|true|none|Admin username|
|Password|string|true|none|Admin password|

<h2 id="tocS_PostTokenResponse">PostTokenResponse</h2>
<!-- backwards compatibility -->
<a id="schemaposttokenresponse"></a>
<a id="schema_PostTokenResponse"></a>
<a id="tocSposttokenresponse"></a>
<a id="tocsposttokenresponse"></a>

```json
{
  "Token": ""
}

```

PostTokenResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Token|string|true|none|The generated token|

<h2 id="tocS_GetAdvancedSpendRulesResponse">GetAdvancedSpendRulesResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetadvancedspendrulesresponse"></a>
<a id="schema_GetAdvancedSpendRulesResponse"></a>
<a id="tocSgetadvancedspendrulesresponse"></a>
<a id="tocsgetadvancedspendrulesresponse"></a>

```json
{
  "AdvancedSpendRules": {
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ],
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}

```

GetAdvancedSpendRulesResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AdvancedSpendRules|[AdvancedSpendRulesResponse](#schemaadvancedspendrulesresponse)|true|none|Advanced Spend Rules Response|

<h2 id="tocS_AdvancedSpendRulesResponse">AdvancedSpendRulesResponse</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedspendrulesresponse"></a>
<a id="schema_AdvancedSpendRulesResponse"></a>
<a id="tocSadvancedspendrulesresponse"></a>
<a id="tocsadvancedspendrulesresponse"></a>

```json
{
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "Description": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalSpendEnabled": false,
  "IsDailySpendLimitEnabled": false,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

AdvancedSpendRulesResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|MerchantCategories|[[MerchantCategoryResponse](#schemamerchantcategoryresponse)]|false|none|List of merchant categories|
|InternationalSpendEnabled|boolean|false|none|Whether or not international spend is enabled|
|IsDailySpendLimitEnabled|boolean|false|none|Whether or not a daily spend limit is set|
|DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|WeeklySpendLimit|number(double)|false|none|Weekly spend limit, rounded to 2 decimal places|
|MonthlySpendLimit|number(double)|false|none|Monthly spend limit, rounded to 2 decimal places|
|YearlySpendLimit|number(double)|false|none|Yearly spend limit, rounded to 2 decimal places|
|LifetimeSpendLimit|number(double)|false|none|Lifetime spend limit, rounded to 2 decimal places|
|CardNotPresentUse|boolean|false|none|Whether or not card is present to use|
|UsePexAccountBalanceForAuths|boolean|false|none|Whether or not auto business balance funding to use|
|UseCustomerAuthDecision|boolean|false|none|Whether or not decision control allowed to use|

<h2 id="tocS_MerchantCategoryResponse">MerchantCategoryResponse</h2>
<!-- backwards compatibility -->
<a id="schemamerchantcategoryresponse"></a>
<a id="schema_MerchantCategoryResponse"></a>
<a id="tocSmerchantcategoryresponse"></a>
<a id="tocsmerchantcategoryresponse"></a>

```json
{
  "Id": 0,
  "Name": "",
  "Description": "",
  "TransactionLimit": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0
}

```

MerchantCategoryResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|false|none|Merchant Category Id|
|Name|string|false|none|Merchant Category Name|
|Description|string|false|none|Merchant Category Description|
|TransactionLimit|number(double)|false|none|Transaction limit, rounded to 2 decimal places|
|DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|WeeklySpendLimit|number(double)|false|none|Weekly spend limit, rounded to 2 decimal places|
|MonthlySpendLimit|number(double)|false|none|Monthly spend limit, rounded to 2 decimal places|
|YearlySpendLimit|number(double)|false|none|Yearly spend limit, rounded to 2 decimal places|
|LifetimeSpendLimit|number(double)|false|none|Lifetime spend limit, rounded to 2 decimal places|

<h2 id="tocS_SetAdvancedSpendRulesRequest">SetAdvancedSpendRulesRequest</h2>
<!-- backwards compatibility -->
<a id="schemasetadvancedspendrulesrequest"></a>
<a id="schema_SetAdvancedSpendRulesRequest"></a>
<a id="tocSsetadvancedspendrulesrequest"></a>
<a id="tocssetadvancedspendrulesrequest"></a>

```json
{
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalSpendEnabled": false,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

SetAdvancedSpendRulesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|MerchantCategories|[[MerchantCategoryRequest](#schemamerchantcategoryrequest)]|false|none|List of merchant categories|
|InternationalSpendEnabled|boolean|false|none|Whether or not international spend is enabled|
|DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|WeeklySpendLimit|number(double)|false|none|Weekly spend limit, rounded to 2 decimal places|
|MonthlySpendLimit|number(double)|false|none|Monthly spend limit, rounded to 2 decimal places|
|YearlySpendLimit|number(double)|false|none|Yearly spend limit, rounded to 2 decimal places|
|LifetimeSpendLimit|number(double)|false|none|Lifetime spend limit, rounded to 2 decimal places|
|CardNotPresentUse|boolean|false|none|Whether or not card is present to use|
|UsePexAccountBalanceForAuths|boolean|false|none|Whether or not auto business balance funding to use|
|UseCustomerAuthDecision|boolean|false|none|Whether or not decision control allowed to use|

<h2 id="tocS_MerchantCategoryRequest">MerchantCategoryRequest</h2>
<!-- backwards compatibility -->
<a id="schemamerchantcategoryrequest"></a>
<a id="schema_MerchantCategoryRequest"></a>
<a id="tocSmerchantcategoryrequest"></a>
<a id="tocsmerchantcategoryrequest"></a>

```json
{
  "Id": 0,
  "Name": "",
  "TransactionLimit": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0
}

```

MerchantCategoryRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|false|none|Merchant Category Id|
|Name|string|false|none|Merchant Category Name|
|TransactionLimit|number(double)|false|none|Transaction Limit, rounded to 2 decimal places|
|DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|WeeklySpendLimit|number(double)|false|none|Weekly spend limit, rounded to 2 decimal places|
|MonthlySpendLimit|number(double)|false|none|Monthly spend limit, rounded to 2 decimal places|
|YearlySpendLimit|number(double)|false|none|Yearly spend limit, rounded to 2 decimal places|
|LifetimeSpendLimit|number(double)|false|none|Lifetime spend limit, rounded to 2 decimal places|

<h2 id="tocS_SetCardholderPinRequest">SetCardholderPinRequest</h2>
<!-- backwards compatibility -->
<a id="schemasetcardholderpinrequest"></a>
<a id="schema_SetCardholderPinRequest"></a>
<a id="tocSsetcardholderpinrequest"></a>
<a id="tocssetcardholderpinrequest"></a>

```json
{
  "Pin": ""
}

```

SetCardholderPinRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Pin|string|true|none|4 digit PIN|

<h2 id="tocS_SetCardholderGroupRequest">SetCardholderGroupRequest</h2>
<!-- backwards compatibility -->
<a id="schemasetcardholdergrouprequest"></a>
<a id="schema_SetCardholderGroupRequest"></a>
<a id="tocSsetcardholdergrouprequest"></a>
<a id="tocssetcardholdergrouprequest"></a>

```json
{
  "GroupId": 0,
  "AcctId": 0
}

```

SetCardholderGroupRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|GroupId|integer(int32)|true|none|Group ID|
|AcctId|integer(int32)|true|none|Account ID|

<h2 id="tocS_FundResponse">FundResponse</h2>
<!-- backwards compatibility -->
<a id="schemafundresponse"></a>
<a id="schema_FundResponse"></a>
<a id="tocSfundresponse"></a>
<a id="tocsfundresponse"></a>

```json
{
  "AccountId": 0,
  "AvailableBalance": 0,
  "LedgerBalance": 0
}

```

FundResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|true|none|Unique id of the cardholder account|
|AvailableBalance|number(double)|true|none|Available balance for the card account, rounded to 2 decimal places|
|LedgerBalance|number(double)|true|none|Ledger balance for the card account, rounded to 2 decimal places|

<h2 id="tocS_CardOrderResponse">CardOrderResponse</h2>
<!-- backwards compatibility -->
<a id="schemacardorderresponse"></a>
<a id="schema_CardOrderResponse"></a>
<a id="tocScardorderresponse"></a>
<a id="tocscardorderresponse"></a>

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "BusinessAccountId": 0,
  "Cards": [
    {
      "AcctId": 0,
      "Status": "",
      "FirstName": "",
      "MiddleName": "",
      "LastName": "",
      "DateOfBirth": "",
      "HomePhone": "",
      "MobilePhone": "",
      "Email": "",
      "HomeAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "ShippingAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "Recipient": "",
      "ShipToShippingAddress": false,
      "ShippingContactNumber": "",
      "BundleCards": false,
      "ShippingMethod": "",
      "ShippingDate": "",
      "Errors": [
        {
          "Code": "",
          "Message": ""
        }
      ],
      "FailReason": "",
      "AccountNumber": "",
      "SpendingRulesetId": 0,
      "GroupId": 0,
      "CustomId": ""
    }
  ]
}

```

CardOrderResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardOrderId|integer(int32)|false|none|order id|
|OrderDateTime|string(date-time)|false|none|date and time of order|
|UserName|string|false|none|admin username|
|BusinessAccountId|integer(int32)|false|none|Business Account ID|
|Cards|[[CardHolderCardResponse](#schemacardholdercardresponse)]|false|none|Cards|

<h2 id="tocS_CardHolderCardResponse">CardHolderCardResponse</h2>
<!-- backwards compatibility -->
<a id="schemacardholdercardresponse"></a>
<a id="schema_CardHolderCardResponse"></a>
<a id="tocScardholdercardresponse"></a>
<a id="tocscardholdercardresponse"></a>

```json
{
  "AcctId": 0,
  "Status": "",
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "DateOfBirth": "",
  "HomePhone": "",
  "MobilePhone": "",
  "Email": "",
  "HomeAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Recipient": "",
  "ShipToShippingAddress": false,
  "ShippingContactNumber": "",
  "BundleCards": false,
  "ShippingMethod": "",
  "ShippingDate": "",
  "Errors": [
    {
      "Code": "",
      "Message": ""
    }
  ],
  "FailReason": "",
  "AccountNumber": "",
  "SpendingRulesetId": 0,
  "GroupId": 0,
  "CustomId": ""
}

```

CardHolderCardResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AcctId|integer(int32)|false|none|Acct ID|
|Status|string|false|none|Status|
|FirstName|string|false|none|First Name|
|MiddleName|string|false|none|Middle Name|
|LastName|string|false|none|Last Name|
|DateOfBirth|string(date-time)|false|none|Date of Birth|
|HomePhone|string|false|none|Home Phone|
|MobilePhone|string|false|none|Mobile Phone|
|Email|string|false|none|Email|
|HomeAddress|[Address](#schemaaddress)|false|none|none|
|ShippingAddress|[Address](#schemaaddress)|false|none|none|
|Recipient|string|false|none|Recipient|
|ShipToShippingAddress|boolean|false|none|Ship to Shipping Address Flag|
|ShippingContactNumber|string|false|none|Shipping Contact Number|
|BundleCards|boolean|false|none|Bundle Cards Flag|
|ShippingMethod|string|false|none|Shipping Method|
|ShippingDate|string(date-time)|false|none|Shipping Date|
|Errors|[[Error](#schemaerror)]|false|none|Error Message|
|FailReason|string|false|none|Fail reason|
|AccountNumber|string|false|none|Account Number|
|SpendingRulesetId|integer(int32)|false|none|Spending Ruleset ID|
|GroupId|integer(int32)|false|none|Group ID|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<h2 id="tocS_Address">Address</h2>
<!-- backwards compatibility -->
<a id="schemaaddress"></a>
<a id="schema_Address"></a>
<a id="tocSaddress"></a>
<a id="tocsaddress"></a>

```json
{
  "AddressLine1": "",
  "AddressLine2": "",
  "City": "",
  "State": "",
  "PostalCode": "",
  "Country": ""
}

```

Address

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AddressLine1|string|true|none|none|
|AddressLine2|string|false|none|none|
|City|string|true|none|none|
|State|string|true|none|none|
|PostalCode|string|true|none|none|
|Country|string|false|read-only|none|

<h2 id="tocS_Error">Error</h2>
<!-- backwards compatibility -->
<a id="schemaerror"></a>
<a id="schema_Error"></a>
<a id="tocSerror"></a>
<a id="tocserror"></a>

```json
{
  "Code": "",
  "Message": ""
}

```

Error

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Code|string|false|none|Error Code|
|Message|string|false|none|Error Message|

<h2 id="tocS_GetCardOrderRequest">GetCardOrderRequest</h2>
<!-- backwards compatibility -->
<a id="schemagetcardorderrequest"></a>
<a id="schema_GetCardOrderRequest"></a>
<a id="tocSgetcardorderrequest"></a>
<a id="tocsgetcardorderrequest"></a>

```json
{
  "StartDate": "",
  "EndDate": ""
}

```

GetCardOrderRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|StartDate|string(date-time)|false|none|Start date (format - YYYY-MM-DDThh:mm:ss)|
|EndDate|string(date-time)|false|none|End date (format - YYYY-MM-DDThh:mm:ss)|

<h2 id="tocS_GetCardOrderResponse">GetCardOrderResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetcardorderresponse"></a>
<a id="schema_GetCardOrderResponse"></a>
<a id="tocSgetcardorderresponse"></a>
<a id="tocsgetcardorderresponse"></a>

```json
{
  "CardOrders": [
    {
      "CardOrderId": 0,
      "OrderDateTime": "",
      "UserName": "",
      "BusinessAdminId": 0,
      "BusinessAccountId": 0,
      "NumberOfCards": 0
    }
  ]
}

```

GetCardOrderResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardOrders|[[SingleCardOrderResponse](#schemasinglecardorderresponse)]|false|none|List of card order objects|

<h2 id="tocS_SingleCardOrderResponse">SingleCardOrderResponse</h2>
<!-- backwards compatibility -->
<a id="schemasinglecardorderresponse"></a>
<a id="schema_SingleCardOrderResponse"></a>
<a id="tocSsinglecardorderresponse"></a>
<a id="tocssinglecardorderresponse"></a>

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "BusinessAdminId": 0,
  "BusinessAccountId": 0,
  "NumberOfCards": 0
}

```

SingleCardOrderResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardOrderId|integer(int32)|false|none|Card order id|
|OrderDateTime|string(date-time)|false|none|Order date|
|UserName|string|false|none|Order creator|
|BusinessAdminId|integer(int32)|false|none|Administrator id who created card order|
|BusinessAccountId|integer(int32)|false|none|Business associated with order|
|NumberOfCards|integer(int32)|false|none|Number of cards in order|

<h2 id="tocS_UpdateProfileRequest">UpdateProfileRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdateprofilerequest"></a>
<a id="schema_UpdateProfileRequest"></a>
<a id="tocSupdateprofilerequest"></a>
<a id="tocsupdateprofilerequest"></a>

```json
{
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "Phone": "",
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "CustomId": "",
  "FirstName": "",
  "LastName": "",
  "NormalizeProfileAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "NormalizeShippingAddress": false,
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  }
}

```

UpdateProfileRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardholderGroupId|integer(int32)|false|none|Unique id of the cardholder group (use 0 to remove cardholder from a group)|
|SpendRulesetId|integer(int32)|false|none|Unique id of the spending ruleset (use 0 to remove cardholder from a spending ruleset)|
|Phone|string|false|none|Phone number|
|ShippingPhone|string|false|none|Shipping Phone number|
|DateOfBirth|string(date-time)|false|none|Cardholder date of birth|
|Email|string|true|none|Cardholder email address|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|
|FirstName|string|true|none|none|
|LastName|string|true|none|none|
|NormalizeProfileAddress|boolean|false|none|none|
|ProfileAddress|[Address](#schemaaddress)|true|none|none|
|NormalizeShippingAddress|boolean|false|none|none|
|ShippingAddress|[AddressContact](#schemaaddresscontact)|false|none|none|

<h2 id="tocS_AddressContact">AddressContact</h2>
<!-- backwards compatibility -->
<a id="schemaaddresscontact"></a>
<a id="schema_AddressContact"></a>
<a id="tocSaddresscontact"></a>
<a id="tocsaddresscontact"></a>

```json
{
  "ContactName": "",
  "AddressLine1": "",
  "AddressLine2": "",
  "City": "",
  "State": "",
  "PostalCode": "",
  "Country": ""
}

```

AddressContact

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ContactName|string|false|none|none|
|AddressLine1|string|true|none|none|
|AddressLine2|string|false|none|none|
|City|string|true|none|none|
|State|string|true|none|none|
|PostalCode|string|true|none|none|
|Country|string|false|read-only|none|

<h2 id="tocS_GetProfileResponse">GetProfileResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetprofileresponse"></a>
<a id="schema_GetProfileResponse"></a>
<a id="tocSgetprofileresponse"></a>
<a id="tocsgetprofileresponse"></a>

```json
{
  "AccountId": 0,
  "AccountStatus": "",
  "FirstName": "",
  "LastName": "",
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CustomId": ""
}

```

GetProfileResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|true|none|Card account ID. 0 will be returned as the Account ID for cards that are pending|
|AccountStatus|string|true|none|Status of the account|
|FirstName|string|true|none|Cardholder first name|
|LastName|string|true|none|Cardholder last name|
|CardholderGroupId|integer(int32)|false|none|Unique id of the cardholder group|
|SpendRulesetId|integer(int32)|false|none|Unique id of the spending ruleset|
|ProfileAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|Phone|string|false|none|Phone number|
|ShippingAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|ShippingPhone|string|false|none|Shipping Phone number|
|DateOfBirth|string(date-time)|true|none|Cardholder date of birth|
|Email|string|true|none|Cardholder email address|
|IsVirtual|boolean|false|none|Identifies virtual cardholder|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<h2 id="tocS_FundRequest">FundRequest</h2>
<!-- backwards compatibility -->
<a id="schemafundrequest"></a>
<a id="schema_FundRequest"></a>
<a id="tocSfundrequest"></a>
<a id="tocsfundrequest"></a>

```json
{
  "Amount": 0
}

```

FundRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Amount|number(double)|true|none|The amount to fund the card account, rounded to 2 decimal places|

<h2 id="tocS_CreateCardAsyncRequest">CreateCardAsyncRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatecardasyncrequest"></a>
<a id="schema_CreateCardAsyncRequest"></a>
<a id="tocScreatecardasyncrequest"></a>
<a id="tocscreatecardasyncrequest"></a>

```json
{
  "Cards": [
    {
      "Phone": "",
      "ShippingPhone": "",
      "ShippingMethod": "",
      "DateOfBirth": "",
      "Email": "",
      "GroupId": 0,
      "RulesetId": 0,
      "CustomId": "",
      "FirstName": "",
      "LastName": "",
      "NormalizeProfileAddress": false,
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "NormalizeShippingAddress": false,
      "ShippingAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      }
    }
  ],
  "NormalizeHomeAddress": false,
  "NormalizeShippingAddress": false
}

```

CreateCardAsyncRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Cards|[[CreateCardRequest](#schemacreatecardrequest)]|false|none|New Card List|
|NormalizeHomeAddress|boolean|false|none|Normalize Home Address|
|NormalizeShippingAddress|boolean|false|none|Normalize Shipping Address|

<h2 id="tocS_CreateCardRequest">CreateCardRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatecardrequest"></a>
<a id="schema_CreateCardRequest"></a>
<a id="tocScreatecardrequest"></a>
<a id="tocscreatecardrequest"></a>

```json
{
  "Phone": "",
  "ShippingPhone": "",
  "ShippingMethod": "",
  "DateOfBirth": "",
  "Email": "",
  "GroupId": 0,
  "RulesetId": 0,
  "CustomId": "",
  "FirstName": "",
  "LastName": "",
  "NormalizeProfileAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "NormalizeShippingAddress": false,
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  }
}

```

CreateCardRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Phone|string|true|none|Phone number|
|ShippingPhone|string|true|none|Shipping Phone number|
|ShippingMethod|string|true|none|Method for shipping the card|
|DateOfBirth|string(date-time)|true|none|Cardholder date of birth|
|Email|string|true|none|Cardholder email address|
|GroupId|integer(int32)|false|none|Cardholder group id|
|RulesetId|integer(int32)|false|none|Cardhodler ruleset id|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|
|FirstName|string|true|none|none|
|LastName|string|true|none|none|
|NormalizeProfileAddress|boolean|false|none|none|
|ProfileAddress|[Address](#schemaaddress)|true|none|none|
|NormalizeShippingAddress|boolean|false|none|none|
|ShippingAddress|[AddressContact](#schemaaddresscontact)|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|ShippingMethod|Invalid|
|ShippingMethod|FirstClassMail|
|ShippingMethod|Expedited|
|ShippingMethod|Rush|

<h2 id="tocS_CreateCardAsyncResponse">CreateCardAsyncResponse</h2>
<!-- backwards compatibility -->
<a id="schemacreatecardasyncresponse"></a>
<a id="schema_CreateCardAsyncResponse"></a>
<a id="tocScreatecardasyncresponse"></a>
<a id="tocscreatecardasyncresponse"></a>

```json
{
  "CardOrderId": 0
}

```

CreateCardAsyncResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardOrderId|integer(int32)|false|none|Card Order ID|

<h2 id="tocS_UpdateCardStatusRequest">UpdateCardStatusRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatecardstatusrequest"></a>
<a id="schema_UpdateCardStatusRequest"></a>
<a id="tocSupdatecardstatusrequest"></a>
<a id="tocsupdatecardstatusrequest"></a>

```json
{
  "Status": ""
}

```

UpdateCardStatusRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Status|string|true|none|New status for the card.<br /><list type="enum"><item><description><i>Inactive</i>: All new Cards are Inactive, which means they can't be used to make purchases.<br /></description></item><item><description><i>Active</i>: Cards in this state can be used to make purchases when funded.<br /></description></item><item><description><i>Blocked</i>: In this state, cards cannot be used for purchases. It can be activated again for the use.<br /></description></item><item><description><i>Closed</i>: This Card account is closed. It can not be activated again for the purchase.<br /></description></item><item><description><i>Removed</i>: This Card account is removed.</description></item></list>|

#### Enumerated Values

|Property|Value|
|---|---|
|Status|Invalid|
|Status|Active|
|Status|Inactive|
|Status|Blocked|
|Status|Closed|
|Status|Removed|

<h2 id="tocS_SetSpendRulesRequest">SetSpendRulesRequest</h2>
<!-- backwards compatibility -->
<a id="schemasetspendrulesrequest"></a>
<a id="schema_SetSpendRulesRequest"></a>
<a id="tocSsetspendrulesrequest"></a>
<a id="tocssetspendrulesrequest"></a>

```json
{
  "MerchantCategories": {
    "AssociationsAndOrganizations": false,
    "AutomotiveDealers": false,
    "EducationalServices": false,
    "Entertainment": false,
    "FuelAndConvenienceStores": false,
    "GroceryStores": false,
    "HealthcareAndChildcareServices": false,
    "ProfessionalServices": false,
    "Restaurants": false,
    "RetailStores": false,
    "TravelAndTransportation": false,
    "FuelPumpOnly": false,
    "HardwareStores": false
  },
  "InternationalSpendEnabled": false,
  "DailySpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

SetSpendRulesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|MerchantCategories|[MerchantCategories](#schemamerchantcategories)|false|none|none|
|InternationalSpendEnabled|boolean|false|none|Whether or not international spend is enabled|
|DailySpendLimit|number(double)|false|none|Daily spend limit, rounded to 2 decimal places|
|CardNotPresentUse|boolean|false|none|Whether or not card is present to use|
|UsePexAccountBalanceForAuths|boolean|false|none|Whether or not auto business balance funding to use|
|UseCustomerAuthDecision|boolean|false|none|Whether or not decision control allowed to use|

<h2 id="tocS_MerchantCategories">MerchantCategories</h2>
<!-- backwards compatibility -->
<a id="schemamerchantcategories"></a>
<a id="schema_MerchantCategories"></a>
<a id="tocSmerchantcategories"></a>
<a id="tocsmerchantcategories"></a>

```json
{
  "AssociationsAndOrganizations": false,
  "AutomotiveDealers": false,
  "EducationalServices": false,
  "Entertainment": false,
  "FuelAndConvenienceStores": false,
  "GroceryStores": false,
  "HealthcareAndChildcareServices": false,
  "ProfessionalServices": false,
  "Restaurants": false,
  "RetailStores": false,
  "TravelAndTransportation": false,
  "FuelPumpOnly": false,
  "HardwareStores": false
}

```

MerchantCategories

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AssociationsAndOrganizations|boolean|false|none|none|
|AutomotiveDealers|boolean|false|none|none|
|EducationalServices|boolean|false|none|none|
|Entertainment|boolean|false|none|none|
|FuelAndConvenienceStores|boolean|false|none|none|
|GroceryStores|boolean|false|none|none|
|HealthcareAndChildcareServices|boolean|false|none|none|
|ProfessionalServices|boolean|false|none|none|
|Restaurants|boolean|false|none|none|
|RetailStores|boolean|false|none|none|
|TravelAndTransportation|boolean|false|none|none|
|FuelPumpOnly|boolean|false|none|none|
|HardwareStores|boolean|false|none|none|

<h2 id="tocS_GetSpendRulesResponse">GetSpendRulesResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetspendrulesresponse"></a>
<a id="schema_GetSpendRulesResponse"></a>
<a id="tocSgetspendrulesresponse"></a>
<a id="tocsgetspendrulesresponse"></a>

```json
{
  "SpendRules": {
    "UseMerchantCategory": false,
    "MerchantCategories": {
      "AssociationsAndOrganizations": false,
      "AutomotiveDealers": false,
      "EducationalServices": false,
      "Entertainment": false,
      "FuelAndConvenienceStores": false,
      "GroceryStores": false,
      "HealthcareAndChildcareServices": false,
      "ProfessionalServices": false,
      "Restaurants": false,
      "RetailStores": false,
      "TravelAndTransportation": false,
      "FuelPumpOnly": false,
      "HardwareStores": false
    },
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}

```

GetSpendRulesResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|SpendRules|[SpendRules](#schemaspendrules)|true|none|none|

<h2 id="tocS_SpendRules">SpendRules</h2>
<!-- backwards compatibility -->
<a id="schemaspendrules"></a>
<a id="schema_SpendRules"></a>
<a id="tocSspendrules"></a>
<a id="tocsspendrules"></a>

```json
{
  "UseMerchantCategory": false,
  "MerchantCategories": {
    "AssociationsAndOrganizations": false,
    "AutomotiveDealers": false,
    "EducationalServices": false,
    "Entertainment": false,
    "FuelAndConvenienceStores": false,
    "GroceryStores": false,
    "HealthcareAndChildcareServices": false,
    "ProfessionalServices": false,
    "Restaurants": false,
    "RetailStores": false,
    "TravelAndTransportation": false,
    "FuelPumpOnly": false,
    "HardwareStores": false
  },
  "InternationalSpendEnabled": false,
  "IsDailySpendLimitEnabled": false,
  "DailySpendLimit": 0,
  "CardNotPresentUse": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

SpendRules

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|UseMerchantCategory|boolean|false|none|none|
|MerchantCategories|[MerchantCategories](#schemamerchantcategories)|false|none|none|
|InternationalSpendEnabled|boolean|false|none|none|
|IsDailySpendLimitEnabled|boolean|false|none|none|
|DailySpendLimit|number(double)|false|none|none|
|CardNotPresentUse|boolean|false|none|none|
|UsePexAccountBalanceForAuths|boolean|false|none|none|
|UseCustomerAuthDecision|boolean|false|none|none|

<h2 id="tocS_SetScheduledFundingRulesRequest">SetScheduledFundingRulesRequest</h2>
<!-- backwards compatibility -->
<a id="schemasetscheduledfundingrulesrequest"></a>
<a id="schema_SetScheduledFundingRulesRequest"></a>
<a id="tocSsetscheduledfundingrulesrequest"></a>
<a id="tocssetscheduledfundingrulesrequest"></a>

```json
{
  "Amount": 0,
  "Frequency": ""
}

```

SetScheduledFundingRulesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Amount|number(double)|false|none|Amount of the scheduled funding, rounded to 2 decimal places|
|Frequency|string|true|none|Describes when the scheduled funding should occur|

#### Enumerated Values

|Property|Value|
|---|---|
|Frequency|DAY|
|Frequency|MONDAY|
|Frequency|TUESDAY|
|Frequency|WEDNESDAY|
|Frequency|THURSDAY|
|Frequency|FRIDAY|
|Frequency|SATURDAY|
|Frequency|SUNDAY|
|Frequency|FIRSTOFMONTH|

<h2 id="tocS_GetScheduledFundingRulesResponse">GetScheduledFundingRulesResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetscheduledfundingrulesresponse"></a>
<a id="schema_GetScheduledFundingRulesResponse"></a>
<a id="tocSgetscheduledfundingrulesresponse"></a>
<a id="tocsgetscheduledfundingrulesresponse"></a>

```json
{
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": ""
  }
}

```

GetScheduledFundingRulesResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ScheduledFunding|[ScheduledFunding](#schemascheduledfunding)|false|none|Details about scheduled funding|

<h2 id="tocS_ScheduledFunding">ScheduledFunding</h2>
<!-- backwards compatibility -->
<a id="schemascheduledfunding"></a>
<a id="schema_ScheduledFunding"></a>
<a id="tocSscheduledfunding"></a>
<a id="tocsscheduledfunding"></a>

```json
{
  "Amount": 0,
  "Frequency": ""
}

```

ScheduledFunding

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Amount|number(double)|true|none|Amount of scheduled funding, rounded to 2 decimal places|
|Frequency|string|true|none|Describes when scheduled funding should occur.<br /><br>            Possible string values for Frequency parameter of scheduled funding are: <br /><list type="enum"><item><description> - '0' or 'DAY' - every Day<br /></description></item><item><description> - '1' or 'MONDAY' - every Monday<br /></description></item><item><description> - '2' or 'TUESDAY' - every Tuesday<br /></description></item><item><description> - '3' or 'WEDNESDAY' - every Wednesday<br /></description></item><item><description> - '4' or 'THURSDAY' - every Thursday<br /></description></item><item><description> - '5' or 'FRIDAY' - every Friday<br /></description></item><item><description> - '6' or 'SATURDAY' - every Saturday<br /></description></item><item><description> - '7' or 'SUNDAY' - every Sunday<br /></description></item><item><description> - '8' or 'FIRSTOFMONTH' - every 1st of the Month<br /></description></item></list>|

#### Enumerated Values

|Property|Value|
|---|---|
|Frequency|DAY|
|Frequency|MONDAY|
|Frequency|TUESDAY|
|Frequency|WEDNESDAY|
|Frequency|THURSDAY|
|Frequency|FRIDAY|
|Frequency|SATURDAY|
|Frequency|SUNDAY|
|Frequency|FIRSTOFMONTH|

<h2 id="tocS_SetCardholderRulesetRequest">SetCardholderRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemasetcardholderrulesetrequest"></a>
<a id="schema_SetCardholderRulesetRequest"></a>
<a id="tocSsetcardholderrulesetrequest"></a>
<a id="tocssetcardholderrulesetrequest"></a>

```json
{
  "RulesetId": 0,
  "AccountId": 0
}

```

SetCardholderRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|true|none|Spending Ruleset ID|
|AccountId|integer(int32)|true|none|Account ID|

<h2 id="tocS_CardholderSpendRulesetResponse">CardholderSpendRulesetResponse</h2>
<!-- backwards compatibility -->
<a id="schemacardholderspendrulesetresponse"></a>
<a id="schema_CardholderSpendRulesetResponse"></a>
<a id="tocScardholderspendrulesetresponse"></a>
<a id="tocscardholderspendrulesetresponse"></a>

```json
{
  "AccountId": 0
}

```

CardholderSpendRulesetResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|false|none|Account ID|

<h2 id="tocS_GetAdvancedAccountDetailsResponse">GetAdvancedAccountDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetadvancedaccountdetailsresponse"></a>
<a id="schema_GetAdvancedAccountDetailsResponse"></a>
<a id="tocSgetadvancedaccountdetailsresponse"></a>
<a id="tocsgetadvancedaccountdetailsresponse"></a>

```json
{
  "AccountId": 0,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "AccountStatus": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CardList": [
    {
      "CardId": 0,
      "IssuedDate": "",
      "ExpirationDate": "",
      "Last4CardNumber": "",
      "CardStatus": ""
    }
  ],
  "SpendingRulesetId": 0,
  "SpendRules": {
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ],
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  },
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": ""
  },
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  },
  "CustomId": ""
}

```

GetAdvancedAccountDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|false|none|Unique cardholder account id|
|Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|AccountStatus|string|false|none|Cardholder account status (OPEN or CLOSED)|
|LedgerBalance|number(double)|false|none|Ledger balance for the card account, rounded to 2 decimal places|
|AvailableBalance|number(double)|false|none|Available balance for the card account, rounded to 2 decimal places|
|ProfileAddress|[AddressContact](#schemaaddresscontact)|false|none|none|
|Phone|string|false|none|Phone number|
|ShippingAddress|[AddressContact](#schemaaddresscontact)|false|none|none|
|ShippingPhone|string|false|none|Shipping Phone number|
|DateOfBirth|string(date-time)|false|none|Cardholder date of birth|
|Email|string|false|none|Cardholder email address|
|IsVirtual|boolean|false|none|Identifies virtual cardholder|
|CardList|[[CardDetail](#schemacarddetail)]|false|none|List of details about cards associated with the account|
|SpendingRulesetId|integer(int32)|false|none|SpendingRulesetId for the cardholder account|
|SpendRules|[AdvancedSpendRulesResponse](#schemaadvancedspendrulesresponse)|false|none|Advanced Spend Rules Response|
|ScheduledFunding|[ScheduledFunding](#schemascheduledfunding)|false|none|Details about scheduled funding|
|LowBalanceFunding|[LowBalanceFunding](#schemalowbalancefunding)|false|none|Details about low balance funding|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<h2 id="tocS_CardholderGroup">CardholderGroup</h2>
<!-- backwards compatibility -->
<a id="schemacardholdergroup"></a>
<a id="schema_CardholderGroup"></a>
<a id="tocScardholdergroup"></a>
<a id="tocscardholdergroup"></a>

```json
{
  "Id": 0,
  "GroupName": ""
}

```

CardholderGroup

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|true|none|Unique id of the cardholder group|
|GroupName|string|true|none|Name of the cardholder group|

<h2 id="tocS_CardDetail">CardDetail</h2>
<!-- backwards compatibility -->
<a id="schemacarddetail"></a>
<a id="schema_CardDetail"></a>
<a id="tocScarddetail"></a>
<a id="tocscarddetail"></a>

```json
{
  "CardId": 0,
  "IssuedDate": "",
  "ExpirationDate": "",
  "Last4CardNumber": "",
  "CardStatus": ""
}

```

CardDetail

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardId|integer(int32)|true|none|Unique id for the card|
|IssuedDate|string(date-time)|true|none|Date card was issued|
|ExpirationDate|string(date-time)|true|none|Expiration date for the card|
|Last4CardNumber|string|true|none|Last four digits of card number|
|CardStatus|string|true|none|Card status<br /><br>            Possible string values for CardStatus parameter of card detail are: <br /><list type="enum"><item><description> - <i>Inactive</i>: All new Cards are Inactive, which means they can't be used to make purchases.<br /></description></item><item><description> - <i>Active</i>: Cards in this state can be used to make purchases when funded.<br /></description></item><item><description> - <i>Blocked</i>: In this state, cards cannot be used for purchases. It can be activated again for the use.<br /></description></item><item><description> - <i>Closed</i>: This Card account is closed. It can not be activated again for the purchase.<br /></description></item></list>|

<h2 id="tocS_LowBalanceFunding">LowBalanceFunding</h2>
<!-- backwards compatibility -->
<a id="schemalowbalancefunding"></a>
<a id="schema_LowBalanceFunding"></a>
<a id="tocSlowbalancefunding"></a>
<a id="tocslowbalancefunding"></a>

```json
{
  "ThresholdAmount": 0,
  "AmountToFund": 0
}

```

LowBalanceFunding

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ThresholdAmount|number(double)|true|none|Threshold, rounded to 2 decimal places, to determine when funding should occur|
|AmountToFund|number(double)|true|none|Amount, rounded to 2 decimal places, to fund when threshold is hit|

<h2 id="tocS_AccountRemainingLimitsResponse">AccountRemainingLimitsResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaccountremaininglimitsresponse"></a>
<a id="schema_AccountRemainingLimitsResponse"></a>
<a id="tocSaccountremaininglimitsresponse"></a>
<a id="tocsaccountremaininglimitsresponse"></a>

```json
{
  "AccountId": 0,
  "GlobalLimits": [
    {
      "Type": "",
      "EnforcedLimit": 0,
      "RemainingSpend": 0
    }
  ],
  "MerchantCategoryLimits": [
    {
      "MerchantCategoryId": 0,
      "Category": "",
      "Type": "",
      "EnforcedLimit": 0,
      "RemainingSpend": 0
    }
  ]
}

```

AccountRemainingLimitsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|false|none|Account Id|
|GlobalLimits|[[GlobalLimit](#schemagloballimit)]|false|none|Global limits|
|MerchantCategoryLimits|[[MerchantCategoryLimit](#schemamerchantcategorylimit)]|false|none|Merchant category limits|

<h2 id="tocS_GlobalLimit">GlobalLimit</h2>
<!-- backwards compatibility -->
<a id="schemagloballimit"></a>
<a id="schema_GlobalLimit"></a>
<a id="tocSgloballimit"></a>
<a id="tocsgloballimit"></a>

```json
{
  "Type": "",
  "EnforcedLimit": 0,
  "RemainingSpend": 0
}

```

GlobalLimit

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Type|string|false|none|Period type|
|EnforcedLimit|number(double)|false|none|Enforced spend limit|
|RemainingSpend|number(double)|false|none|Remaining spend|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|PerDay|
|Type|PerWeek|
|Type|PerMonth|
|Type|PerYear|
|Type|Lifetime|

<h2 id="tocS_MerchantCategoryLimit">MerchantCategoryLimit</h2>
<!-- backwards compatibility -->
<a id="schemamerchantcategorylimit"></a>
<a id="schema_MerchantCategoryLimit"></a>
<a id="tocSmerchantcategorylimit"></a>
<a id="tocsmerchantcategorylimit"></a>

```json
{
  "MerchantCategoryId": 0,
  "Category": "",
  "Type": "",
  "EnforcedLimit": 0,
  "RemainingSpend": 0
}

```

MerchantCategoryLimit

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|MerchantCategoryId|integer(int32)|false|none|Category Id|
|Category|string|false|none|Name of category|
|Type|string|false|none|Period type|
|EnforcedLimit|number(double)|false|none|Enforced rule limit|
|RemainingSpend|number(double)|false|none|Remaining spending|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|PerDay|
|Type|PerWeek|
|Type|PerMonth|
|Type|PerYear|
|Type|Lifetime|

<h2 id="tocS_DateRange">DateRange</h2>
<!-- backwards compatibility -->
<a id="schemadaterange"></a>
<a id="schema_DateRange"></a>
<a id="tocSdaterange"></a>
<a id="tocsdaterange"></a>

```json
{
  "StartDate": "",
  "EndDate": ""
}

```

DateRange

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|StartDate|string(date-time)|true|none|YYYY-MM-DDThh:mm:ss|
|EndDate|string(date-time)|true|none|YYYY-MM-DDThh:mm:ss|

<h2 id="tocS_NetworkTransactionDetailsResponse">NetworkTransactionDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schemanetworktransactiondetailsresponse"></a>
<a id="schema_NetworkTransactionDetailsResponse"></a>
<a id="tocSnetworktransactiondetailsresponse"></a>
<a id="tocsnetworktransactiondetailsresponse"></a>

```json
{
  "TransactionList": [
    {
      "NetworkTransactionId": 0,
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "MerchantLocalTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "AvailableBalance": 0,
      "LedgerBalance": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "ReferencedTranId": 0,
      "ReferencedTransactionTime": "",
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkType": "",
      "NetworkStatus": "",
      "IsCardPresent": false,
      "Message": "",
      "MessageCode": "",
      "MerchantRequestedAmount": 0
    }
  ]
}

```

NetworkTransactionDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TransactionList|[[NetworkTransaction](#schemanetworktransaction)]|true|none|The list of netword transaction details|

<h2 id="tocS_NetworkTransaction">NetworkTransaction</h2>
<!-- backwards compatibility -->
<a id="schemanetworktransaction"></a>
<a id="schema_NetworkTransaction"></a>
<a id="tocSnetworktransaction"></a>
<a id="tocsnetworktransaction"></a>

```json
{
  "NetworkTransactionId": 0,
  "TransactionId": 0,
  "AcctId": 0,
  "TransactionTime": "",
  "HoldTime": "",
  "SettlementTime": "",
  "MerchantLocalTime": "",
  "AuthTransactionId": 0,
  "TransactionAmount": 0,
  "PaddingAmount": 0,
  "AvailableBalance": 0,
  "LedgerBalance": 0,
  "TransactionType": "",
  "Description": "",
  "TransactionNotes": [
    {
      "NoteId": 0,
      "UserName": "",
      "NoteText": "",
      "NoteDate": ""
    }
  ],
  "ReferencedTranId": 0,
  "ReferencedTransactionTime": "",
  "MerchantName": "",
  "MerchantCity": "",
  "MerchantState": "",
  "MerchantZip": "",
  "MerchantCountry": "",
  "MCCCode": "",
  "AuthIdentityResponseCode": "",
  "MerchantId": "",
  "TerminalId": "",
  "NetworkType": "",
  "NetworkStatus": "",
  "IsCardPresent": false,
  "Message": "",
  "MessageCode": "",
  "MerchantRequestedAmount": 0
}

```

NetworkTransaction

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|NetworkTransactionId|integer(int64)|false|none|ID of network transaction|
|TransactionId|integer(int64)|false|none|ID of transaction|
|AcctId|integer(int32)|false|none|Account ID|
|TransactionTime|string(date-time)|false|none|Transaction time|
|HoldTime|string(date-time)|false|none|Hold time|
|SettlementTime|string(date-time)|false|none|Settlement time|
|MerchantLocalTime|string(date-time)|false|none|Merchant local time|
|AuthTransactionId|integer(int64)|false|none|ID of auth transaction|
|TransactionAmount|number(double)|false|none|Transaction amount|
|PaddingAmount|number(double)|false|none|Padding amount|
|AvailableBalance|number(double)|false|none|Available balance|
|LedgerBalance|number(double)|false|none|Ledger balance|
|TransactionType|string|false|none|Transaction type|
|Description|string|false|none|Description|
|TransactionNotes|[[TransactionNote](#schematransactionnote)]|false|none|List of transaction notes|
|ReferencedTranId|integer(int64)|false|none|ID of referenced transaction|
|ReferencedTransactionTime|string(date-time)|false|none|Referenced transaction time|
|MerchantName|string|false|none|Merchant name|
|MerchantCity|string|false|none|Merchant city|
|MerchantState|string|false|none|Merchant state|
|MerchantZip|string|false|none|Merchant zip|
|MerchantCountry|string|false|none|Merchant country|
|MCCCode|string|false|none|Merchant category code|
|AuthIdentityResponseCode|string|false|none|Auth identityRresponse code|
|MerchantId|string|false|none|ID of merchant|
|TerminalId|string|false|none|ID of terminal|
|NetworkType|string|false|none|Network type|
|NetworkStatus|string|false|none|Network status|
|IsCardPresent|boolean|false|none|Is card present flag|
|Message|string|false|none|Message|
|MessageCode|string|false|none|Message code|
|MerchantRequestedAmount|number(double)|false|none|Merchant Requested Amount|

<h2 id="tocS_TransactionNote">TransactionNote</h2>
<!-- backwards compatibility -->
<a id="schematransactionnote"></a>
<a id="schema_TransactionNote"></a>
<a id="tocStransactionnote"></a>
<a id="tocstransactionnote"></a>

```json
{
  "NoteId": 0,
  "UserName": "",
  "NoteText": "",
  "NoteDate": ""
}

```

TransactionNote

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|NoteId|integer(int64)|true|none|Unique id for the note|
|UserName|string|true|none|Admin username who wrote the note|
|NoteText|string|true|none|Text of the note|
|NoteDate|string(date-time)|true|none|Time the note was added|

<h2 id="tocS_BusinessDetailsResponse">BusinessDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schemabusinessdetailsresponse"></a>
<a id="schema_BusinessDetailsResponse"></a>
<a id="tocSbusinessdetailsresponse"></a>
<a id="tocsbusinessdetailsresponse"></a>

```json
{
  "BusinessAccountId": 0,
  "BusinessName": "",
  "BusinessAccountStatus": "",
  "BusinessAccountBalance": 0,
  "PendingTransferAmount": 0,
  "BankAccountList": [
    {
      "ExternalBankAcctId": 0,
      "RoutingNumber": "",
      "BankAccountNumber": "",
      "BankName": "",
      "BankAccountType": "",
      "IsActive": false
    }
  ],
  "CHAccountList": [
    {
      "AccountId": 0,
      "FirstName": "",
      "LastName": "",
      "LedgerBalance": 0,
      "AvailableBalance": 0,
      "AccountStatus": "",
      "IsVirtual": false,
      "CustomId": ""
    }
  ],
  "CardholderGroups": [
    {
      "Id": 0,
      "Name": ""
    }
  ]
}

```

BusinessDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|BusinessAccountId|integer(int32)|true|none|Unique account id for the business|
|BusinessName|string|true|none|Name of the business|
|BusinessAccountStatus|string|true|none|Business account status (OPEN or CLOSED)|
|BusinessAccountBalance|number(double)|true|none|Account balance for the business, rounded to 2 decimal places|
|PendingTransferAmount|number(double)|true|none|Amount of pending transfers, rounded to 2 decimal places|
|BankAccountList|[[ExternalBankAccount](#schemaexternalbankaccount)]|true|none|List of external bank accounts associated with the business|
|CHAccountList|[[BusinessCHAccountDetail](#schemabusinesschaccountdetail)]|true|none|List of cardholder account details for the business|
|CardholderGroups|[[CardHolderGroup](#schemacardholdergroup)]|true|none|a list of groups that the Business can use|

<h2 id="tocS_ExternalBankAccount">ExternalBankAccount</h2>
<!-- backwards compatibility -->
<a id="schemaexternalbankaccount"></a>
<a id="schema_ExternalBankAccount"></a>
<a id="tocSexternalbankaccount"></a>
<a id="tocsexternalbankaccount"></a>

```json
{
  "ExternalBankAcctId": 0,
  "RoutingNumber": "",
  "BankAccountNumber": "",
  "BankName": "",
  "BankAccountType": "",
  "IsActive": false
}

```

ExternalBankAccount

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ExternalBankAcctId|integer(int32)|true|none|Unique external bank account id|
|RoutingNumber|string|true|none|Routing number|
|BankAccountNumber|string|true|none|Last 4 digits of bank account number|
|BankName|string|true|none|Bank name|
|BankAccountType|string|true|none|Type of account (ACH or Wire)|
|IsActive|boolean|true|none|Whether or not the bank account is active|

<h2 id="tocS_BusinessCHAccountDetail">BusinessCHAccountDetail</h2>
<!-- backwards compatibility -->
<a id="schemabusinesschaccountdetail"></a>
<a id="schema_BusinessCHAccountDetail"></a>
<a id="tocSbusinesschaccountdetail"></a>
<a id="tocsbusinesschaccountdetail"></a>

```json
{
  "AccountId": 0,
  "FirstName": "",
  "LastName": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "AccountStatus": "",
  "IsVirtual": false,
  "CustomId": ""
}

```

BusinessCHAccountDetail

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|true|none|Unique id for the cardholder account|
|FirstName|string|true|none|Cardholder first name|
|LastName|string|true|none|Cardholder last name|
|LedgerBalance|number(double)|true|none|Ledger balance for the cardholder account, rounded to 2 decimal places|
|AvailableBalance|number(double)|true|none|Available balance for the cardholder account, rounded to 2 decimal places|
|AccountStatus|string|true|none|Cardholder account status (OPEN or CLOSED)|
|IsVirtual|boolean|false|none|Identifies virtual cardholder|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<h2 id="tocS_CardHolderGroup">CardHolderGroup</h2>
<!-- backwards compatibility -->
<a id="schemacardholdergroup"></a>
<a id="schema_CardHolderGroup"></a>
<a id="tocScardholdergroup"></a>
<a id="tocscardholdergroup"></a>

```json
{
  "Id": 0,
  "Name": ""
}

```

CardHolderGroup

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|false|none|group Id|
|Name|string|false|none|group Name|

<h2 id="tocS_CardholderDetailsResponse">CardholderDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schemacardholderdetailsresponse"></a>
<a id="schema_CardholderDetailsResponse"></a>
<a id="tocScardholderdetailsresponse"></a>
<a id="tocscardholderdetailsresponse"></a>

```json
{
  "AccountId": 0,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "AccountStatus": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CardList": [
    {
      "CardId": 0,
      "IssuedDate": "",
      "ExpirationDate": "",
      "Last4CardNumber": "",
      "CardStatus": ""
    }
  ],
  "SpendingRulesetId": 0,
  "SpendRules": {
    "UseMerchantCategory": false,
    "MerchantCategories": {
      "AssociationsAndOrganizations": false,
      "AutomotiveDealers": false,
      "EducationalServices": false,
      "Entertainment": false,
      "FuelAndConvenienceStores": false,
      "GroceryStores": false,
      "HealthcareAndChildcareServices": false,
      "ProfessionalServices": false,
      "Restaurants": false,
      "RetailStores": false,
      "TravelAndTransportation": false,
      "FuelPumpOnly": false,
      "HardwareStores": false
    },
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  },
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": ""
  },
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  },
  "CustomId": ""
}

```

CardholderDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|true|none|Unique cardholder account id|
|Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|AccountStatus|string|true|none|Cardholder account status (OPEN or CLOSED)|
|LedgerBalance|number(double)|true|none|Ledger balance for the card account, rounded to 2 decimal places|
|AvailableBalance|number(double)|true|none|Available balance for the card account, rounded to 2 decimal places|
|ProfileAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|Phone|string|false|none|Phone number|
|ShippingAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|ShippingPhone|string|false|none|Shipping Phone number|
|DateOfBirth|string(date-time)|true|none|Cardholder date of birth|
|Email|string|true|none|Cardholder email address|
|IsVirtual|boolean|false|none|Identifies virtual cardholder|
|CardList|[[CardDetail](#schemacarddetail)]|true|none|List of details about cards associated with the account|
|SpendingRulesetId|integer(int32)|true|none|SpendingRulesetId for the cardholder account|
|SpendRules|[SpendRules](#schemaspendrules)|true|none|none|
|ScheduledFunding|[ScheduledFunding](#schemascheduledfunding)|false|none|Details about scheduled funding|
|LowBalanceFunding|[LowBalanceFunding](#schemalowbalancefunding)|false|none|Details about low balance funding|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<h2 id="tocS_TransactionDetailsRequest">TransactionDetailsRequest</h2>
<!-- backwards compatibility -->
<a id="schematransactiondetailsrequest"></a>
<a id="schema_TransactionDetailsRequest"></a>
<a id="tocStransactiondetailsrequest"></a>
<a id="tocstransactiondetailsrequest"></a>

```json
{
  "IncludePendings": false,
  "IncludeDeclines": false,
  "StartDate": "",
  "EndDate": ""
}

```

TransactionDetailsRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|IncludePendings|boolean|false|none|1 to include pending transactions and 0 to exclude|
|IncludeDeclines|boolean|false|none|1 to include decline transactions and 0 to exclude|
|StartDate|string(date-time)|true|none|YYYY-MM-DDThh:mm:ss|
|EndDate|string(date-time)|true|none|YYYY-MM-DDThh:mm:ss|

<h2 id="tocS_TransactionDetailsResponse">TransactionDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schematransactiondetailsresponse"></a>
<a id="schema_TransactionDetailsResponse"></a>
<a id="tocStransactiondetailsresponse"></a>
<a id="tocstransactiondetailsresponse"></a>

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": "",
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}

```

TransactionDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TransactionList|[[Transaction](#schematransaction)]|true|none|The list of transaction details|
|Pages|[PageInfo](#schemapageinfo)|true|none|Pagination information used for operations returning a large result set|

<h2 id="tocS_Transaction">Transaction</h2>
<!-- backwards compatibility -->
<a id="schematransaction"></a>
<a id="schema_Transaction"></a>
<a id="tocStransaction"></a>
<a id="tocstransaction"></a>

```json
{
  "TransactionId": 0,
  "AcctId": 0,
  "TransactionTime": "",
  "MerchantLocalTime": "",
  "HoldTime": "",
  "SettlementTime": "",
  "AuthTransactionId": 0,
  "TransactionAmount": 0,
  "PaddingAmount": 0,
  "TransactionType": "",
  "Description": "",
  "TransactionNotes": [
    {
      "NoteId": 0,
      "UserName": "",
      "NoteText": "",
      "NoteDate": ""
    }
  ],
  "IsPending": false,
  "IsDecline": false,
  "MerchantName": "",
  "MerchantCity": "",
  "MerchantState": "",
  "MerchantZip": "",
  "MerchantCountry": "",
  "MCCCode": "",
  "TransferToOrFromAccountId": 0,
  "AuthIdentityResponseCode": "",
  "MerchantId": "",
  "TerminalId": "",
  "NetworkTransactionId": 0,
  "SourceCurrencyCodeDescription": "",
  "SourceCurrencyNumericCode": "",
  "SourceAmount": 0,
  "TransactionTags": {
    "Tags": [
      {
        "FieldId": "",
        "Value": {},
        "Name": ""
      }
    ],
    "State": "",
    "FieldsVersion": ""
  },
  "MetadataApprovalStatus": "",
  "TransactionTypeCategory": ""
}

```

Transaction

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TransactionId|integer(int64)|true|none|Unique Id for the transaction|
|AcctId|integer(int32)|true|none|Unique cardholder account id|
|TransactionTime|string(date-time)|true|none|Time the transaction entered the system|
|MerchantLocalTime|string(date-time)|false|none|Merchant local time the transaction took place|
|HoldTime|string(date-time)|false|none|Time the hold authorization entered the system|
|SettlementTime|string(date-time)|false|none|Settlement time, if applicable|
|AuthTransactionId|integer(int64)|true|none|The transaction Id of the authorization if the transaction is a settlement|
|TransactionAmount|number(double)|true|none|Amount of the transaction, rounded to 2 decimal places|
|PaddingAmount|number(double)|true|none|Padding amount, rounded to 2 decimal places|
|TransactionType|string|true|none|Type of transaction|
|Description|string|true|none|Transaction description|
|TransactionNotes|[[TransactionNote](#schematransactionnote)]|false|none|List of transaction notes|
|IsPending|boolean|true|none|Whether or not the transaction is pending|
|IsDecline|boolean|true|none|Whether or not the transaction is a decline|
|MerchantName|string|true|none|Merchant name|
|MerchantCity|string|true|none|Merchant city|
|MerchantState|string|true|none|Merchant state|
|MerchantZip|string|true|none|Merchant zip|
|MerchantCountry|string|true|none|Merchant country|
|MCCCode|string|true|none|MCC Code|
|TransferToOrFromAccountId|integer(int32)|false|none|Id of the account the transaction is going to or coming from, if applicable|
|AuthIdentityResponseCode|string|false|none|Authorization Identification Response code from Star data element 38 in Auth Response message|
|MerchantId|string|false|none|The number a financial institution assigns to a merchant to identify your business|
|TerminalId|string|false|none|TerminalId|
|NetworkTransactionId|integer(int64)|false|none|The transaction Id of the network authorization if the transaction is a settlement|
|SourceCurrencyCodeDescription|string|false|none|Source Currency Code Description|
|SourceCurrencyNumericCode|string|false|none|The three-digit numeric code assigned to each currency as defined in ISO 4217 standard.|
|SourceAmount|number(double)|false|none|Source Amount|
|TransactionTags|[TransactionTags](#schematransactiontags)|false|none|Transaction Tags Entity|
|MetadataApprovalStatus|string|false|none|Metadata Approval Status|
|TransactionTypeCategory|string|false|none|Transaction Type Category|

#### Enumerated Values

|Property|Value|
|---|---|
|TransactionType|Transfer|
|TransactionType|Network|
|TransactionType|Load|
|TransactionType|Invalid|

<h2 id="tocS_PageInfo">PageInfo</h2>
<!-- backwards compatibility -->
<a id="schemapageinfo"></a>
<a id="schema_PageInfo"></a>
<a id="tocSpageinfo"></a>
<a id="tocspageinfo"></a>

```json
{
  "PageSize": 0,
  "TotalRecords": 0,
  "NumberOfPages": 0,
  "LastTimeRetrieved": ""
}

```

PageInfo

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|PageSize|integer(int32)|true|none|Number of records per page|
|TotalRecords|integer(int32)|true|none|Total number of records returned by query|
|NumberOfPages|integer(int32)|true|none|Number of pages returned by query|
|LastTimeRetrieved|string(date-time)|true|none|Last transaction time received on the current page|

<h2 id="tocS_TransactionTags">TransactionTags</h2>
<!-- backwards compatibility -->
<a id="schematransactiontags"></a>
<a id="schema_TransactionTags"></a>
<a id="tocStransactiontags"></a>
<a id="tocstransactiontags"></a>

```json
{
  "Tags": [
    {
      "FieldId": "",
      "Value": {},
      "Name": ""
    }
  ],
  "State": "",
  "FieldsVersion": ""
}

```

TransactionTags

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Tags|[[TransactionTag](#schematransactiontag)]|false|none|Transaction Tags|
|State|string|false|none|State|
|FieldsVersion|string|false|none|Fields Version|

#### Enumerated Values

|Property|Value|
|---|---|
|State|Initial|
|State|Selected|

<h2 id="tocS_TransactionTag">TransactionTag</h2>
<!-- backwards compatibility -->
<a id="schematransactiontag"></a>
<a id="schema_TransactionTag"></a>
<a id="tocStransactiontag"></a>
<a id="tocstransactiontag"></a>

```json
{
  "FieldId": "",
  "Value": {},
  "Name": ""
}

```

TransactionTag

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FieldId|string|false|none|Field ID|
|Value|object|false|none|Field Value|
|Name|string|false|none|Field Name|

<h2 id="tocS_GetAttachments">GetAttachments</h2>
<!-- backwards compatibility -->
<a id="schemagetattachments"></a>
<a id="schema_GetAttachments"></a>
<a id="tocSgetattachments"></a>
<a id="tocsgetattachments"></a>

```json
{
  "Attachments": [
    {
      "AttachmentId": "",
      "Type": "",
      "Size": 0,
      "Link": {
        "related": ""
      },
      "UploadStatus": "",
      "CreatedDateUtc": "",
      "CreatedBy": {
        "AdminId": 0,
        "UserId": 0
      },
      "UpdatedDateUtc": "",
      "UpdatedBy": {
        "AdminId": 0,
        "UserId": 0
      }
    }
  ],
  "ApprovalStatus": ""
}

```

GetAttachments

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Attachments|[[AttachmentWithRelatedLink](#schemaattachmentwithrelatedlink)]|false|none|Attachments|
|ApprovalStatus|string|false|none|Approval status is on the transaction level and not only for attachment.<br>           If the transaction is approved, all related data i.e Attachments, Tags etc are approved.|

#### Enumerated Values

|Property|Value|
|---|---|
|ApprovalStatus|NotReviewed|
|ApprovalStatus|Ignored|
|ApprovalStatus|Approved|
|ApprovalStatus|Rejected|
|ApprovalStatus|NoReceipt|

<h2 id="tocS_AttachmentWithRelatedLink">AttachmentWithRelatedLink</h2>
<!-- backwards compatibility -->
<a id="schemaattachmentwithrelatedlink"></a>
<a id="schema_AttachmentWithRelatedLink"></a>
<a id="tocSattachmentwithrelatedlink"></a>
<a id="tocsattachmentwithrelatedlink"></a>

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "Link": {
    "related": ""
  },
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}

```

AttachmentWithRelatedLink

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AttachmentId|string|false|none|Unique identifier of the attachment.|
|Type|string|false|none|Specifies the type of attachment Image/PDF|
|Size|integer(int64)|false|none|Size of the attachment.|
|Link|[LinkRelated](#schemalinkrelated)|false|none|Link|
|UploadStatus|string|false|none|the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.|
|CreatedDateUtc|string(date-time)|false|none|Created date in UTC|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Updated date in UTC|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Image|
|Type|Pdf|
|UploadStatus|NotLoaded|
|UploadStatus|Loaded|
|UploadStatus|Deleted|
|UploadStatus|HasMalware|
|UploadStatus|LoadFailed|

<h2 id="tocS_LinkRelated">LinkRelated</h2>
<!-- backwards compatibility -->
<a id="schemalinkrelated"></a>
<a id="schema_LinkRelated"></a>
<a id="tocSlinkrelated"></a>
<a id="tocslinkrelated"></a>

```json
{
  "related": ""
}

```

LinkRelated

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|related|string|false|none|The Link property provides a link to /AttachmentId resource which contains the encoded image details.|

<h2 id="tocS_MetadataUser">MetadataUser</h2>
<!-- backwards compatibility -->
<a id="schemametadatauser"></a>
<a id="schema_MetadataUser"></a>
<a id="tocSmetadatauser"></a>
<a id="tocsmetadatauser"></a>

```json
{
  "AdminId": 0,
  "UserId": 0
}

```

MetadataUser

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AdminId|integer(int32)|false|none|Admin Id of the user who created, updated, or deleted the tag definition|
|UserId|integer(int32)|false|none|User Id of the user who created, updated, or deleted the tag definition|

<h2 id="tocS_DeleteAttachment">DeleteAttachment</h2>
<!-- backwards compatibility -->
<a id="schemadeleteattachment"></a>
<a id="schema_DeleteAttachment"></a>
<a id="tocSdeleteattachment"></a>
<a id="tocsdeleteattachment"></a>

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}

```

DeleteAttachment

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AttachmentId|string|false|none|Unique identifier of the attachment.|
|Type|string|false|none|Specifies the type of attachment Image/PDF|
|Size|integer(int64)|false|none|Size of the attachment.|
|UploadStatus|string|false|none|the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.|
|CreatedDateUtc|string(date-time)|false|none|Created date in UTC|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Updated date in UTC|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|DeletedDateUtc|string(date-time)|false|none|Deleted date in UTC|
|DeletedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Image|
|Type|Pdf|
|UploadStatus|NotLoaded|
|UploadStatus|Loaded|
|UploadStatus|Deleted|
|UploadStatus|HasMalware|
|UploadStatus|LoadFailed|

<h2 id="tocS_Attachment">Attachment</h2>
<!-- backwards compatibility -->
<a id="schemaattachment"></a>
<a id="schema_Attachment"></a>
<a id="tocSattachment"></a>
<a id="tocsattachment"></a>

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "Content": "",
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "ApprovalStatus": ""
}

```

Attachment

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AttachmentId|string|false|none|Unique identifier of the attachment.|
|Type|string|false|none|Specifies the type of attachment Image/PDF|
|Size|integer(int64)|false|none|Size of the attachment.|
|Content|string|false|none|BASE64_ENCODED_DATA|
|UploadStatus|string|false|none|the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.|
|CreatedDateUtc|string(date-time)|false|none|Created date in UTC|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Updated date in UTC|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|ApprovalStatus|string|false|none|Approval status is on the transaction level and not only for attachment.<br>           If the transaction is approved, all related data i.e Attachments, Tags etc are approved.|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Image|
|Type|Pdf|
|UploadStatus|NotLoaded|
|UploadStatus|Loaded|
|UploadStatus|Deleted|
|UploadStatus|HasMalware|
|UploadStatus|LoadFailed|
|ApprovalStatus|NotReviewed|
|ApprovalStatus|Ignored|
|ApprovalStatus|Approved|
|ApprovalStatus|Rejected|
|ApprovalStatus|NoReceipt|

<h2 id="tocS_CreateOrUpdateAttachmentRequest">CreateOrUpdateAttachmentRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreateorupdateattachmentrequest"></a>
<a id="schema_CreateOrUpdateAttachmentRequest"></a>
<a id="tocScreateorupdateattachmentrequest"></a>
<a id="tocscreateorupdateattachmentrequest"></a>

```json
{
  "Content": "",
  "Type": ""
}

```

CreateOrUpdateAttachmentRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Content|string|true|none|BASE64_ENCODED_DATA|
|Type|string|false|none|Specifies the type of attachment Image/PDF|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Image|
|Type|Pdf|

<h2 id="tocS_AttachmentWithSelfLink">AttachmentWithSelfLink</h2>
<!-- backwards compatibility -->
<a id="schemaattachmentwithselflink"></a>
<a id="schema_AttachmentWithSelfLink"></a>
<a id="tocSattachmentwithselflink"></a>
<a id="tocsattachmentwithselflink"></a>

```json
{
  "AttachmentId": "",
  "Type": "",
  "Size": 0,
  "Link": {
    "self": ""
  },
  "UploadStatus": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}

```

AttachmentWithSelfLink

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AttachmentId|string|false|none|Unique identifier of the attachment.|
|Type|string|false|none|Specifies the type of attachment Image/PDF|
|Size|integer(int64)|false|none|Size of the attachment.|
|Link|[LinkSelf](#schemalinkself)|false|none|Self Link|
|UploadStatus|string|false|none|the system assigned status of the attachment valid values are:  Not Loaded, Loaded, Deleted, HasMalware, LoadFailed.|
|CreatedDateUtc|string(date-time)|false|none|Created date in UTC|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Updated date in UTC|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Image|
|Type|Pdf|
|UploadStatus|NotLoaded|
|UploadStatus|Loaded|
|UploadStatus|Deleted|
|UploadStatus|HasMalware|
|UploadStatus|LoadFailed|

<h2 id="tocS_LinkSelf">LinkSelf</h2>
<!-- backwards compatibility -->
<a id="schemalinkself"></a>
<a id="schema_LinkSelf"></a>
<a id="tocSlinkself"></a>
<a id="tocslinkself"></a>

```json
{
  "self": ""
}

```

LinkSelf

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|self|string|false|none|The Link property provides a link to /AttachmentId resource which contains the encoded image details.|

<h2 id="tocS_Tags">Tags</h2>
<!-- backwards compatibility -->
<a id="schematags"></a>
<a id="schema_Tags"></a>
<a id="tocStags"></a>
<a id="tocstags"></a>

```json
{
  "Id": "",
  "ConcurrencyKey": "",
  "State": "",
  "Values": {},
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}

```

Tags

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|string|false|none|Unique identifier for tag values|
|ConcurrencyKey|string|false|none|Prevent conflicts when multiple users update tag values at the same time|
|State|string|false|none|Tag review state|
|Values|object|false|none|Values|
|CreatedDateUtc|string(date-time)|false|none|Created date in UTC|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Updated date in UTC|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|State|NotReviewed|
|State|Ignored|
|State|Alphabetic|
|State|Alphanumeric|

<h2 id="tocS_CreateTagValuesRequest">CreateTagValuesRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatetagvaluesrequest"></a>
<a id="schema_CreateTagValuesRequest"></a>
<a id="tocScreatetagvaluesrequest"></a>
<a id="tocscreatetagvaluesrequest"></a>

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Value": {}
    }
  ]
}

```

CreateTagValuesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|Values|[[TagValueItem](#schematagvalueitem)]|false|none|Tag values|

<h2 id="tocS_TagValueItem">TagValueItem</h2>
<!-- backwards compatibility -->
<a id="schematagvalueitem"></a>
<a id="schema_TagValueItem"></a>
<a id="tocStagvalueitem"></a>
<a id="tocstagvalueitem"></a>

```json
{
  "TagId": "",
  "Value": {}
}

```

TagValueItem

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TagId|string|false|none|Tag definition Id|
|Value|object|false|none|Value|

<h2 id="tocS_UpdateTagValuesRequest">UpdateTagValuesRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatetagvaluesrequest"></a>
<a id="schema_UpdateTagValuesRequest"></a>
<a id="tocSupdatetagvaluesrequest"></a>
<a id="tocsupdatetagvaluesrequest"></a>

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Value": {}
    }
  ]
}

```

UpdateTagValuesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|Values|[[TagValueItem](#schematagvalueitem)]|false|none|Tag values|

<h2 id="tocS_CreateAllocationTagValuesRequest">CreateAllocationTagValuesRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreateallocationtagvaluesrequest"></a>
<a id="schema_CreateAllocationTagValuesRequest"></a>
<a id="tocScreateallocationtagvaluesrequest"></a>
<a id="tocscreateallocationtagvaluesrequest"></a>

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Allocation": [
        {
          "TagId": "",
          "Value": {}
        }
      ],
      "Amount": 0
    }
  ]
}

```

CreateAllocationTagValuesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|Values|[[AllocationTagValue](#schemaallocationtagvalue)]|false|none|Allocation tag values|

<h2 id="tocS_AllocationTagValue">AllocationTagValue</h2>
<!-- backwards compatibility -->
<a id="schemaallocationtagvalue"></a>
<a id="schema_AllocationTagValue"></a>
<a id="tocSallocationtagvalue"></a>
<a id="tocsallocationtagvalue"></a>

```json
{
  "TagId": "",
  "Allocation": [
    {
      "TagId": "",
      "Value": {}
    }
  ],
  "Amount": 0
}

```

AllocationTagValue

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TagId|string|false|none|Tag definition Id|
|Allocation|[[TagValueItem](#schematagvalueitem)]|false|none|Value|
|Amount|number(double)|false|none|Amount|

<h2 id="tocS_UpdateAllocationTagValuesRequest">UpdateAllocationTagValuesRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdateallocationtagvaluesrequest"></a>
<a id="schema_UpdateAllocationTagValuesRequest"></a>
<a id="tocSupdateallocationtagvaluesrequest"></a>
<a id="tocsupdateallocationtagvaluesrequest"></a>

```json
{
  "ConcurrencyKey": "",
  "Values": [
    {
      "TagId": "",
      "Allocation": [
        {
          "TagId": "",
          "Value": {}
        }
      ],
      "Amount": 0
    }
  ]
}

```

UpdateAllocationTagValuesRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|Values|[[AllocationTagValue](#schemaallocationtagvalue)]|false|none|Allocation tag values|

<h2 id="tocS_VirtualCardsOrderRequest">VirtualCardsOrderRequest</h2>
<!-- backwards compatibility -->
<a id="schemavirtualcardsorderrequest"></a>
<a id="schema_VirtualCardsOrderRequest"></a>
<a id="tocSvirtualcardsorderrequest"></a>
<a id="tocsvirtualcardsorderrequest"></a>

```json
{
  "VirtualCards": [
    {
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "GroupId": 0,
      "RulesetId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": ""
    }
  ]
}

```

VirtualCardsOrderRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|VirtualCards|[[VirtualCardCreationRequest](#schemavirtualcardcreationrequest)]|true|none|Virtual Cards requests|

<h2 id="tocS_VirtualCardCreationRequest">VirtualCardCreationRequest</h2>
<!-- backwards compatibility -->
<a id="schemavirtualcardcreationrequest"></a>
<a id="schema_VirtualCardCreationRequest"></a>
<a id="tocSvirtualcardcreationrequest"></a>
<a id="tocsvirtualcardcreationrequest"></a>

```json
{
  "FirstName": "",
  "LastName": "",
  "DateOfBirth": "",
  "Phone": "",
  "Email": "",
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "GroupId": 0,
  "RulesetId": 0,
  "AutoActivation": false,
  "FundCardAmount": 0,
  "CardDataWebhookURL": ""
}

```

VirtualCardCreationRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FirstName|string|true|none|First Name|
|LastName|string|true|none|Last Name|
|DateOfBirth|string(date-time)|true|none|Cardholder date of birth|
|Phone|string|true|none|Phone number|
|Email|string|true|none|Cardholder email address|
|ProfileAddress|[Address](#schemaaddress)|false|none|none|
|GroupId|integer(int32)|false|none|Cardholder group id|
|RulesetId|integer(int32)|false|none|Cardhodler ruleset id|
|AutoActivation|boolean|false|none|Auto Activation true/false|
|FundCardAmount|number(double)|false|none|Fund Card Amount|
|CardDataWebhookURL|string|true|none|Card Data Webhook URL|

<h2 id="tocS_VirtualCardsOrderResponse">VirtualCardsOrderResponse</h2>
<!-- backwards compatibility -->
<a id="schemavirtualcardsorderresponse"></a>
<a id="schema_VirtualCardsOrderResponse"></a>
<a id="tocSvirtualcardsorderresponse"></a>
<a id="tocsvirtualcardsorderresponse"></a>

```json
{
  "VirtualCardOrderId": 0,
  "NumberOfCardsRequested": 0
}

```

VirtualCardsOrderResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|VirtualCardOrderId|integer(int32)|false|none|Virtual Card Order Id|
|NumberOfCardsRequested|integer(int32)|false|none|Number Of Cards Requested|

<h2 id="tocS_VirtualCardsGetOrderResponse">VirtualCardsGetOrderResponse</h2>
<!-- backwards compatibility -->
<a id="schemavirtualcardsgetorderresponse"></a>
<a id="schema_VirtualCardsGetOrderResponse"></a>
<a id="tocSvirtualcardsgetorderresponse"></a>
<a id="tocsvirtualcardsgetorderresponse"></a>

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "Cards": [
    {
      "RequestId": 0,
      "AcctId": 0,
      "AccountNumber": "",
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "HomeAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "GroupId": 0,
      "SpendingRulesetsId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": "",
      "Status": "",
      "Errors": [
        "string"
      ],
      "ErrorMessage": ""
    }
  ]
}

```

VirtualCardsGetOrderResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CardOrderId|integer(int32)|false|none|VC Order Id|
|OrderDateTime|string(date-time)|false|none|Order DateTime|
|UserName|string|false|none|User Name|
|Cards|[[VirtualCardGetOrderResponse](#schemavirtualcardgetorderresponse)]|false|none|Virtual Cards|

<h2 id="tocS_VirtualCardGetOrderResponse">VirtualCardGetOrderResponse</h2>
<!-- backwards compatibility -->
<a id="schemavirtualcardgetorderresponse"></a>
<a id="schema_VirtualCardGetOrderResponse"></a>
<a id="tocSvirtualcardgetorderresponse"></a>
<a id="tocsvirtualcardgetorderresponse"></a>

```json
{
  "RequestId": 0,
  "AcctId": 0,
  "AccountNumber": "",
  "FirstName": "",
  "LastName": "",
  "DateOfBirth": "",
  "Phone": "",
  "Email": "",
  "HomeAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "GroupId": 0,
  "SpendingRulesetsId": 0,
  "AutoActivation": false,
  "FundCardAmount": 0,
  "CardDataWebhookURL": "",
  "Status": "",
  "Errors": [
    "string"
  ],
  "ErrorMessage": ""
}

```

VirtualCardGetOrderResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RequestId|integer(int32)|false|none|Request Id|
|AcctId|integer(int32)|false|none|Account Id|
|AccountNumber|string|false|none|Account Number|
|FirstName|string|false|none|First Name|
|LastName|string|false|none|Last Name|
|DateOfBirth|string(date-time)|false|none|Date Of Birth|
|Phone|string|false|none|Phone|
|Email|string|false|none|Email|
|HomeAddress|[Address](#schemaaddress)|false|none|none|
|GroupId|integer(int32)|false|none|Group Id|
|SpendingRulesetsId|integer(int32)|false|none|Spending Rulesets Id|
|AutoActivation|boolean|false|none|Auto Activation|
|FundCardAmount|number(double)|false|none|Fund Card Amount|
|CardDataWebhookURL|string|false|none|Card Data Webhook URL|
|Status|string|false|none|Status|
|Errors|[string]|false|none|Errors|
|ErrorMessage|string|false|none|Error Message|

<h2 id="tocS_VirtualCardDataRequest">VirtualCardDataRequest</h2>
<!-- backwards compatibility -->
<a id="schemavirtualcarddatarequest"></a>
<a id="schema_VirtualCardDataRequest"></a>
<a id="tocSvirtualcarddatarequest"></a>
<a id="tocsvirtualcarddatarequest"></a>

```json
{
  "AcctId": 0,
  "CardDataWebhookURL": ""
}

```

VirtualCardDataRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AcctId|integer(int32)|false|none|Cardholder Account Id|
|CardDataWebhookURL|string|true|none|Card Data Webhook URL|

<h2 id="tocS_Tag">Tag</h2>
<!-- backwards compatibility -->
<a id="schematag"></a>
<a id="schema_Tag"></a>
<a id="tocStag"></a>
<a id="tocstag"></a>

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}

```

Tag

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|string|false|none|Unique Identifier of the tag definition|
|Type|string|false|none|Type of the tag definition {Dropdown, Text, Decimal, Yes/No}|
|Name|string|false|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|IsEnabled|boolean|false|none|This flag determines if the tag definition is visible to the card holder|
|IsDeleted|boolean|false|none|If set to true, the tag is deleted|
|IsRequired|boolean|false|none|If set to true, tag is not required|
|Order|integer(int32)|false|none|Determines the position where tag appears. It is a 0 based index|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|CreatedDateUtc|string(date-time)|false|none|Date when the tag definition was created|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Date when the tag definition was last updated|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|DeletedDateUtc|string(date-time)|false|none|Date when the tag definition was deleted|
|DeletedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Text|
|Type|YesNo|
|Type|Dropdown|
|Type|Decimal|
|Type|Allocation|

<h2 id="tocS_UpdateDropdownTagRequest">UpdateDropdownTagRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatedropdowntagrequest"></a>
<a id="schema_UpdateDropdownTagRequest"></a>
<a id="tocSupdatedropdowntagrequest"></a>
<a id="tocsupdatedropdowntagrequest"></a>

```json
{
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ],
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}

```

UpdateDropdownTagRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Options|[[TagOptionRequest](#schematagoptionrequest)]|true|none|Options|
|Name|string|true|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|Order|integer(int32)|true|none|Determines the position where tag appears. It is a 0 based index|
|IsRequired|boolean|true|none|If set to true, tag is not required|
|IsEnabled|boolean|true|none|This flag determines if the tag definition is visible to the card holder|

<h2 id="tocS_TagOptionRequest">TagOptionRequest</h2>
<!-- backwards compatibility -->
<a id="schematagoptionrequest"></a>
<a id="schema_TagOptionRequest"></a>
<a id="tocStagoptionrequest"></a>
<a id="tocstagoptionrequest"></a>

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}

```

TagOptionRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Name of the option ("Display as" on PEX Admin site) for Type = Dropdown|
|Value|string|true|none|Value of an option ("Option Value" on PEX Admin site) for Type = Dropdown|
|Order|integer(int32)|false|none|Determines the position where tag option appears. It is a 0 based index|
|IsEnabled|boolean|false|none|This flag determines if the tag option is visible to the card holder for selection|

<h2 id="tocS_DropdownTag">DropdownTag</h2>
<!-- backwards compatibility -->
<a id="schemadropdowntag"></a>
<a id="schema_DropdownTag"></a>
<a id="tocSdropdowntag"></a>
<a id="tocsdropdowntag"></a>

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}

```

DropdownTag

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|string|false|none|Unique Identifier of the tag definition|
|Type|string|false|none|Type of the tag definition {Dropdown, Text, Decimal, Yes/No}|
|Name|string|false|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|IsEnabled|boolean|false|none|This flag determines if the tag definition is visible to the card holder|
|IsDeleted|boolean|false|none|If set to true, the tag is deleted|
|IsRequired|boolean|false|none|If set to true, tag is not required|
|Order|integer(int32)|false|none|Determines the position where tag appears. It is a 0 based index|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|CreatedDateUtc|string(date-time)|false|none|Date when the tag definition was created|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Date when the tag definition was last updated|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|DeletedDateUtc|string(date-time)|false|none|Date when the tag definition was deleted|
|DeletedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|Options|[[ITagOption](#schemaitagoption)]|false|none|Dropdown tag options|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Text|
|Type|YesNo|
|Type|Dropdown|
|Type|Decimal|
|Type|Allocation|

<h2 id="tocS_ITagOption">ITagOption</h2>
<!-- backwards compatibility -->
<a id="schemaitagoption"></a>
<a id="schema_ITagOption"></a>
<a id="tocSitagoption"></a>
<a id="tocsitagoption"></a>

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}

```

ITagOption

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|false|none|Name of the option ("Display as" on PEX Admin site) for Type = Dropdown|
|Value|string|false|none|Value of an option ("Option Value" on PEX Admin site) for Type = Dropdown|
|Order|integer(int32)|false|none|Determines the position where tag option appears. It is a 0 based index|
|IsEnabled|boolean|false|none|This flag determines if the tag option is visible to the card holder for selection|

<h2 id="tocS_CreateDropdownTagRequest">CreateDropdownTagRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatedropdowntagrequest"></a>
<a id="schema_CreateDropdownTagRequest"></a>
<a id="tocScreatedropdowntagrequest"></a>
<a id="tocscreatedropdowntagrequest"></a>

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false,
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}

```

CreateDropdownTagRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|Order|integer(int32)|true|none|Determines the position where tag appears. It is a 0 based index|
|IsRequired|boolean|true|none|If set to true, tag is not required|
|IsEnabled|boolean|true|none|This flag determines if the tag definition is visible to the card holder|
|Options|[[CreateTagOptionRequest](#schemacreatetagoptionrequest)]|true|none|Dropdown tag options|

<h2 id="tocS_CreateTagOptionRequest">CreateTagOptionRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatetagoptionrequest"></a>
<a id="schema_CreateTagOptionRequest"></a>
<a id="tocScreatetagoptionrequest"></a>
<a id="tocscreatetagoptionrequest"></a>

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}

```

CreateTagOptionRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Name of the option ("Display as" on PEX Admin site) for Type = Dropdown|
|Value|string|true|none|Value of an option ("Option Value" on PEX Admin site) for Type = Dropdown|
|Order|integer(int32)|false|none|Determines the position where tag option appears. It is a 0 based index|
|IsEnabled|boolean|false|none|This flag determines if the tag option is visible to the card holder for selection|

<h2 id="tocS_TagOptionsRequest">TagOptionsRequest</h2>
<!-- backwards compatibility -->
<a id="schematagoptionsrequest"></a>
<a id="schema_TagOptionsRequest"></a>
<a id="tocStagoptionsrequest"></a>
<a id="tocstagoptionsrequest"></a>

```json
{
  "Options": [
    {
      "Name": "",
      "Value": "",
      "Order": 0,
      "IsEnabled": false
    }
  ]
}

```

TagOptionsRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Options|[[TagOptionRequest](#schematagoptionrequest)]|true|none|Options|

<h2 id="tocS_CreateTextTagRequest">CreateTextTagRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatetexttagrequest"></a>
<a id="schema_CreateTextTagRequest"></a>
<a id="tocScreatetexttagrequest"></a>
<a id="tocscreatetexttagrequest"></a>

```json
{
  "Length": 0,
  "ValidationType": "",
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}

```

CreateTextTagRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Length|integer(int32)|true|none|Length|
|ValidationType|string|false|none|Validation type|
|Name|string|true|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|Order|integer(int32)|true|none|Determines the position where tag appears. It is a 0 based index|
|IsRequired|boolean|true|none|If set to true, tag is not required|
|IsEnabled|boolean|true|none|This flag determines if the tag definition is visible to the card holder|

#### Enumerated Values

|Property|Value|
|---|---|
|ValidationType|None|
|ValidationType|Numeric|
|ValidationType|Alphabetic|
|ValidationType|Alphanumeric|

<h2 id="tocS_TextTag">TextTag</h2>
<!-- backwards compatibility -->
<a id="schematexttag"></a>
<a id="schema_TextTag"></a>
<a id="tocStexttag"></a>
<a id="tocstexttag"></a>

```json
{
  "Length": 0,
  "ValidationType": "",
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  }
}

```

TextTag

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Length|integer(int32)|false|none|Defines the number of characters allowed for this tag. Length takes numeric values E.g. 5 means the tag can have up to 5 characters. By default 200 char is max length|
|ValidationType|string|false|none|Determines the kind of values this tag definition is allowed to have. Valid values are None, Numeric, Alphabetic, and Alphanumeric|
|Id|string|false|none|Unique Identifier of the tag definition|
|Type|string|false|none|Type of the tag definition {Dropdown, Text, Decimal, Yes/No}|
|Name|string|false|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|IsEnabled|boolean|false|none|This flag determines if the tag definition is visible to the card holder|
|IsDeleted|boolean|false|none|If set to true, the tag is deleted|
|IsRequired|boolean|false|none|If set to true, tag is not required|
|Order|integer(int32)|false|none|Determines the position where tag appears. It is a 0 based index|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|CreatedDateUtc|string(date-time)|false|none|Date when the tag definition was created|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Date when the tag definition was last updated|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|DeletedDateUtc|string(date-time)|false|none|Date when the tag definition was deleted|
|DeletedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|

#### Enumerated Values

|Property|Value|
|---|---|
|ValidationType|None|
|ValidationType|Numeric|
|ValidationType|Alphabetic|
|ValidationType|Alphanumeric|
|Type|Text|
|Type|YesNo|
|Type|Dropdown|
|Type|Decimal|
|Type|Allocation|

<h2 id="tocS_UpdateTextTagRequest">UpdateTextTagRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatetexttagrequest"></a>
<a id="schema_UpdateTextTagRequest"></a>
<a id="tocSupdatetexttagrequest"></a>
<a id="tocsupdatetexttagrequest"></a>

```json
{
  "Length": 0,
  "ValidationType": "",
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}

```

UpdateTextTagRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Length|integer(int32)|true|none|Length|
|ValidationType|string|false|none|Validation type|
|Name|string|true|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|Order|integer(int32)|true|none|Determines the position where tag appears. It is a 0 based index|
|IsRequired|boolean|true|none|If set to true, tag is not required|
|IsEnabled|boolean|true|none|This flag determines if the tag definition is visible to the card holder|

#### Enumerated Values

|Property|Value|
|---|---|
|ValidationType|None|
|ValidationType|Numeric|
|ValidationType|Alphabetic|
|ValidationType|Alphanumeric|

<h2 id="tocS_CreateTagRequest">CreateTagRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatetagrequest"></a>
<a id="schema_CreateTagRequest"></a>
<a id="tocScreatetagrequest"></a>
<a id="tocscreatetagrequest"></a>

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}

```

CreateTagRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|Order|integer(int32)|true|none|Determines the position where tag appears. It is a 0 based index|
|IsRequired|boolean|true|none|If set to true, tag is not required|
|IsEnabled|boolean|true|none|This flag determines if the tag definition is visible to the card holder|

<h2 id="tocS_UpdateTagRequest">UpdateTagRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatetagrequest"></a>
<a id="schema_UpdateTagRequest"></a>
<a id="tocSupdatetagrequest"></a>
<a id="tocsupdatetagrequest"></a>

```json
{
  "Name": "",
  "Description": "",
  "Order": 0,
  "IsRequired": false,
  "IsEnabled": false
}

```

UpdateTagRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|Order|integer(int32)|true|none|Determines the position where tag appears. It is a 0 based index|
|IsRequired|boolean|true|none|If set to true, tag is not required|
|IsEnabled|boolean|true|none|This flag determines if the tag definition is visible to the card holder|

<h2 id="tocS_AllocationTag">AllocationTag</h2>
<!-- backwards compatibility -->
<a id="schemaallocationtag"></a>
<a id="schema_AllocationTag"></a>
<a id="tocSallocationtag"></a>
<a id="tocsallocationtag"></a>

```json
{
  "Id": "",
  "Type": "",
  "Name": "",
  "Description": "",
  "IsEnabled": false,
  "IsDeleted": false,
  "IsRequired": false,
  "Order": 0,
  "ConcurrencyKey": "",
  "CreatedDateUtc": "",
  "CreatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "UpdatedDateUtc": "",
  "UpdatedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "DeletedDateUtc": "",
  "DeletedBy": {
    "AdminId": 0,
    "UserId": 0
  },
  "Tags": [
    {
      "TagId": "",
      "Order": ""
    }
  ]
}

```

AllocationTag

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|string|false|none|Unique Identifier of the tag definition|
|Type|string|false|none|Type of the tag definition {Dropdown, Text, Decimal, Yes/No}|
|Name|string|false|none|Name of the tag definition|
|Description|string|false|none|Descriptive information about the tag definition|
|IsEnabled|boolean|false|none|This flag determines if the tag definition is visible to the card holder|
|IsDeleted|boolean|false|none|If set to true, the tag is deleted|
|IsRequired|boolean|false|none|If set to true, tag is not required|
|Order|integer(int32)|false|none|Determines the position where tag appears. It is a 0 based index|
|ConcurrencyKey|string|false|none|Concurrent editing token|
|CreatedDateUtc|string(date-time)|false|none|Date when the tag definition was created|
|CreatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|UpdatedDateUtc|string(date-time)|false|none|Date when the tag definition was last updated|
|UpdatedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|DeletedDateUtc|string(date-time)|false|none|Date when the tag definition was deleted|
|DeletedBy|[MetadataUser](#schemametadatauser)|false|none|Metadata user|
|Tags|[[IAllocationTagItem](#schemaiallocationtagitem)]|false|none|Tag definitions collection|

#### Enumerated Values

|Property|Value|
|---|---|
|Type|Text|
|Type|YesNo|
|Type|Dropdown|
|Type|Decimal|
|Type|Allocation|

<h2 id="tocS_IAllocationTagItem">IAllocationTagItem</h2>
<!-- backwards compatibility -->
<a id="schemaiallocationtagitem"></a>
<a id="schema_IAllocationTagItem"></a>
<a id="tocSiallocationtagitem"></a>
<a id="tocsiallocationtagitem"></a>

```json
{
  "TagId": "",
  "Order": ""
}

```

IAllocationTagItem

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TagId|string|false|none|Allocation item tag id|
|Order|string|false|none|Allocation item tag order|

<h2 id="tocS_UpdateTagOptionRequest">UpdateTagOptionRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatetagoptionrequest"></a>
<a id="schema_UpdateTagOptionRequest"></a>
<a id="tocSupdatetagoptionrequest"></a>
<a id="tocsupdatetagoptionrequest"></a>

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}

```

UpdateTagOptionRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Name of the option ("Display as" on PEX Admin site) for Type = Dropdown|
|Value|string|true|none|Value of an option ("Option Value" on PEX Admin site) for Type = Dropdown|
|Order|integer(int32)|false|none|Determines the position where tag option appears. It is a 0 based index|
|IsEnabled|boolean|false|none|This flag determines if the tag option is visible to the card holder for selection|

<h2 id="tocS_TagOption">TagOption</h2>
<!-- backwards compatibility -->
<a id="schematagoption"></a>
<a id="schema_TagOption"></a>
<a id="tocStagoption"></a>
<a id="tocstagoption"></a>

```json
{
  "Name": "",
  "Value": "",
  "Order": 0,
  "IsEnabled": false
}

```

TagOption

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|false|none|Name of the option ("Display as" on PEX Admin site) for Type = Dropdown|
|Value|string|false|none|Value of an option ("Option Value" on PEX Admin site) for Type = Dropdown|
|Order|integer(int32)|false|none|Determines the position where tag option appears. It is a 0 based index|
|IsEnabled|boolean|false|none|This flag determines if the tag option is visible to the card holder for selection|

<h2 id="tocS_GetOneTimeTransferResponse">GetOneTimeTransferResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetonetimetransferresponse"></a>
<a id="schema_GetOneTimeTransferResponse"></a>
<a id="tocSgetonetimetransferresponse"></a>
<a id="tocsgetonetimetransferresponse"></a>

```json
{
  "OneTimeTransferDetails": [
    {
      "TransferRequestId": 0,
      "BankInformation": {
        "ExternalBankAcctId": 0,
        "RoutingNumber": "",
        "BankAccountNumber": "",
        "BankName": "",
        "BankAccountType": "",
        "IsActive": false
      },
      "Amount": 0,
      "Status": "",
      "RequestedDate": "",
      "FundAvailableDate": ""
    }
  ]
}

```

GetOneTimeTransferResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|OneTimeTransferDetails|[[OneTimeTransferDetail](#schemaonetimetransferdetail)]|true|none|List of one time transfer details|

<h2 id="tocS_OneTimeTransferDetail">OneTimeTransferDetail</h2>
<!-- backwards compatibility -->
<a id="schemaonetimetransferdetail"></a>
<a id="schema_OneTimeTransferDetail"></a>
<a id="tocSonetimetransferdetail"></a>
<a id="tocsonetimetransferdetail"></a>

```json
{
  "TransferRequestId": 0,
  "BankInformation": {
    "ExternalBankAcctId": 0,
    "RoutingNumber": "",
    "BankAccountNumber": "",
    "BankName": "",
    "BankAccountType": "",
    "IsActive": false
  },
  "Amount": 0,
  "Status": "",
  "RequestedDate": "",
  "FundAvailableDate": ""
}

```

OneTimeTransferDetail

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TransferRequestId|integer(int32)|true|none|Unique one time transfer request id|
|BankInformation|[ExternalBankAccount](#schemaexternalbankaccount)|true|none|External bank account details|
|Amount|number(double)|true|none|Amount of the transfer, rounded to 2 decimal places  (positive = DEBIT, negative = CREDIT.|
|Status|string|true|none|Status of one time transfer request|
|RequestedDate|string(date-time)|true|none|Date one time transfer request was made|
|FundAvailableDate|string(date-time)|true|none|Date funds will be available|

<h2 id="tocS_UpdateBusinessProfileRequest">UpdateBusinessProfileRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatebusinessprofilerequest"></a>
<a id="schema_UpdateBusinessProfileRequest"></a>
<a id="tocSupdatebusinessprofilerequest"></a>
<a id="tocsupdatebusinessprofilerequest"></a>

```json
{
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "NormalizeAddress": false
}

```

UpdateBusinessProfileRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ProfileAddress|[Address](#schemaaddress)|true|none|none|
|Phone|string|false|none|Phone number|
|PhoneExtension|string|false|none|Phone Extension|
|NormalizeAddress|boolean|false|none|Normalize address flag|

<h2 id="tocS_GetBusinessProfileResponse">GetBusinessProfileResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetbusinessprofileresponse"></a>
<a id="schema_GetBusinessProfileResponse"></a>
<a id="tocSgetbusinessprofileresponse"></a>
<a id="tocsgetbusinessprofileresponse"></a>

```json
{
  "BusinessAcctId": 0,
  "FirstName": "",
  "LastName": "",
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "DateOfBirth": "",
  "Email": ""
}

```

GetBusinessProfileResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|BusinessAcctId|integer(int32)|true|none|Business account id|
|FirstName|string|true|none|Business contact first name|
|LastName|string|true|none|Business contact last name|
|ProfileAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|Phone|string|false|none|Phone number|
|PhoneExtension|string|false|none|Phone Extension|
|DateOfBirth|string(date-time)|true|none|Business contact date of birth|
|Email|string|true|none|Business contact email address|

<h2 id="tocS_EditAdminRequest">EditAdminRequest</h2>
<!-- backwards compatibility -->
<a id="schemaeditadminrequest"></a>
<a id="schema_EditAdminRequest"></a>
<a id="tocSeditadminrequest"></a>
<a id="tocseditadminrequest"></a>

```json
{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}

```

EditAdminRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FirstName|string|true|none|Admin first name|
|MiddleName|string|false|none|Admin middle name|
|LastName|string|true|none|Admin last name|
|NormalizeAddress|boolean|false|none|Normalize address|
|ProfileAddress|[Address](#schemaaddress)|true|none|none|
|Phone|string|false|none|Phone number|
|AltPhone|string|false|none|Alternative phone number|
|DateOfBirth|string(date-time)|false|none|Admin date of birth|
|Email|string|true|none|Admin email address|
|Permissions|[AdminPermissions](#schemaadminpermissions)|false|none|Details about the permissions for an admin|

<h2 id="tocS_AdminPermissions">AdminPermissions</h2>
<!-- backwards compatibility -->
<a id="schemaadminpermissions"></a>
<a id="schema_AdminPermissions"></a>
<a id="tocSadminpermissions"></a>
<a id="tocsadminpermissions"></a>

```json
{
  "ViewAdministration": false,
  "AddEditTerminateAdministrator": false,
  "RequestDeleteACHTransfer": false,
  "EditBusinessProfile": false,
  "AddEditTerminateCard": false,
  "RequestCardFunding": false,
  "ViewCardNumberReport": false,
  "ModifyTransactionNotes": false,
  "AdministerInstantIssueCards": false
}

```

AdminPermissions

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|ViewAdministration|boolean|true|none|Whether or not admin can view an administrator|
|AddEditTerminateAdministrator|boolean|true|none|Whether or not admin can create, edit, or delete an administrator|
|RequestDeleteACHTransfer|boolean|true|none|Whether or not admin can create or delete ACH transfer requests|
|EditBusinessProfile|boolean|true|none|Whether or not admin can edit the business profile|
|AddEditTerminateCard|boolean|true|none|Whether or not admin can create, edit, or terminate a card|
|RequestCardFunding|boolean|true|none|Whether or not admin can create a card funding request|
|ViewCardNumberReport|boolean|true|none|Whether or not admin can view the card number report|
|ModifyTransactionNotes|boolean|true|none|Whether or not admin can modify transaction notes|
|AdministerInstantIssueCards|boolean|false|none|Whether or not admin can administer instant issue cards|

<h2 id="tocS_EditAdminResponse">EditAdminResponse</h2>
<!-- backwards compatibility -->
<a id="schemaeditadminresponse"></a>
<a id="schema_EditAdminResponse"></a>
<a id="tocSeditadminresponse"></a>
<a id="tocseditadminresponse"></a>

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}

```

EditAdminResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Admin|[BusinessAdmin](#schemabusinessadmin)|true|none|Details about the business admin|

<h2 id="tocS_BusinessAdmin">BusinessAdmin</h2>
<!-- backwards compatibility -->
<a id="schemabusinessadmin"></a>
<a id="schema_BusinessAdmin"></a>
<a id="tocSbusinessadmin"></a>
<a id="tocsbusinessadmin"></a>

```json
{
  "BusinessAdminId": 0,
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  },
  "Status": ""
}

```

BusinessAdmin

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|BusinessAdminId|integer(int32)|true|none|Unique business admin id|
|FirstName|string|true|none|First name|
|MiddleName|string|false|none|Middle name|
|LastName|string|true|none|Last name|
|ProfileAddress|[AddressContact](#schemaaddresscontact)|true|none|none|
|Phone|string|false|none|Phone number|
|AltPhone|string|false|none|Alternative phone number|
|DateOfBirth|string(date-time)|true|none|Admin date of birth|
|Email|string|true|none|Admin email address|
|Permissions|[AdminPermissions](#schemaadminpermissions)|true|none|Details about the permissions for an admin|
|Status|string|true|none|Status of the business admin|

<h2 id="tocS_GetAdminResponse">GetAdminResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetadminresponse"></a>
<a id="schema_GetAdminResponse"></a>
<a id="tocSgetadminresponse"></a>
<a id="tocsgetadminresponse"></a>

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}

```

GetAdminResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Admin|[BusinessAdmin](#schemabusinessadmin)|true|none|Details about the business admin|

<h2 id="tocS_GetAdminListResponse">GetAdminListResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetadminlistresponse"></a>
<a id="schema_GetAdminListResponse"></a>
<a id="tocSgetadminlistresponse"></a>
<a id="tocsgetadminlistresponse"></a>

```json
{
  "BusinessAdmins": [
    {
      "BusinessAdminId": 0,
      "FirstName": "",
      "MiddleName": "",
      "LastName": "",
      "ProfileAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "Phone": "",
      "AltPhone": "",
      "DateOfBirth": "",
      "Email": "",
      "Permissions": {
        "ViewAdministration": false,
        "AddEditTerminateAdministrator": false,
        "RequestDeleteACHTransfer": false,
        "EditBusinessProfile": false,
        "AddEditTerminateCard": false,
        "RequestCardFunding": false,
        "ViewCardNumberReport": false,
        "ModifyTransactionNotes": false,
        "AdministerInstantIssueCards": false
      },
      "Status": ""
    }
  ]
}

```

GetAdminListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|BusinessAdmins|[[BusinessAdmin](#schemabusinessadmin)]|true|none|List of details about business admins|

<h2 id="tocS_GetBusinessBalanceResponse">GetBusinessBalanceResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetbusinessbalanceresponse"></a>
<a id="schema_GetBusinessBalanceResponse"></a>
<a id="tocSgetbusinessbalanceresponse"></a>
<a id="tocsgetbusinessbalanceresponse"></a>

```json
{
  "BusinessAccountId": 0,
  "BusinessAccountBalance": 0
}

```

GetBusinessBalanceResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|BusinessAccountId|integer(int32)|false|none|Business account id|
|BusinessAccountBalance|number(double)|false|none|Business account balance|

<h2 id="tocS_AdvancedCardholderDetailsResponse">AdvancedCardholderDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedcardholderdetailsresponse"></a>
<a id="schema_AdvancedCardholderDetailsResponse"></a>
<a id="tocSadvancedcardholderdetailsresponse"></a>
<a id="tocsadvancedcardholderdetailsresponse"></a>

```json
{
  "AccountId": 0,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "AccountStatus": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "CardList": [
    {
      "CardId": 0,
      "IssuedDate": "",
      "ExpirationDate": "",
      "Last4CardNumber": "",
      "CardStatus": ""
    }
  ],
  "SpendingRulesetId": 0,
  "SpendRules": {
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ],
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  },
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": ""
  },
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  },
  "CustomId": "",
  "IsVirtual": false
}

```

AdvancedCardholderDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|false|none|Unique cardholder account id|
|Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|AccountStatus|string|false|none|Cardholder account status (OPEN or CLOSED)|
|LedgerBalance|number(double)|false|none|Ledger balance for the card account, rounded to 2 decimal places|
|AvailableBalance|number(double)|false|none|Available balance for the card account, rounded to 2 decimal places|
|ProfileAddress|[AddressContact](#schemaaddresscontact)|false|none|none|
|Phone|string|false|none|Phone number|
|ShippingAddress|[AddressContact](#schemaaddresscontact)|false|none|none|
|ShippingPhone|string|false|none|Shipping Phone number|
|DateOfBirth|string(date-time)|false|none|Cardholder date of birth|
|Email|string|false|none|Cardholder email address|
|CardList|[[CardDetail](#schemacarddetail)]|false|none|List of details about cards associated with the account|
|SpendingRulesetId|integer(int32)|false|none|SpendingRulesetId for the cardholder account|
|SpendRules|[AdvancedSpendRulesResponse](#schemaadvancedspendrulesresponse)|false|none|Advanced Spend Rules Response|
|ScheduledFunding|[ScheduledFunding](#schemascheduledfunding)|false|none|Details about scheduled funding|
|LowBalanceFunding|[LowBalanceFunding](#schemalowbalancefunding)|false|none|Details about low balance funding|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|
|IsVirtual|boolean|false|none|Identifies virtual cardholder|

<h2 id="tocS_AdvancedSpendingRulesetItemResponse">AdvancedSpendingRulesetItemResponse</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedspendingrulesetitemresponse"></a>
<a id="schema_AdvancedSpendingRulesetItemResponse"></a>
<a id="tocSadvancedspendingrulesetitemresponse"></a>
<a id="tocsadvancedspendingrulesetitemresponse"></a>

```json
{
  "Id": 0,
  "Name": "",
  "CardCount": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false,
  "MccRestrictions": false,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "Description": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ]
}

```

AdvancedSpendingRulesetItemResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|false|none|Id|
|Name|string|false|none|Name|
|CardCount|integer(int32)|false|none|Card Count|
|DailySpendLimit|number(double)|false|none|Daily Spend Limit|
|WeeklySpendLimit|number(double)|false|none|Weekly Spend Limit|
|MonthlySpendLimit|number(double)|false|none|Monthly Spend Limit|
|YearlySpendLimit|number(double)|false|none|Yearly Spend Limit|
|LifetimeSpendLimit|number(double)|false|none|Lifetime Spend Limit|
|InternationalAllowed|boolean|false|none|International Allowed|
|CardNotPresentAllowed|boolean|false|none|Card Not Present Allowed|
|UsePexAccountBalanceForAuths|boolean|false|none|Use Pex Account Balance For Auths|
|UseCustomerAuthDecision|boolean|false|none|Use Customer Auth Decision|
|MccRestrictions|boolean|false|none|MCC Restrictions|
|MerchantCategories|[[AdvancedSpendingRulesetMerchantCategoryItemResponse](#schemaadvancedspendingrulesetmerchantcategoryitemresponse)]|false|none|Merchant Categories|

<h2 id="tocS_AdvancedSpendingRulesetMerchantCategoryItemResponse">AdvancedSpendingRulesetMerchantCategoryItemResponse</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedspendingrulesetmerchantcategoryitemresponse"></a>
<a id="schema_AdvancedSpendingRulesetMerchantCategoryItemResponse"></a>
<a id="tocSadvancedspendingrulesetmerchantcategoryitemresponse"></a>
<a id="tocsadvancedspendingrulesetmerchantcategoryitemresponse"></a>

```json
{
  "Id": 0,
  "Name": "",
  "Description": "",
  "TransactionLimit": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0
}

```

AdvancedSpendingRulesetMerchantCategoryItemResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|false|none|Id|
|Name|string|false|none|Name|
|Description|string|false|none|Description|
|TransactionLimit|number(double)|false|none|Transaction Limit|
|DailySpendLimit|number(double)|false|none|Daily Spend Limit|
|WeeklySpendLimit|number(double)|false|none|Weekly Spend Limit|
|MonthlySpendLimit|number(double)|false|none|Monthly Spend Limit|
|YearlySpendLimit|number(double)|false|none|Yearly Spend Limit|
|LifetimeSpendLimit|number(double)|false|none|Lifetime Spend Limit|

<h2 id="tocS_CreateAdvancedSpendingRulesetRequest">CreateAdvancedSpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreateadvancedspendingrulesetrequest"></a>
<a id="schema_CreateAdvancedSpendingRulesetRequest"></a>
<a id="tocScreateadvancedspendingrulesetrequest"></a>
<a id="tocscreateadvancedspendingrulesetrequest"></a>

```json
{
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

CreateAdvancedSpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Advance Spending Ruleset name|
|DailySpendLimit|number(double)|false|none|Advance Spending Ruleset daily spending limit|
|WeeklySpendLimit|number(double)|false|none|Advance Spending Ruleset weekly spending limit|
|MonthlySpendLimit|number(double)|false|none|Advance Spending Ruleset monthly spending limit|
|YearlySpendLimit|number(double)|false|none|Advance Spending Ruleset yearly spending limit|
|LifetimeSpendLimit|number(double)|false|none|Advance Spending Ruleset lifetime spending limit|
|MerchantCategories|[[AdvancedSpendingRulesetMerchantCategory](#schemaadvancedspendingrulesetmerchantcategory)]|false|none|Merchant categories|
|InternationalAllowed|boolean|false|none|Advance Spending Ruleset international purchases allowed|
|CardNotPresentAllowed|boolean|false|none|Advance Spending Ruleset card not present allowed on purchases|
|UsePexAccountBalanceForAuths|boolean|false|none|Advance Spending Ruleset use PEX account balance instead of card balance allowed|
|UseCustomerAuthDecision|boolean|false|none|Advance Spending Ruleset use customer authorization decision allowed|

<h2 id="tocS_AdvancedSpendingRulesetMerchantCategory">AdvancedSpendingRulesetMerchantCategory</h2>
<!-- backwards compatibility -->
<a id="schemaadvancedspendingrulesetmerchantcategory"></a>
<a id="schema_AdvancedSpendingRulesetMerchantCategory"></a>
<a id="tocSadvancedspendingrulesetmerchantcategory"></a>
<a id="tocsadvancedspendingrulesetmerchantcategory"></a>

```json
{
  "Id": 0,
  "Name": "",
  "TransactionLimit": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0
}

```

AdvancedSpendingRulesetMerchantCategory

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|false|none|Merchant Category Id|
|Name|string|false|none|Merchant Category Name|
|TransactionLimit|number(double)|false|none|Transaction Limit|
|DailySpendLimit|number(double)|false|none|Daily limit|
|WeeklySpendLimit|number(double)|false|none|Weekly limit|
|MonthlySpendLimit|number(double)|false|none|Monthly limit|
|YearlySpendLimit|number(double)|false|none|Yearly limit|
|LifetimeSpendLimit|number(double)|false|none|Lifetime limit|

<h2 id="tocS_CreateAdvancedSpendingRulesetResponse">CreateAdvancedSpendingRulesetResponse</h2>
<!-- backwards compatibility -->
<a id="schemacreateadvancedspendingrulesetresponse"></a>
<a id="schema_CreateAdvancedSpendingRulesetResponse"></a>
<a id="tocScreateadvancedspendingrulesetresponse"></a>
<a id="tocscreateadvancedspendingrulesetresponse"></a>

```json
{
  "RulesetId": 0
}

```

CreateAdvancedSpendingRulesetResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|Advance Spending Ruleset ID|

<h2 id="tocS_UpdateAdvancedSpendingRulesetRequest">UpdateAdvancedSpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdateadvancedspendingrulesetrequest"></a>
<a id="schema_UpdateAdvancedSpendingRulesetRequest"></a>
<a id="tocSupdateadvancedspendingrulesetrequest"></a>
<a id="tocsupdateadvancedspendingrulesetrequest"></a>

```json
{
  "Id": 0,
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

UpdateAdvancedSpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|true|none|Advance Spending Ruleset Id|
|Name|string|true|none|Advance Spending Ruleset name|
|DailySpendLimit|number(double)|false|none|Advance Spending Ruleset daily spending limit|
|WeeklySpendLimit|number(double)|false|none|Advance Spending Ruleset weekly spending limit|
|MonthlySpendLimit|number(double)|false|none|Advance Spending Ruleset monthly spending limit|
|YearlySpendLimit|number(double)|false|none|Advance Spending Ruleset yearly spending limit|
|LifetimeSpendLimit|number(double)|false|none|Advance Spending Ruleset lifetime spending limit|
|MerchantCategories|[[AdvancedSpendingRulesetMerchantCategory](#schemaadvancedspendingrulesetmerchantcategory)]|false|none|Merchant categories|
|InternationalAllowed|boolean|false|none|Advance Spending Ruleset international purchases allowed|
|CardNotPresentAllowed|boolean|false|none|Advance Spending Ruleset card not present allowed on purchases|
|UsePexAccountBalanceForAuths|boolean|false|none|Advance Spending Ruleset use PEX account balance instead of card balance allowed|
|UseCustomerAuthDecision|boolean|false|none|Advance Spending Ruleset use customer authorization decision allowed|

<h2 id="tocS_DeleteAdvancedSpendingRulesetRequest">DeleteAdvancedSpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemadeleteadvancedspendingrulesetrequest"></a>
<a id="schema_DeleteAdvancedSpendingRulesetRequest"></a>
<a id="tocSdeleteadvancedspendingrulesetrequest"></a>
<a id="tocsdeleteadvancedspendingrulesetrequest"></a>

```json
{
  "Id": 0
}

```

DeleteAdvancedSpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|true|none|Advance Spending Ruleset Id|

<h2 id="tocS_GetSpendingRulesetsResponse">GetSpendingRulesetsResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetspendingrulesetsresponse"></a>
<a id="schema_GetSpendingRulesetsResponse"></a>
<a id="tocSgetspendingrulesetsresponse"></a>
<a id="tocsgetspendingrulesetsresponse"></a>

```json
{
  "SpendingRulesets": [
    {
      "RulesetId": 0,
      "SpendingRulesetCategories": {
        "CategoryId": 0,
        "AssociationsOrganizationsAllowed": false,
        "AutomotiveDealersAllowed": false,
        "EducationalServicesAllowed": false,
        "EntertainmentAllowed": false,
        "FuelPumpsAllowed": false,
        "GasStationsConvenienceStoresAllowed": false,
        "GroceryStoresAllowed": false,
        "HealthcareChildcareServicesAllowed": false,
        "ProfessionalServicesAllowed": false,
        "RestaurantsAllowed": false,
        "RetailStoresAllowed": false,
        "TravelTransportationAllowed": false,
        "HardwareStoresAllowed": false
      },
      "MccRestrictions": false,
      "BacctId": 0,
      "Name": "",
      "CountCardsPresent": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0,
      "InternationalAllowed": false,
      "CardNotPresentAllowed": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    }
  ]
}

```

GetSpendingRulesetsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|SpendingRulesets|[[SpendingRuleset](#schemaspendingruleset)]|false|none|none|

<h2 id="tocS_SpendingRuleset">SpendingRuleset</h2>
<!-- backwards compatibility -->
<a id="schemaspendingruleset"></a>
<a id="schema_SpendingRuleset"></a>
<a id="tocSspendingruleset"></a>
<a id="tocsspendingruleset"></a>

```json
{
  "RulesetId": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "MccRestrictions": false,
  "BacctId": 0,
  "Name": "",
  "CountCardsPresent": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

SpendingRuleset

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|none|
|SpendingRulesetCategories|[SpendingRulesetCategories](#schemaspendingrulesetcategories)|false|none|none|
|MccRestrictions|boolean|false|read-only|none|
|BacctId|integer(int32)|false|none|none|
|Name|string|true|none|none|
|CountCardsPresent|integer(int32)|false|none|none|
|DailySpendLimit|number(double)|false|none|none|
|WeeklySpendLimit|number(double)|false|none|none|
|MonthlySpendLimit|number(double)|false|none|none|
|YearlySpendLimit|number(double)|false|none|none|
|LifetimeSpendLimit|number(double)|false|none|none|
|InternationalAllowed|boolean|false|none|none|
|CardNotPresentAllowed|boolean|false|none|none|
|UsePexAccountBalanceForAuths|boolean|false|none|none|
|UseCustomerAuthDecision|boolean|false|none|none|

<h2 id="tocS_SpendingRulesetCategories">SpendingRulesetCategories</h2>
<!-- backwards compatibility -->
<a id="schemaspendingrulesetcategories"></a>
<a id="schema_SpendingRulesetCategories"></a>
<a id="tocSspendingrulesetcategories"></a>
<a id="tocsspendingrulesetcategories"></a>

```json
{
  "CategoryId": 0,
  "AssociationsOrganizationsAllowed": false,
  "AutomotiveDealersAllowed": false,
  "EducationalServicesAllowed": false,
  "EntertainmentAllowed": false,
  "FuelPumpsAllowed": false,
  "GasStationsConvenienceStoresAllowed": false,
  "GroceryStoresAllowed": false,
  "HealthcareChildcareServicesAllowed": false,
  "ProfessionalServicesAllowed": false,
  "RestaurantsAllowed": false,
  "RetailStoresAllowed": false,
  "TravelTransportationAllowed": false,
  "HardwareStoresAllowed": false
}

```

SpendingRulesetCategories

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|CategoryId|integer(int32)|false|none|none|
|AssociationsOrganizationsAllowed|boolean|false|none|none|
|AutomotiveDealersAllowed|boolean|false|none|none|
|EducationalServicesAllowed|boolean|false|none|none|
|EntertainmentAllowed|boolean|false|none|none|
|FuelPumpsAllowed|boolean|false|none|none|
|GasStationsConvenienceStoresAllowed|boolean|false|none|none|
|GroceryStoresAllowed|boolean|false|none|none|
|HealthcareChildcareServicesAllowed|boolean|false|none|none|
|ProfessionalServicesAllowed|boolean|false|none|none|
|RestaurantsAllowed|boolean|false|none|none|
|RetailStoresAllowed|boolean|false|none|none|
|TravelTransportationAllowed|boolean|false|none|none|
|HardwareStoresAllowed|boolean|false|none|none|

<h2 id="tocS_CreateSpendingRulesetRequest">CreateSpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatespendingrulesetrequest"></a>
<a id="schema_CreateSpendingRulesetRequest"></a>
<a id="tocScreatespendingrulesetrequest"></a>
<a id="tocscreatespendingrulesetrequest"></a>

```json
{
  "Name": "",
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

CreateSpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Spending Ruleset name|
|DailySpendLimit|number(double)|false|none|Spending Ruleset count cards present|
|SpendingRulesetCategories|[SpendingRulesetCategories](#schemaspendingrulesetcategories)|false|none|none|
|InternationalAllowed|boolean|false|none|Spending Ruleset MCC restrictions|
|CardNotPresentAllowed|boolean|false|none|Spending Ruleset card not present allowed on purchases|
|UsePexAccountBalanceForAuths|boolean|false|none|Spending Ruleset use PEX account balance instead of card balance allowed|
|UseCustomerAuthDecision|boolean|false|none|Spending Ruleset use customer authorization decision allowed|

<h2 id="tocS_CreateSpendingRulesetResponse">CreateSpendingRulesetResponse</h2>
<!-- backwards compatibility -->
<a id="schemacreatespendingrulesetresponse"></a>
<a id="schema_CreateSpendingRulesetResponse"></a>
<a id="tocScreatespendingrulesetresponse"></a>
<a id="tocscreatespendingrulesetresponse"></a>

```json
{
  "RulesetId": 0
}

```

CreateSpendingRulesetResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|none|

<h2 id="tocS_UpdateSpendingRulesetRequest">UpdateSpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdatespendingrulesetrequest"></a>
<a id="schema_UpdateSpendingRulesetRequest"></a>
<a id="tocSupdatespendingrulesetrequest"></a>
<a id="tocsupdatespendingrulesetrequest"></a>

```json
{
  "RulesetId": 0,
  "Name": "",
  "CountCardsPresent": 0,
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "MccRestrictions": false,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

UpdateSpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|true|none|Spending Ruleset Id|
|Name|string|true|none|Spending Ruleset name|
|CountCardsPresent|integer(int32)|false|none|Spending Ruleset count cards present|
|DailySpendLimit|number(double)|false|none|Spending Ruleset daily spending limit|
|SpendingRulesetCategories|[SpendingRulesetCategories](#schemaspendingrulesetcategories)|false|none|none|
|MccRestrictions|boolean|false|read-only|Spending Ruleset MCC restrictions|
|InternationalAllowed|boolean|false|none|Spending Ruleset international purchases allowed|
|CardNotPresentAllowed|boolean|false|none|Spending Ruleset card not present allowed on purchases|
|UsePexAccountBalanceForAuths|boolean|false|none|Spending Ruleset use PEX account balance instead of card balance allowed|
|UseCustomerAuthDecision|boolean|false|none|Spending Ruleset use customer authorization decision allowed|

<h2 id="tocS_SpendingRulesetResponse">SpendingRulesetResponse</h2>
<!-- backwards compatibility -->
<a id="schemaspendingrulesetresponse"></a>
<a id="schema_SpendingRulesetResponse"></a>
<a id="tocSspendingrulesetresponse"></a>
<a id="tocsspendingrulesetresponse"></a>

```json
{
  "RulesetId": 0
}

```

SpendingRulesetResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|Spending Ruleset Id|

<h2 id="tocS_DeleteSpendingRulesetRequest">DeleteSpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemadeletespendingrulesetrequest"></a>
<a id="schema_DeleteSpendingRulesetRequest"></a>
<a id="tocSdeletespendingrulesetrequest"></a>
<a id="tocsdeletespendingrulesetrequest"></a>

```json
{
  "RulesetId": 0
}

```

DeleteSpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|true|none|Spending Ruleset Id|

<h2 id="tocS_GetSpendingRulesetResponse">GetSpendingRulesetResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetspendingrulesetresponse"></a>
<a id="schema_GetSpendingRulesetResponse"></a>
<a id="tocSgetspendingrulesetresponse"></a>
<a id="tocsgetspendingrulesetresponse"></a>

```json
{
  "SpendingRuleset": {
    "RulesetId": 0,
    "Name": "",
    "DailySpendLimit": 0,
    "SpendingRulesetCategories": {
      "CategoryId": 0,
      "AssociationsOrganizationsAllowed": false,
      "AutomotiveDealersAllowed": false,
      "EducationalServicesAllowed": false,
      "EntertainmentAllowed": false,
      "FuelPumpsAllowed": false,
      "GasStationsConvenienceStoresAllowed": false,
      "GroceryStoresAllowed": false,
      "HealthcareChildcareServicesAllowed": false,
      "ProfessionalServicesAllowed": false,
      "RestaurantsAllowed": false,
      "RetailStoresAllowed": false,
      "TravelTransportationAllowed": false,
      "HardwareStoresAllowed": false
    },
    "MccRestrictions": false,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}

```

GetSpendingRulesetResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|SpendingRuleset|[SpendingRulesetGet](#schemaspendingrulesetget)|false|none|Spending Ruleset Get|

<h2 id="tocS_SpendingRulesetGet">SpendingRulesetGet</h2>
<!-- backwards compatibility -->
<a id="schemaspendingrulesetget"></a>
<a id="schema_SpendingRulesetGet"></a>
<a id="tocSspendingrulesetget"></a>
<a id="tocsspendingrulesetget"></a>

```json
{
  "RulesetId": 0,
  "Name": "",
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "MccRestrictions": false,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}

```

SpendingRulesetGet

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|Ruleset Id|
|Name|string|true|none|Name|
|DailySpendLimit|number(double)|false|none|Daily Spend Limit|
|SpendingRulesetCategories|[SpendingRulesetCategories](#schemaspendingrulesetcategories)|false|none|none|
|MccRestrictions|boolean|false|read-only|Mcc Restrictions|
|InternationalAllowed|boolean|false|none|International Allowed|
|CardNotPresentAllowed|boolean|false|none|Card Not Present Allowed|
|UsePexAccountBalanceForAuths|boolean|false|none|Use Pex Account Balance For Auths|
|UseCustomerAuthDecision|boolean|false|none|Use Customer Auth Decision|

<h2 id="tocS_RemoteAuthorizationResponse">RemoteAuthorizationResponse</h2>
<!-- backwards compatibility -->
<a id="schemaremoteauthorizationresponse"></a>
<a id="schema_RemoteAuthorizationResponse"></a>
<a id="tocSremoteauthorizationresponse"></a>
<a id="tocsremoteauthorizationresponse"></a>

```json
{
  "StatusCode": "",
  "Ticks": 0
}

```

RemoteAuthorizationResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|StatusCode|string|false|none|Status Code|
|Ticks|integer(int64)|false|none|Ticks|

#### Enumerated Values

|Property|Value|
|---|---|
|StatusCode|Continue|
|StatusCode|SwitchingProtocols|
|StatusCode|OK|
|StatusCode|Created|
|StatusCode|Accepted|
|StatusCode|NonAuthoritativeInformation|
|StatusCode|NoContent|
|StatusCode|ResetContent|
|StatusCode|PartialContent|
|StatusCode|MultipleChoices|
|StatusCode|Ambiguous|
|StatusCode|MovedPermanently|
|StatusCode|Moved|
|StatusCode|Found|
|StatusCode|Redirect|
|StatusCode|SeeOther|
|StatusCode|RedirectMethod|
|StatusCode|NotModified|
|StatusCode|UseProxy|
|StatusCode|Unused|
|StatusCode|TemporaryRedirect|
|StatusCode|RedirectKeepVerb|
|StatusCode|BadRequest|
|StatusCode|Unauthorized|
|StatusCode|PaymentRequired|
|StatusCode|Forbidden|
|StatusCode|NotFound|
|StatusCode|MethodNotAllowed|
|StatusCode|NotAcceptable|
|StatusCode|ProxyAuthenticationRequired|
|StatusCode|RequestTimeout|
|StatusCode|Conflict|
|StatusCode|Gone|
|StatusCode|LengthRequired|
|StatusCode|PreconditionFailed|
|StatusCode|RequestEntityTooLarge|
|StatusCode|RequestUriTooLong|
|StatusCode|UnsupportedMediaType|
|StatusCode|RequestedRangeNotSatisfiable|
|StatusCode|ExpectationFailed|
|StatusCode|UpgradeRequired|
|StatusCode|InternalServerError|
|StatusCode|NotImplemented|
|StatusCode|BadGateway|
|StatusCode|ServiceUnavailable|
|StatusCode|GatewayTimeout|
|StatusCode|HttpVersionNotSupported|

<h2 id="tocS_CreateNoteByNetworkTransactionIdRequest">CreateNoteByNetworkTransactionIdRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatenotebynetworktransactionidrequest"></a>
<a id="schema_CreateNoteByNetworkTransactionIdRequest"></a>
<a id="tocScreatenotebynetworktransactionidrequest"></a>
<a id="tocscreatenotebynetworktransactionidrequest"></a>

```json
{
  "NoteText": "",
  "NetworkTransactionId": 0
}

```

CreateNoteByNetworkTransactionIdRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|NoteText|string|true|none|Transaction note text|
|NetworkTransactionId|integer(int64)|true|none|Transaction id|

<h2 id="tocS_NoteResponse">NoteResponse</h2>
<!-- backwards compatibility -->
<a id="schemanoteresponse"></a>
<a id="schema_NoteResponse"></a>
<a id="tocSnoteresponse"></a>
<a id="tocsnoteresponse"></a>

```json
{
  "Id": 0
}

```

NoteResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int64)|false|none|Transaction note id|

<h2 id="tocS_CreateNoteRequest">CreateNoteRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatenoterequest"></a>
<a id="schema_CreateNoteRequest"></a>
<a id="tocScreatenoterequest"></a>
<a id="tocscreatenoterequest"></a>

```json
{
  "TransactionId": 0,
  "NoteText": "",
  "Pending": false
}

```

CreateNoteRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TransactionId|integer(int64)|true|none|Transaction id|
|NoteText|string|true|none|Transaction note text|
|Pending|boolean|false|none|Is pending transaction|

<h2 id="tocS_NoteRequest">NoteRequest</h2>
<!-- backwards compatibility -->
<a id="schemanoterequest"></a>
<a id="schema_NoteRequest"></a>
<a id="tocSnoterequest"></a>
<a id="tocsnoterequest"></a>

```json
{
  "NoteText": "",
  "Pending": false
}

```

NoteRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|NoteText|string|true|none|Transaction note text|
|Pending|boolean|false|none|Is pending transaction|

<h2 id="tocS_DeleteNoteRequest">DeleteNoteRequest</h2>
<!-- backwards compatibility -->
<a id="schemadeletenoterequest"></a>
<a id="schema_DeleteNoteRequest"></a>
<a id="tocSdeletenoterequest"></a>
<a id="tocsdeletenoterequest"></a>

```json
{
  "Pending": false
}

```

DeleteNoteRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Pending|boolean|false|none|Is pending transaction|

<h2 id="tocS_GetGroupsResponse">GetGroupsResponse</h2>
<!-- backwards compatibility -->
<a id="schemagetgroupsresponse"></a>
<a id="schema_GetGroupsResponse"></a>
<a id="tocSgetgroupsresponse"></a>
<a id="tocsgetgroupsresponse"></a>

```json
{
  "Groups": [
    {
      "Id": 0,
      "Name": ""
    }
  ]
}

```

GetGroupsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Groups|[[Group](#schemagroup)]|true|none|The list of groups|

<h2 id="tocS_Group">Group</h2>
<!-- backwards compatibility -->
<a id="schemagroup"></a>
<a id="schema_Group"></a>
<a id="tocSgroup"></a>
<a id="tocsgroup"></a>

```json
{
  "Id": 0,
  "Name": ""
}

```

Group

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Id|integer(int32)|true|none|Unique Id of the Group|
|Name|string|true|none|Group Name|

<h2 id="tocS_CreateGroupRequest">CreateGroupRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreategrouprequest"></a>
<a id="schema_CreateGroupRequest"></a>
<a id="tocScreategrouprequest"></a>
<a id="tocscreategrouprequest"></a>

```json
{
  "Name": ""
}

```

CreateGroupRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Group name|

<h2 id="tocS_CreateGroupResponse">CreateGroupResponse</h2>
<!-- backwards compatibility -->
<a id="schemacreategroupresponse"></a>
<a id="schema_CreateGroupResponse"></a>
<a id="tocScreategroupresponse"></a>
<a id="tocscreategroupresponse"></a>

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}

```

CreateGroupResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Group|[Group](#schemagroup)|true|none|Details about a cardholder group|

<h2 id="tocS_UpdateGroupRequest">UpdateGroupRequest</h2>
<!-- backwards compatibility -->
<a id="schemaupdategrouprequest"></a>
<a id="schema_UpdateGroupRequest"></a>
<a id="tocSupdategrouprequest"></a>
<a id="tocsupdategrouprequest"></a>

```json
{
  "Name": ""
}

```

UpdateGroupRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Name|string|true|none|Group name|

<h2 id="tocS_UpdateGroupResponse">UpdateGroupResponse</h2>
<!-- backwards compatibility -->
<a id="schemaupdategroupresponse"></a>
<a id="schema_UpdateGroupResponse"></a>
<a id="tocSupdategroupresponse"></a>
<a id="tocsupdategroupresponse"></a>

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}

```

UpdateGroupResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Group|[Group](#schemagroup)|true|none|Details about a cardholder group|

<h2 id="tocS_RemoveGroupResponse">RemoveGroupResponse</h2>
<!-- backwards compatibility -->
<a id="schemaremovegroupresponse"></a>
<a id="schema_RemoveGroupResponse"></a>
<a id="tocSremovegroupresponse"></a>
<a id="tocsremovegroupresponse"></a>

```json
{
  "GroupId": 0
}

```

RemoveGroupResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|GroupId|integer(int32)|true|none|The group ID that was removed|

<h2 id="tocS_CardHolderDetailsResponse">CardHolderDetailsResponse</h2>
<!-- backwards compatibility -->
<a id="schemacardholderdetailsresponse"></a>
<a id="schema_CardHolderDetailsResponse"></a>
<a id="tocScardholderdetailsresponse"></a>
<a id="tocscardholderdetailsresponse"></a>

```json
{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "AccountId": 0,
  "AccountNumber": "",
  "AvailableBalance": 0,
  "LedgerBalance": 0,
  "SpendRules": false,
  "AccountCreationTime": "",
  "ManualStatus": "",
  "SystemStatus": "",
  "PinSet": false,
  "BSAcctId": 0,
  "IsVirtual": false,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "SpendingRulesetModel": {
    "RulesetId": 0,
    "Name": ""
  },
  "EmbossingDetails": [
    {
      "AccountId": 0,
      "CardNumber": "",
      "ManualStatus": "",
      "SystemStatus": "",
      "CreatedDate": "",
      "PlasticDetails": [
        {
          "PlasticSequence": "",
          "ManualStatus": "",
          "IssuedDate": "",
          "ExpirationDate": ""
        }
      ]
    }
  ],
  "CustomId": ""
}

```

CardHolderDetailsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FirstName|string|false|none|Firs tName|
|MiddleName|string|false|none|Middle Name|
|LastName|string|false|none|Last Name|
|AccountId|integer(int32)|false|none|Account Id|
|AccountNumber|string|false|none|Account Number|
|AvailableBalance|number(double)|false|none|Available Balance|
|LedgerBalance|number(double)|false|none|Ledger Balance|
|SpendRules|boolean|false|none|Spend Rules|
|AccountCreationTime|string(date-time)|false|none|Account Creation Time|
|ManualStatus|string|false|none|Manual Status|
|SystemStatus|string|false|none|System Status|
|PinSet|boolean|false|none|Pin Set|
|BSAcctId|integer(int32)|false|none|Business Account Id|
|IsVirtual|boolean|false|none|Identifies virtual cardholder|
|Group|[CardholderGroup](#schemacardholdergroup)|false|none|Details about a cardholder group|
|SpendingRulesetModel|[SpendingRulesetModel](#schemaspendingrulesetmodel)|false|none|Spending Ruleset Model|
|EmbossingDetails|[[EmbossingDetails](#schemaembossingdetails)]|false|none|Embossing Details|
|CustomId|string|false|none|User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters)|

<h2 id="tocS_SpendingRulesetModel">SpendingRulesetModel</h2>
<!-- backwards compatibility -->
<a id="schemaspendingrulesetmodel"></a>
<a id="schema_SpendingRulesetModel"></a>
<a id="tocSspendingrulesetmodel"></a>
<a id="tocsspendingrulesetmodel"></a>

```json
{
  "RulesetId": 0,
  "Name": ""
}

```

SpendingRulesetModel

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|Rulese tId|
|Name|string|false|none|Name|

<h2 id="tocS_EmbossingDetails">EmbossingDetails</h2>
<!-- backwards compatibility -->
<a id="schemaembossingdetails"></a>
<a id="schema_EmbossingDetails"></a>
<a id="tocSembossingdetails"></a>
<a id="tocsembossingdetails"></a>

```json
{
  "AccountId": 0,
  "CardNumber": "",
  "ManualStatus": "",
  "SystemStatus": "",
  "CreatedDate": "",
  "PlasticDetails": [
    {
      "PlasticSequence": "",
      "ManualStatus": "",
      "IssuedDate": "",
      "ExpirationDate": ""
    }
  ]
}

```

EmbossingDetails

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|false|none|Account Id|
|CardNumber|string|false|none|Card Number|
|ManualStatus|string|false|none|Manual Status|
|SystemStatus|string|false|none|System Status|
|CreatedDate|string(date-time)|false|none|Created Date|
|PlasticDetails|[[PlasticDetials](#schemaplasticdetials)]|false|none|Plastic Details|

<h2 id="tocS_PlasticDetials">PlasticDetials</h2>
<!-- backwards compatibility -->
<a id="schemaplasticdetials"></a>
<a id="schema_PlasticDetials"></a>
<a id="tocSplasticdetials"></a>
<a id="tocsplasticdetials"></a>

```json
{
  "PlasticSequence": "",
  "ManualStatus": "",
  "IssuedDate": "",
  "ExpirationDate": ""
}

```

PlasticDetials

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|PlasticSequence|string|false|none|Plastic Sequence|
|ManualStatus|string|false|none|Manual Status|
|IssuedDate|string(date-time)|false|none|Issued Date|
|ExpirationDate|string(date-time)|false|none|Expiration Date|

<h2 id="tocS_BulkResponse">BulkResponse</h2>
<!-- backwards compatibility -->
<a id="schemabulkresponse"></a>
<a id="schema_BulkResponse"></a>
<a id="tocSbulkresponse"></a>
<a id="tocsbulkresponse"></a>

```json
{
  "TotalNumberOfCards": 0
}

```

BulkResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TotalNumberOfCards|integer(int32)|false|none|Total number of cards|

<h2 id="tocS_FundingRequest">FundingRequest</h2>
<!-- backwards compatibility -->
<a id="schemafundingrequest"></a>
<a id="schema_FundingRequest"></a>
<a id="tocSfundingrequest"></a>
<a id="tocsfundingrequest"></a>

```json
{
  "Amount": 0
}

```

FundingRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Amount|number(double)|false|none|Funding amount|

<h2 id="tocS_FundMultipleCardsRequest">FundMultipleCardsRequest</h2>
<!-- backwards compatibility -->
<a id="schemafundmultiplecardsrequest"></a>
<a id="schema_FundMultipleCardsRequest"></a>
<a id="tocSfundmultiplecardsrequest"></a>
<a id="tocsfundmultiplecardsrequest"></a>

```json
{
  "Cards": [
    {
      "AccountId": 0,
      "Amount": 0
    }
  ],
  "TransferType": ""
}

```

FundMultipleCardsRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Cards|[[FundCardItem](#schemafundcarditem)]|true|none|Cards|
|TransferType|string|true|none|B2C or C2B fund or defund transfer type codes  (ErrorMessage = "Required") [EnumDataType(TransferTypeEnum)]|

<h2 id="tocS_FundCardItem">FundCardItem</h2>
<!-- backwards compatibility -->
<a id="schemafundcarditem"></a>
<a id="schema_FundCardItem"></a>
<a id="tocSfundcarditem"></a>
<a id="tocsfundcarditem"></a>

```json
{
  "AccountId": 0,
  "Amount": 0
}

```

FundCardItem

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|true|none|Account id|
|Amount|number(double)|true|none|Funding amount|

<h2 id="tocS_FundMultipleCardsResponse">FundMultipleCardsResponse</h2>
<!-- backwards compatibility -->
<a id="schemafundmultiplecardsresponse"></a>
<a id="schema_FundMultipleCardsResponse"></a>
<a id="tocSfundmultiplecardsresponse"></a>
<a id="tocsfundmultiplecardsresponse"></a>

```json
{
  "Success": false,
  "Results": [
    {
      "BusinessTransactionId": 0,
      "BusinessCurrentBalance": 0,
      "AccountId": 0,
      "TransactionId": 0,
      "CurrentBalance": 0,
      "ResponseCode": 0,
      "Message": ""
    }
  ],
  "Errors": [
    {
      "AccountId": 0,
      "ResponseCode": 0,
      "Message": ""
    }
  ]
}

```

FundMultipleCardsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Success|boolean|false|none|Success|
|Results|[[FundCardItemResponse](#schemafundcarditemresponse)]|false|none|Succesful funding|
|Errors|[[FundCardItemErrorResponse](#schemafundcarditemerrorresponse)]|false|none|Unsuccesful fundings with errors|

<h2 id="tocS_FundCardItemResponse">FundCardItemResponse</h2>
<!-- backwards compatibility -->
<a id="schemafundcarditemresponse"></a>
<a id="schema_FundCardItemResponse"></a>
<a id="tocSfundcarditemresponse"></a>
<a id="tocsfundcarditemresponse"></a>

```json
{
  "BusinessTransactionId": 0,
  "BusinessCurrentBalance": 0,
  "AccountId": 0,
  "TransactionId": 0,
  "CurrentBalance": 0,
  "ResponseCode": 0,
  "Message": ""
}

```

FundCardItemResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|BusinessTransactionId|integer(int64)|false|none|Business transaction id|
|BusinessCurrentBalance|number(double)|false|none|Business current balance|
|AccountId|integer(int32)|false|none|Cardholder account id|
|TransactionId|integer(int64)|false|none|Cardholder transaction id|
|CurrentBalance|number(double)|false|none|Cardholder current balance|
|ResponseCode|integer(int32)|false|none|Response code|
|Message|string|false|none|Response message|

<h2 id="tocS_FundCardItemErrorResponse">FundCardItemErrorResponse</h2>
<!-- backwards compatibility -->
<a id="schemafundcarditemerrorresponse"></a>
<a id="schema_FundCardItemErrorResponse"></a>
<a id="tocSfundcarditemerrorresponse"></a>
<a id="tocsfundcarditemerrorresponse"></a>

```json
{
  "AccountId": 0,
  "ResponseCode": 0,
  "Message": ""
}

```

FundCardItemErrorResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AccountId|integer(int32)|false|none|Cardholder account id|
|ResponseCode|integer(int32)|false|none|Response code|
|Message|string|false|none|Response message|

<h2 id="tocS_ScheduledFundingRequest">ScheduledFundingRequest</h2>
<!-- backwards compatibility -->
<a id="schemascheduledfundingrequest"></a>
<a id="schema_ScheduledFundingRequest"></a>
<a id="tocSscheduledfundingrequest"></a>
<a id="tocsscheduledfundingrequest"></a>

```json
{
  "Frequency": "",
  "Amount": 0
}

```

ScheduledFundingRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Frequency|string|false|none|Funding frequency<br /><br>&lt;br/&gt;<br>Possible interger values for Frequency parameter of scheduled funding are: <br>&lt;br/&gt;<br>0 - every Day<br /><br>&lt;br/&gt;<br>1 - every Monday<br /><br>&lt;br/&gt;<br>2 - every Tuesday<br /><br>&lt;br/&gt;<br>3 - every Wednesday<br /><br>&lt;br/&gt;<br>4 - every Thursday<br /><br>&lt;br/&gt;<br>5 - every Friday<br /><br>&lt;br/&gt;<br>6 - every Saturday<br /><br>&lt;br/&gt;<br>7 - every Sunday<br /><br>&lt;br/&gt;<br>8 - every 1st of the Month<br />|
|Amount|number(double)|false|none|Funding amount|

#### Enumerated Values

|Property|Value|
|---|---|
|Frequency|DAY|
|Frequency|MONDAY|
|Frequency|TUESDAY|
|Frequency|WEDNESDAY|
|Frequency|THURSDAY|
|Frequency|FRIDAY|
|Frequency|SATURDAY|
|Frequency|SUNDAY|
|Frequency|FIRSTOFMONTH|

<h2 id="tocS_SpendingRulesetRequest">SpendingRulesetRequest</h2>
<!-- backwards compatibility -->
<a id="schemaspendingrulesetrequest"></a>
<a id="schema_SpendingRulesetRequest"></a>
<a id="tocSspendingrulesetrequest"></a>
<a id="tocsspendingrulesetrequest"></a>

```json
{
  "RulesetId": 0
}

```

SpendingRulesetRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|RulesetId|integer(int32)|false|none|Id of ruleset or null|

