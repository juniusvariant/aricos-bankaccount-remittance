---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
- <a href='#'>Contact for API User and Password</a>
- <a href='#'>Contact us if you got any trouble for using this API</a>

includes:
  - data-references
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Aricos Bank Accout Remittance API
---

# Introduction

Aricos is middleware that is make transfer transaction easy, fast, secure, reliable and accessible from all around the World. We provide simple APIs which you can use to send money to all banks in Indonesia quickly and securely.

Aricos is organized around REST. We use built-in HTTP features and HTTP verbs and we return all responses in JSON.

## Bank Account Remittance Overview

Use the Remittance API to transfer funds instantly to any bank in Indonesia at any time, including holidays and weekends. Due to restrictions from the banks, we’re unable to disburse when the bank channel are offline or when they fail.

The remittance flow is as follows:

1. [Prefund](#prefund) your Aricos account balance

2. [Create a customer](#create-customer) which represents the sender, and a customer which represents the recipient of the remittance. You’ll get an id for each

3. [Create a remittance](#create-remittance), attaching ids of the sender and recipient

4. We run this remittance through our risk-scoring system. If necessary, our compliance team will contact you for additional verification of information

5. We process the remittance and return a callback with the status of the remittance. You may also query the status of a remittance anytime via the [Get Remittance](#get-remittance) API

# Getting Started

## Set Up Your Account

To use our Bank Account Remittance APIs, register for an Aricos account by contacting your account manager or our support team.

You can start testing our APIs immediately in development environment. When you are ready to process live transactions, contact your account manager to go live.

## Retrieve Your API Account

Before you access all our features, you have to register your account to access all our API Feature. Our support team will give you the information of your account to login into our API.

To successfully authenticate with Aricos's API, you must append a colon and Base 64 encode the API key. All API requests should be made over HTTPS instead of HTTP (all calls made over plain HTTP will fail).

You can access our development end-point url to <span style="color:blue"> https://dev-bankaccount.aricos.co.id </span> and production end-point url to <span style="color:blue"> https://bankaccount.aricos.co.id </span>.

## Start Testing!

You may test our APIs by sending requests in the development environment--You will automatically get IDR balances in your development account balance for testing. Requests made in the development environment will not hit the banking networks and will not cost you anything.

## Postman Collection

The easiest way to get started using our API is to use our Postman Collection. Postman is a free client application that enables you to make calls to APIs easily. To make integrating with our APIs easier, we've created a Postman Collection of our endpoints so that you can test our APIs more easily.

The following is an outline of actions to get started with Postman.

1. Install [Postman](https://www.getpostman.com/).

2. Download our <a href="https://s.id/-Tcoq" download> Postman collection</a>.

3. Open Postman and Import the Aricos API Postman Collection.

4. Set up the collection’s Authorization header.

	a. Under the Authorization tab of each folder, the default authorization type is set to “Inherit auth from parent”. The “Inherit auth from parent” setting indicates that every request in the folder by default uses the authorization type from the parent.

	b. Edit the Aricos API collection.

	c. Under “Authorization”, paste your secret API key into the Username. Use your Development Key to test in the development environment, and your Live Key to send live transactions.

	d. Click Update.

	e. This authorization key will be automatically used for each request in the collection.

5. Try getting [your balance](#balance).

	a. Click on the Balances folder and click Get Balances.

	b. Hit the blue Send button.

	c. In the response area, you should get your latest cash balance.

6. If you can query your balance successfully, you’re all set up! Feel free to explore our other APIs by selecting it in the collection and launching it.

# Account

## Account Register

All information about your account and password will be provide by our support team by email. So if you're not getting any information about your account for development testing or for go live, please let us know.

## Account Login

```shell
POST https://dev-bankaccount.aricos.co.id/oauth/token
```

You have to login to get token access before you do a request to our APIs. You have to keep every token from our request response every time you want to access another request.

### Login Request

> Login Example Request:

```shell
curl --location --request POST 'https://dev-bankaccount.aricos.co.id/oauth/token' \

--header 'Accept: application/json' \

--form 'grant_type="password"' \

--form 'password="password"' \

--form 'username="user@mail.com"' \

--form 'client_id="94c92649-ae06-4f6e-b03b-b5a4327d0a50"' \

--form 'client_secret="te4hNdxm9BM8eRcG4AQMDes4GLQt0ujPbS5d8CHR"'
```
> Make sure to replace `username` and `password` with your account credential. </br>

Parameter | Description
--------- | -----------
grant_type | Grant Type To Generate Token And Fix Value
username | The User Account That Provided By Our Team
password | The User Password That Provided By Our Team
client_id | The Client ID That Provided By Our Team
client_secret | The Client Secret That Provided By Our Team

<aside class="notice">
   Make sure to replace <code>username</code> and <code>password</code> with your account credential.
</aside>

### Login Response

> Login Example Response:

```shell
{

"token_type": "Bearer",

"expires_in": 31536000,

"access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5NGM5MjY0OS1hZTA2LTRmNmUtYjAzYi1iNWE0MzI3ZDBhNDgiLCJqdGkiOiI1NmU3ZTUyZGQ3ZGNmOTBiM2Q3MDFkY2M5MTVmYzFmYWU2YWFjMjAwNjg1Mjc0ZmI2MThiZjY0ZGZhZmVlY2M1MTEwOGI1OTg4YzIwNTkwNiIsImlhdCI6MTY0MjA2NTU3OS4wNTU1ODksIm5iZiI6MTY0MjA2NTU3OS4wNTU1OTgsImV4cCI6MTY3MzYwMTU3OS4wMjM4NTUsInN1YiI6ImFlMzYwZjk2LWNkMjYtNGVlYy1hNzFlLTk1MTZkN2YzZjUwYSIsInNjb3BlcyI6W119.rgeLHfR97_ntN3lwdfUbM2XqxMGQ8jHXjYYvaXGpsp-JVc9MFPVv-_x9mNE_9JguPV1eyOVrCO2Rsf6RT9VRpLYShZ1bDt4ZFCkJ6GC_iE7rL8GIzdNxXCOOuCmDT8u1L_V6y81f9jdMYfLqtDgU54EFoPTZbIRD9-NPshtzM3bkGLT8PomKdJw5_-fUnuYIsZ3alh8j8hdZ2Yl1nthiBoF4vMBKjRG3SJbex3Rb08Lyy11J6lT26dDcLMMKTHqBIYarfwHdZtJs-qHJxg1Ne142y4L4g_jcAjQ-eVR7EcGWaMDN-3yqqEyX1tlcYkd-d4FcFYxWv6kuZ7y8LuXMUtYgXWlrb8ntcpEvviESVTmK9RN3l26Tmz_-QPVaJMdGJ0tljiS29LIm13kabps0Uav8AR0C3dA7S7XZm2FlaKwBtBunOguO4yIvY4dHuEkFuKcCr5GHFdFgsGWDX6LjBuYxRL9KUaas_gTHvMlMGeAaM7n5w55F44SAWNgZyvvEGciwMW0uOYHr9a1RNUiBafmAsDFpoO7FUu-lrUom2VLzfXWuIZF8sOV4rJRdas5vDwOZTBcMSt7fSUtpR2HdOzAw0MR5hsMYWCV9TjeWTiRGgBXZvE1j6LuD-22idsaInVFrCENyO9jsmrSs7GPLHlkYXDV0-wmZCDoOP1nnQk4",

"refresh_token": "def50200325bd991fab946343ce6c945a498696fce7d15c2b70c8354e5266e595f2853ffdfcd8b918b6c3eba922bd870f1f493bf3803611bd7329512a48d8448524f96a7ec85c984676c7a3856ef5e67cd3cd02fc58235e728cbfd656c43c261a153122804791ba5a31588f3ecbd03b79996aa5b688a3f053fb0b929acba44164cd5df70b8068a871e3fb746f59032d79c81187e4e5c59eb029b562f62f142ab83dbd4b462dd904a44ed6195c89be2996a79702a27b6a5468a1b2cb48abe52b160c243f3790c99cb67dd85e60d1c0e809b22129cbb9fd2f5f36d7468d78d38d77ae8167c49ba8db12c8fc55b94b92cee0d6b85e64a32c575d43953683403a068845bdf06ae6277b0013999d286fe28216726ab85170ab726c7bdb8c4a5fec361a651ec4e984c1ba262b2d755a6206380c6cd5b2f38744a89c8205ceea0760059ac47d67ffc1d358b31fe9516373d652afa396ca9fde9c4f912c0b0bd790a284cbbd5885ffecb88567cd2949b85d0d6853798d63c58812dabeeb59767f81e4a2da0b0b888e3f908fd8ce148eec28ed1f12f889b3798dbf0772486346dced260e0f32d5ba8f1380279d6"

}
```

Parameter | Description
--------- | -----------
expires_in | User Validity Period Time To Access Our API
access_token | Bearer Token That You Have To Use Everytime When You Want To Access Our APIs

# Balance

## Prefund Your Balance

Your balance refers to stored value in your Aricos account which can be sent out in remittances or withdrawn. Before you do any remittances, you will first have to add to your account balance ("prefund"). You can do this by transferring funds to Aricos's bank accounts. You can will get information about our bank account from our team so you can do prefund. After you have transferred the funds, please save the proof of transfer.

If you have prefunding to your account, the balance should be detected and updated in your account in 15-30 minutes. If prefunding failed or have technical issues, please contact our support team with the proof of transfer to complete the prefund.

## Get Balance

```shell
GET https://dev-bankaccount.aricos.co.id/api/user-balances
```

Retrieves your account balance. There are two balances: <b>CASH</b> refers to funds available for you to remit or withdraw. <b>HOLDING</b> refers to funds which are in transit.

## Get Balance Request

> Get Balance Example Request: </br>

```shell
curl --location --request GET 'https://dev-bankaccount.aricos.co.id/api/user-balances' \

--header 'Accept: application/json' \

--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5NGM5MjY0OS1hZTA2LTRmNmUtYjAzYi1iNWE0MzI3ZDBhNDgiLCJqdGkiOiJiZTcwMTJjZWIyOTNiYTJlMWNlZDE0MWI0YmZiZWExNzA5MmNiZjI5NTIyNTQzOWMyZDMzY2E4N2YwMjVmZDQ4ZTg0NTc5OGI2N2YzNWRmNiIsImlhdCI6MTY0MjY3NTYyMC42NTQ3MywibmJmIjoxNjQyNjc1NjIwLjY1NDczNywiZXhwIjoxNjc0MjExNjIwLjYzODE4OSwic3ViIjoiYWUzNjBmOTYtY2QyNi00ZWVjLWE3MWUtOTUxNmQ3ZjNmNTBhIiwic2NvcGVzIjpbXX0.faK3IffH8w5R7EEIscvnYbnhn9uQMS6206TEovhP9lgh1XUD6PubsPiyYtPWyCo_NhO-RzRI_8CHpKaMTPK9hLRUvAeNpV2CjUmM3GG2HSmgwC5a863IJoGvaGSL90aBtw-Ub3DBv1dzn00_-98982o-gSKHElsgf1o0EYGA1Y7vXEdEfN45Eww5rFG2cVUyKQo_eh8J8aITQQ15xydDsWe1lFPYYqrDIfZ6xTNa00b-GYP-DIVHP1NOYPdihOKPgt4uSzb03vfu62PFYzlR2gQiodW7Ellf-5-kIrGVRbogcZzTnBw41yKm7jU9hxx5hLgfEB5sImBMRcihER4W4GM5fLmpVQHmlOT9hTCQrtr__XEZK481OrZ75TsEYE0oaAygP2qMrlGgMYPxXvtsF9jLOrIzSmBx16mV7OeV1hytgot2KcppO-5hui5UI1kRuSY-YIY8I0y7AGX74Sq3SGQnvnesF0r5LbrxZiGP1pDUKHmn37O0SFYXT1QNEJPwwkMwVHmqsaggrl0QNejCXQRNr2eQHc1zq5umw1oTDvoxQhHTfmtyJx3zGYhKfQckoULUZs79Z0MXsqVB1n_8fFxymdagoI2EVMQ-geb0k8a9VdXTffXzAcEMD4z7ZUhx56jnNYJz62R-ZNtkxrMAOsjS3tfMje7WKoRhgOJ4HKY'
```
Our get balance end-point doesn't have any body request just send the `BEARER TOKEN`  as auth

<!--- 
Parameter | Description
--------- | -----------
account_type </br><small><span style="color:grey">*optional* </span></small> </br> <small><span style="color:grey">*default* </span> `CASH`</small> | `string` The selected account type (`CASH` or `HOLDING`). 
--->

## Get Balance Response

> Get Balance Example Response:

```shell
{
	"data": [{
		"id": "ae360f96-cd26-4eec-a71e-9516d7f3f50a",
		"email": "argjkt2@gmail.com",
		"name": "ARG_OTR",
		"balance": 8288000,
		"on_hold_balance": 870000
	}],
	"links": {
		"first": "https://dev-bankaccount.aricos.co.id/api/user-balances?page=1",
		"last": null,
		"prev": null,
		"next": null
	},
	"meta": {
		"current_page": 1,
		"from": 1,
		"path": "https://dev-bankaccount.aricos.co.id/api/user-balances",
		"per_page": 15,
		"to": 1
	}
}
```

Parameter | Description
--------- | -----------
id | The unique identity of your account
email | The user account that you use
name | The user name of your account
balance | The real balance that you can use to transfer remittance
on_hold_balance | The retained balance from accumulation of every unfinished transaction 

# Customers

## Customer Data

Customers are your end-customers, which include the sender and recipient of a remittance. You can perform recurring remittances with the same customers.

Use the following Customers API to manage your customers with Aricos. Your customers’ personal data is retained to comply with regulatory requirements for fund transfer services in Indonesia, and also allows Aricos to fulfill Know-Your-Client obligations.

## Create Customer Request

```shell
POST https://dev-bankaccount.aricos.co.id/api/customers
```

</br></br>

Create customer for your end-customers for the sender and recipient.

> Create Customer Example Request:

```shell
curl --location --request POST 'https://dev-bankaccount.aricos.co.id/api/customers' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5NGM5MjY0OS1hZTA2LTRmNmUtYjAzYi1iNWE0MzI3ZDBhNDgiLCJqdGkiOiJjNWMxNzVjMDAwOTE3ZjM3NmFlODQxN2YyNzExNzM0YzEyZTExYmIxOGNkNzBlYTMzZjRiMzM5MThmODQ5ZGIwMWMyNTA4ODI0NWEzN2M1NyIsImlhdCI6MTY0MjczMzE2Mi4yMTg2NTksIm5iZiI6MTY0MjczMzE2Mi4yMTg2NjcsImV4cCI6MTY3NDI2OTE2Mi4xOTA4NzUsInN1YiI6ImFlMzYwZjk2LWNkMjYtNGVlYy1hNzFlLTk1MTZkN2YzZjUwYSIsInNjb3BlcyI6W119.SSWzHI2hOKtWDzzwUCTqrZzs7uXK132BXmw5h_yDkIpAKQa91TdxdMTU-VhWMunmsQ8aAHRB2tlj-lyQk5P1XYXqeXCpajKgLHIL-P-r7PkXdHQmg8l8qamy_Vrz26zCtuSgD7YhqaTax7IxEXQL4mR9ixZnJ2wvUWz-lDIV0AbxxB5uQqspYcq-8kRjgMEr_wJvPcNW7gg9cPpznHIMcKP5XKpjjzvkn0LxKDkVB5mnAESpknchTdaMIeqFRQ_u3-kLuIm3Qp7Ri-4iiDY4I0N0MqGH93i-W-bOeF_MVI-CIa0AwLuBac-7gnsCVoxfi5QwJrs-pf1VbwsTTw6RSyxnFhp_DDiwC2pZFkoeyIu5hqPgq-u40wWsdHhCmXrurZJVntRDeMER_aC6nIo5WrMxSb_taqYLrzxuQ_ytht8N9ftkcIGt12xpp10jMcNzpECs5Of1Oc8cz5GudgkwOCpX98btstkVYjG-nu_QU0FI_Fxpv-XGGBJ6sbR9ZY96FRBLmjMfUEX7HPQ-HDo44TonabBvv0UhiEbTTYYman0F9PHWRctuc5Xi31m8fnWpOlRcr5dHKmOqxa2YTZgSzhMsZw2gAOXhmH49ef4TNm3ly2bbMHZqDcx6GwTa-rdIK2TZ4uXU9MwZ6fWliu3O5oKOYu2dcLQLBZyeN_BOPak' \
--data-raw '{
    "reference_id": "x-7986",
    "customer_type": "INDIVIDUAL",
    "given_name": "Cika Jerika",
    "surname": "Cijer",
    "nationality":"ID",
    "gender": "Female",
    "occupation":"OTHER",
    "address": {
        "country_code": "ID",
        "province_id": "31",
        "city_id": "3171",
        "line_1": "Jl. Senayan 1 No.15",
        "line_2": "Komplek BNI",
        "postal_code": "16320"
    },
    "date_of_birth": "11-01-1990",
    "place_of_birth": "Prabumulih",
    "identifications": [
        {
            "identification_type": "ktp",
            "identification_country": "ID",
            "identification_number": "1025456545454545"
        },
        {
            "identification_type": "npwp",
            "identification_country": "ID",
            "identification_number": "254545465425489"
        }
    ],
    "account_details": {
        "account_code": "BNI",
        "account_number": "123456789",
        "account_holder_name": "Cika Jerika"
    },
    "email": "cijer@email.com",
    "mobile": {
        "country_code": "62",
        "number": "08111555777"
    },
    "phone": {
        "country_code": "62",
        "number": "02199990000"
    },
    "fax": {
        "country_code": "62",
        "number": "02199991111"
    }
}'
```

Parameter | Description
--------- | -----------
reference_id </br><small><span style="color:grey">*required* </span></small>| `string` Your unique id for this customer. </br></br><span>`Characters` <span style="color:grey"><small>Special and alphanumeric</small></span></br><span style="color:grey">Maximum length <small>100 maximum characters</small></span>
customer_type </br><small><span style="color:grey">*required* </span></small>| `string` Legal entity. Valid values: `INDIVIDUAL` or `BUSINESS`
given_name </br><small><span style="color:grey">*conditionally required* </span></small>| `string` Given name(s). Required if `customer_type` is `INDIVIDUAL`. Only allowed if `customer_type` is `INDIVIDUAL`
surname </br><small><span style="color:grey">*required* </span></small>| `string` Surname or family name or last name. Only allowed if `customer_type` is `INDIVIDUAL`
nationality </br><small><span style="color:grey">*required* </span></small>| `string` Nationality country of the Customer. 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
gender </br><small><span style="color:grey">*required* </span></small>| `string` Gender of the Customer. Only allowed `Male` or `Female` value
occupation </br><small><span style="color:grey">*required* </span></small>| `string` Occupation of the Customer. See [Occupation Codes](#occupation-codes)
business_name </br><small><span style="color:grey">*conditionally required* </span></small>| `string` Required if `customer_type` is `BUSINESS`. Only allowed if `customer_type` is `BUSINESS`
address </br><small><span style="color:grey">*optional* </span></small>| `object` Customer's address
address.country_code </br><small><span style="color:grey">*required* </span></small>| `string` Customer’s country. 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). If `customer_type` is `BUSINESS`, the country in which the corporate entity is registered. If `customer_type` is `INDIVIDUAL`, a country in which the customer holds nationality
address.state </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s state. Download [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.province </br><small><span style="color:grey">*required* </span></small>| `string` Customer’s province. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.city </br><small><span style="color:grey">*required* </span></small>| `string` Customer’s city. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.district </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s district. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.village </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s village. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.post_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s postal code
address.line_1 </br><small><span style="color:grey">*optional* </span></small>| `string` First line of customer’s address. Typically used for building name and / or apartment number
address.line_2 </br><small><span style="color:grey">*optional* </span></small>| `string` Second line of customer’s address. Typically used for building name and / or apartment number
date_of_birth </br><small><span style="color:grey">*optional* </span></small>| `string` Date of Birth. Only allowed if `customer_type` is `INDIVIDUAL`. ISO 8601 format YYYY-MM-DD
place_of_birth </br><small><span style="color:grey">*optional* </span></small>| `string` Place of Birth. Only allowed if `customer_type` is `INDIVIDUAL`
date_of_registration </br><small><span style="color:grey">*optional* </span></small>| `string` Date of Registration. Only allowed if `customer_type` is `BUSINESS`. ISO 8601 format YYYY-MM-DD
identifications </br><small><span style="color:grey">*required* </span></small>| `object` A legal document that verifies the identity of the customer
identification.identification_type </br><small><span style="color:grey">*required* </span></small>| `string` Type of identity of the customer.</br></br> Only allowed value  `KTP`,`NPWP`,`SIM`,`PASSPORT`,`KITAS`,`KITAP`</br> `Characters` <span style="color:grey"><small>10 characters</small></span>
identification.identification_country </br><small><span style="color:grey">*required* </span></small>| `string` Country identity publisher of the customer.</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm).</br> `Characters` <span style="color:grey"><small>2 characters</small></span>
identification.identification_number </br><small><span style="color:grey">*required* </span></small>| `string` Identification number of the customer.</br></br> `Characters` <span style="color:grey"><small>15 characters for `NPWP`, 16 characters for `KTP` and other identification type</small></span>
account_details </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s bank account details
account_details.account_code </br><small><span style="color:grey">*optional* </span></small>| `string` The code of the account, can be bank codes (BCA, MANDIRI, etc.) or ewallet codes (GOPAY, OVO, etc.). Only Indonesian banks and ewallets supported currently. See [Account Codes](#account-codes)
account_details.account_number </br><small><span style="color:grey">*optional* </span></small>| `string` Destination bank account number. If disbursing to an e-wallet, phone number registered with the e-wallet account.</br></br> <span style="color:grey">`Characters` <small>Numeric and hyphens</small></br> `BCA required length` <small>10 characters</small></br>` Other banks maximum length` <small>No maximum characters</small></br> `Other banks minimum length` <small>1 character</small></br> `E-wallets` <small>Phone number registered with the e-wallet(Example: 0812XXXXXX)</small></span></br></br> <small>*** We support remittances to virtual accounts of major banks (BRI, BNI, Mandiri, CIMB Niaga, Permata, BTN, and NOBU Bank).<br> *** We support remittances to major e-wallets (GoPay, OVO, and Mandiri e-cash).</small>
account_details.account_holder_name </br><small><span style="color:grey">*optional* </span></small>| `string` Name of account holder per the bank's or e-wallet's records</br> <span style="color:grey">`Characters` <small>Special and alphanumeric</small></br> `Maximum length` <small>No maximum characters</small></br> `Minimum length` <small>1 character</small></span>
email </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s email address. Recommended if you want to notify the customer of the transaction statusShould include the top-level domain name</br> Example: abc@email.com
mobile </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s mobile number.
mobile.country_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s mobile number international  country prefix. Recommended if you want to notify the customer of the transaction status</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). Example: 62
mobile.number </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s mobile number without international prefix. Recommended if you want to notify the customer of the transaction status</br> Example: 812XXXXXX
phone </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s phone number.
phone.country_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s phone number international  country prefix. Recommended if you want to notify the customer of the transaction status</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). Example: 62
phone.number </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s phone number without international prefix. Recommended if you want to notify the customer of the transaction status</br> Example: 812XXXXXX
fax </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s fax number.
fax.country_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s fax number international  country prefix. Recommended if you want to notify the customer of the transaction status</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). Example: 62
fax.number </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s fax number without international prefix. Recommended if you want to notify the customer of the transaction status</br> Example: 812XXXXXX

## Create Customer Response

We return a customer object if the call succeeded.

### Create Customer Errors

> Create Customer Example Response:

```shell
{
    "data": {
        "id": "9564d7a6-f5d3-4dd4-911f-4d13144e8311",
        "reference_id": "x-89456",
        "customer_type": "INDIVIDUAL",
        "given_name": "Thomas Djorgi",
        "surname": "Thomdjor",
        "gender": "Female",
        "occupation": "OTHER",
        "fax": {
            "country_code": "62",
            "number": "02199991111"
        },
        "address": {
            "country_code": "ID",
            "province_id": "31",
            "city_id": "3171",
            "line_1": "Jl. Senayan 1 No.15",
            "line_2": "Komplek BNI",
            "postal_code": "16320"
        },
        "date_of_birth": "11-01-1990",
        "place_of_birth": "Prabumulih",
        "nationality": "ID",
        "identifications": [
            {
                "identification_type": "ktp",
                "identification_country": "ID",
                "identification_number": "1025456545454545"
            },
            {
                "identification_type": "npwp",
                "identification_country": "ID",
                "identification_number": "254545465425489"
            }
        ],
        "account_details": null,
        "email": "tomdjor@email.com",
        "mobile": {
            "country_code": "62",
            "number": "08111555777"
        },
        "phone": {
            "country_code": "62",
            "number": "02199990000"
        }
    }
}
```

Error Code | Description
--------- | -----------
API_VALIDATION_ERROR</br> <span class="badge">400</span>| Inputs are failing validation. The errors field contains details about which fields are violating validation</br> <span class="badge error">No retry</span>
INVALID_JSON_FORMAT</br> <span class="badge">400</span>| The request body is not a valid JSON format</br> <span class="badge error">No retry</span>
ACCOUNT_CODE_NOT_SUPPORTED_ERROR</br> <span class="badge">400</span>| The code of the account is currently not supported</br> <span class="badge error">No retry</span>
ACCOUNT_NUMBER_ERROR</br> <span class="badge">400</span>| Where account_code is “BCA”, account_number input needs to be 10 digits. Please check the account number length before retrying.</br> <span class="badge error">No retry</span>
DUPLICATE_CUSTOMER_ERROR</br> <span class="badge">400</span>| The external_id entered has been used before. Please enter a unique external_id and try again.</br> <span class="badge error">No retry</span>

## Update Customer Request

Updates an existing customer

```shell
PUT https://dev-bankaccount.aricos.co.id/api/customers/{reference_id}
```

> Update Customer Example Request:

```shell
curl --location --request PUT 'https://dev-bankaccount.aricos.co.id/api/customers/c-01256' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5MzFmODI3Ni1mOTBmLTQ0N2ItYjY0ZS1hMjI3MzQxOGVkMzIiLCJqdGkiOiIwYmE2NDcwMTNjYjE2ZTRmYjNhN2RjMGNkYTEyYjk0ZjkwZjExZmE0OWJjN2NjMDdlMmU4MjhlYzQ1MDkxYmM0NDljYjM0ZmQ0ZjVmNWIzNiIsImlhdCI6MTY0MjczOTQxMi44MzE3MjksIm5iZiI6MTY0MjczOTQxMi44MzE3MzYsImV4cCI6MTY3NDI3NTQxMi44MjI3NTQsInN1YiI6IjVhOWEyOGM2ZDRlOGMxMmFkMCIsInNjb3BlcyI6W119.X9hh_rPgAnlreqXZ-CuG-cIub0ihQc1EBNFBluCpcZcAaWJ8WXLrcl1U22etX2TUrBH5ulc7gL8XVaIV-yWSxoK98AbejjcXLzLnrLWvfphAgPmi3nYg96nIagBroVB1HVNByM8LQ8_TA0a7rp8dYqbOQ4zvUpCEPc6SVQo3kcfnxVoNiGuwTrL754kUaAcYhsqyP17m8aO8yDkVbOQzF9dMZDwMRUU_LMMufYJcTMydIIqQBGfzZOyKPTy0AivTe0icT9QmBM_YY-DgZ6sdVKosT3EsTah8Jo9FXKUPxTlDw3Fzwd8WXg6CBDPyz78F9A-n329CLosa16sILlaenBuwwAE-ObLqTVGcfYdATlWDUDDFdtKIdk4Ip2r-LxdLWfix-qF9W2_qrVmqQqIMQz7govDWSaH5pW_nu-v20deAoY5j2HDrQuPtFnd9iUm1UhmHVNOfDTInDw2EqEJ23E_S0A5CY_mgxbiu4leskFsCVVdcqWTA8aRPlUn22tILpk-SQs-NRuwDzX1Z06nuLrCnfFGGXqeLJC2LSFOf82FTHXoUyNMEkKe_uMO3vvavVw-BHoUgMoLyf5ljR4aev69OkJsmSwBXG36o7Ulu8HT514y2gsn0jJW2HSPfLEgwl0Q6e4yM6AFEIR7o_1AMdI-qf2qCg0bQlQCHEfX6RfY' \
--header 'Cookie: TS0126f9dc=01b53461a60cbb3f4b604b6067dc0e494a06a620f7e7e7fef619c6d89a06a08065941af2f434a23c7687fde6280acf1128be33d60b' \
--data-raw '{
    "reference_id": "x-7986",
    "customer_type": "INDIVIDUAL",
    "given_name": "Cika Jerika",
    "surname": "Cijer",
    "nationality":"ID",
    "gender": "Female",
    "occupation":"OTHER",
    "address": {
        "country_code": "ID",
        "province_id": "31",
        "city_id": "3171",
        "line_1": "Jl. Senayan 1 No.15",
        "line_2": "Komplek BNI",
        "postal_code": "16320"
    },
    "date_of_birth": "11-01-1990",
    "place_of_birth": "Prabumulih",
    "identifications": [
        {
            "identification_type": "ktp",
            "identification_country": "ID",
            "identification_number": "1025456545454545"
        },
        {
            "identification_type": "npwp",
            "identification_country": "ID",
            "identification_number": "254545465425489"
        }
    ],
    "account_details": {
        "account_code": "BNI",
        "account_number": "123456789",
        "account_holder_name": "Cika Jerika"
    },
    "email": "cijer@email.com",
    "mobile": {
        "country_code": "62",
        "number": "08111555777"
    },
    "phone": {
        "country_code": "62",
        "number": "02199990000"
    },
    "fax": {
        "country_code": "62",
        "number": "02199991111"
    }
}'
```

Parameter | Description
--------- | -----------
reference_id </br><small><span style="color:grey">*required* </span></small>| `string` Your unique id for this customer. </br></br><span>`Characters` <span style="color:grey"><small>Special and alphanumeric</small></span></br><span style="color:grey">Maximum length <small>100 maximum characters</small></span>
customer_type </br><small><span style="color:grey">*required* </span></small>| `string` Legal entity. Valid values: `INDIVIDUAL` or `BUSINESS`
given_name </br><small><span style="color:grey">*conditionally required* </span></small>| `string` Given name(s). Required if `customer_type` is `INDIVIDUAL`. Only allowed if `customer_type` is `INDIVIDUAL`
surname </br><small><span style="color:grey">*required* </span></small>| `string` Surname or family name or last name. Only allowed if `customer_type` is `INDIVIDUAL`
nationality </br><small><span style="color:grey">*required* </span></small>| `string` Nationality country of the Customer. 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
gender </br><small><span style="color:grey">*required* </span></small>| `string` Gender of the Customer. Only allowed `Male` or `Female` value
occupation </br><small><span style="color:grey">*required* </span></small>| `string` Occupation of the Customer. See [Occupation Codes](#occupation-codes)
business_name </br><small><span style="color:grey">*conditionally required* </span></small>| `string` Required if `customer_type` is `BUSINESS`. Only allowed if `customer_type` is `BUSINESS`
address </br><small><span style="color:grey">*optional* </span></small>| `object` Customer's address
address.country_code </br><small><span style="color:grey">*required* </span></small>| `string` Customer’s country. 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). If `customer_type` is `BUSINESS`, the country in which the corporate entity is registered. If `customer_type` is `INDIVIDUAL`, a country in which the customer holds nationality
address.state </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s state. Download [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.province </br><small><span style="color:grey">*required* </span></small>| `string` Customer’s province. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.city </br><small><span style="color:grey">*required* </span></small>| `string` Customer’s city. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.district </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s district. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.village </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s village. Download list [here](https://www.nationsonline.org/oneworld/country_code_list.htm)
address.post_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s postal code
address.line_1 </br><small><span style="color:grey">*optional* </span></small>| `string` First line of customer’s address. Typically used for building name and / or apartment number
address.line_2 </br><small><span style="color:grey">*optional* </span></small>| `string` Second line of customer’s address. Typically used for building name and / or apartment number
date_of_birth </br><small><span style="color:grey">*optional* </span></small>| `string` Date of Birth. Only allowed if `customer_type` is `INDIVIDUAL`. ISO 8601 format YYYY-MM-DD
place_of_birth </br><small><span style="color:grey">*optional* </span></small>| `string` Place of Birth. Only allowed if `customer_type` is `INDIVIDUAL`
date_of_registration </br><small><span style="color:grey">*optional* </span></small>| `string` Date of Registration. Only allowed if `customer_type` is `BUSINESS`. ISO 8601 format YYYY-MM-DD
identifications </br><small><span style="color:grey">*required* </span></small>| `object` A legal document that verifies the identity of the customer
identification.identification_type </br><small><span style="color:grey">*required* </span></small>| `string` Type of identity of the customer.</br></br> Only allowed value  `KTP`,`NPWP`,`SIM`,`PASSPORT`,`KITAS`,`KITAP`</br> `Characters` <span style="color:grey"><small>10 characters</small></span>
identification.identification_country </br><small><span style="color:grey">*required* </span></small>| `string` Country identity publisher of the customer.</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm).</br> `Characters` <span style="color:grey"><small>2 characters</small></span>
identification.identification_number </br><small><span style="color:grey">*required* </span></small>| `string` Identification number of the customer.</br></br> `Characters` <span style="color:grey"><small>15 characters for `NPWP`, 16 characters for `KTP` and other identification type</small></span>
account_details </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s bank account details
account_details.account_code </br><small><span style="color:grey">*optional* </span></small>| `string` The code of the account, can be bank codes (BCA, MANDIRI, etc.) or ewallet codes (GOPAY, OVO, etc.). Only Indonesian banks and ewallets supported currently. See [Account Codes](#account-codes)
account_details.account_number </br><small><span style="color:grey">*optional* </span></small>| `string` Destination bank account number. If disbursing to an e-wallet, phone number registered with the e-wallet account.</br></br> <span style="color:grey">`Characters` <small>Numeric and hyphens</small></br> `BCA required length` <small>10 characters</small></br>` Other banks maximum length` <small>No maximum characters</small></br> `Other banks minimum length` <small>1 character</small></br> `E-wallets` <small>Phone number registered with the e-wallet(Example: 0812XXXXXX)</small></span></br></br> <small>*** We support remittances to virtual accounts of major banks (BRI, BNI, Mandiri, CIMB Niaga, Permata, BTN, and NOBU Bank).<br> *** We support remittances to major e-wallets (GoPay, OVO, and Mandiri e-cash).</small>
account_details.account_holder_name </br><small><span style="color:grey">*optional* </span></small>| `string` Name of account holder per the bank's or e-wallet's records</br> <span style="color:grey">`Characters` <small>Special and alphanumeric</small></br> `Maximum length` <small>No maximum characters</small></br> `Minimum length` <small>1 character</small></span>
email </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s email address. Recommended if you want to notify the customer of the transaction statusShould include the top-level domain name</br> Example: abc@email.com
mobile </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s mobile number.
mobile.country_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s mobile number international  country prefix. Recommended if you want to notify the customer of the transaction status</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). Example: 62
mobile.number </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s mobile number without international prefix. Recommended if you want to notify the customer of the transaction status</br> Example: 812XXXXXX
phone </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s phone number.
phone.country_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s phone number international  country prefix. Recommended if you want to notify the customer of the transaction status</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). Example: 62
phone.number </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s phone number without international prefix. Recommended if you want to notify the customer of the transaction status</br> Example: 812XXXXXX
fax </br><small><span style="color:grey">*optional* </span></small>| `object` Customer’s fax number.
fax.country_code </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s fax number international  country prefix. Recommended if you want to notify the customer of the transaction status</br></br> 2-letter ISO 3166-2 country code. Refer to code standard [here](https://www.nationsonline.org/oneworld/country_code_list.htm). Example: 62
fax.number </br><small><span style="color:grey">*optional* </span></small>| `string` Customer’s fax number without international prefix. Recommended if you want to notify the customer of the transaction status</br> Example: 812XXXXXX

## Update Customer Response

We return the updated customer object if the call succeeded.

### Update Customer Errors

> Update Customer Example Response:

```shell
{
    "data": {
        "id": "9564d7a6-f5d3-4dd4-911f-4d13144e8311",
        "reference_id": "x-89456",
        "customer_type": "INDIVIDUAL",
        "given_name": "Thomas Djorgi",
        "surname": "Thomdjor",
        "gender": "Female",
        "occupation": "OTHER",
        "fax": {
            "country_code": "62",
            "number": "02199991111"
        },
        "address": {
            "country_code": "ID",
            "province_id": "31",
            "city_id": "3171",
            "line_1": "Jl. Senayan 1 No.15",
            "line_2": "Komplek BNI",
            "postal_code": "16320"
        },
        "date_of_birth": "11-01-1990",
        "place_of_birth": "Prabumulih",
        "nationality": "ID",
        "identifications": [
            {
                "identification_type": "ktp",
                "identification_country": "ID",
                "identification_number": "1025456545454545"
            },
            {
                "identification_type": "npwp",
                "identification_country": "ID",
                "identification_number": "254545465425489"
            }
        ],
        "account_details": null,
        "email": "tomdjor@email.com",
        "mobile": {
            "country_code": "62",
            "number": "08111555777"
        },
        "phone": {
            "country_code": "62",
            "number": "02199990000"
        }
    }
}
```

Error Code | Description
--------- | -----------
API_VALIDATION_ERROR</br> <span class="badge">400</span>| Inputs are failing validation. The errors field contains details about which fields are violating validation</br> <span class="badge error">No retry</span>
INVALID_JSON_FORMAT</br> <span class="badge">400</span>| The request body is not a valid JSON format</br> <span class="badge error">No retry</span>
ACCOUNT_CODE_NOT_SUPPORTED_ERROR</br> <span class="badge">400</span>| The code of the account is currently not supported</br> <span class="badge error">No retry</span>
ACCOUNT_NUMBER_ERROR</br> <span class="badge">400</span>| Where account_code is “BCA”, account_number input needs to be 10 digits. Please check the account number length before retrying.</br> <span class="badge error">No retry</span>
DUPLICATE_CUSTOMER_ERROR</br> <span class="badge">400</span>| The external_id entered has been used before. Please enter a unique external_id and try again.</br> <span class="badge error">No retry</span>
CUSTOMER_NOT_FOUND_ERROR</br> <span class="badge">400</span>| Could not find customer.</br> <span class="badge error">No retry</span>

## Get Customer With external_id Request

```shell
GET https://dev-bankaccount.aricos.co.id/api/customers/{reference_id}
```

Returns an array with a single object which contains the customer corresponding to the unique external_id. Returns an empty array if there is no customer corresponding to the external_id.

> Get Customer With external_id Example Request:

```shell
curl --location --request GET 'https://dev-bankaccount.aricos.co.id/api/customers/x-7986' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5NGM5MjY0OS1hZTA2LTRmNmUtYjAzYi1iNWE0MzI3ZDBhNDgiLCJqdGkiOiJjNWMxNzVjMDAwOTE3ZjM3NmFlODQxN2YyNzExNzM0YzEyZTExYmIxOGNkNzBlYTMzZjRiMzM5MThmODQ5ZGIwMWMyNTA4ODI0NWEzN2M1NyIsImlhdCI6MTY0MjczMzE2Mi4yMTg2NTksIm5iZiI6MTY0MjczMzE2Mi4yMTg2NjcsImV4cCI6MTY3NDI2OTE2Mi4xOTA4NzUsInN1YiI6ImFlMzYwZjk2LWNkMjYtNGVlYy1hNzFlLTk1MTZkN2YzZjUwYSIsInNjb3BlcyI6W119.SSWzHI2hOKtWDzzwUCTqrZzs7uXK132BXmw5h_yDkIpAKQa91TdxdMTU-VhWMunmsQ8aAHRB2tlj-lyQk5P1XYXqeXCpajKgLHIL-P-r7PkXdHQmg8l8qamy_Vrz26zCtuSgD7YhqaTax7IxEXQL4mR9ixZnJ2wvUWz-lDIV0AbxxB5uQqspYcq-8kRjgMEr_wJvPcNW7gg9cPpznHIMcKP5XKpjjzvkn0LxKDkVB5mnAESpknchTdaMIeqFRQ_u3-kLuIm3Qp7Ri-4iiDY4I0N0MqGH93i-W-bOeF_MVI-CIa0AwLuBac-7gnsCVoxfi5QwJrs-pf1VbwsTTw6RSyxnFhp_DDiwC2pZFkoeyIu5hqPgq-u40wWsdHhCmXrurZJVntRDeMER_aC6nIo5WrMxSb_taqYLrzxuQ_ytht8N9ftkcIGt12xpp10jMcNzpECs5Of1Oc8cz5GudgkwOCpX98btstkVYjG-nu_QU0FI_Fxpv-XGGBJ6sbR9ZY96FRBLmjMfUEX7HPQ-HDo44TonabBvv0UhiEbTTYYman0F9PHWRctuc5Xi31m8fnWpOlRcr5dHKmOqxa2YTZgSzhMsZw2gAOXhmH49ef4TNm3ly2bbMHZqDcx6GwTa-rdIK2TZ4uXU9MwZ6fWliu3O5oKOYu2dcLQLBZyeN_BOPak'
```

Query Parameter | Description
--------- | -----------
external_id </br><small><span style="color:grey">*optional* </span></small>| `string` Unique ID you provided in the Create Customer request</br> <span style="color:grey"><small>The external_id must match the external_id used at customer creation precisely</small></span>

> Get Customer With external_id Example Response:

```shell
{
    "data": {
        "id": "9560ea7c-a505-47a9-8482-c2063ba64ae7",
        "reference_id": "x-7986",
        "customer_type": "INDIVIDUAL",
        "given_name": "Cika Jerika",
        "surname": "Cijer",
        "gender": "Female",
        "occupation": "OTHER",
        "fax": {
            "number": "02199991111",
            "country_code": "62"
        },
        "address": {
            "country_code": "ID",
            "province_id": "31",
            "city_id": "3171",
            "line_1": "Jl. Senayan 1 No.15",
            "line_2": "Komplek BNI",
            "postal_code": "16320"
        },
        "date_of_birth": "1990-11-01",
        "place_of_birth": "Prabumulih",
        "nationality": "ID",
        "identifications": [
            {
                "identification_type": "ktp",
                "identification_number": "1025456545454545",
                "identification_country": "ID"
            },
            {
                "identification_type": "npwp",
                "identification_number": "254545465425489",
                "identification_country": "ID"
            }
        ],
        "account_details": {
            "id": "9560ea7c-ad42-4ef9-8d71-39a42f24d1c5",
            "account_code": "BNI",
            "account_number": "123456789",
            "account_holder_name": "Cika Jerika"
        },
        "email": "cijer@email.com",
        "mobile": {
            "country_code": "62",
            "number": "08111555777"
        },
        "phone": {
            "country_code": "62",
            "number": "02199990000"
        }
    }
}
```

# Bank Account Remittance

Our Bank Account Remittance APIs allow you to send remittances from your Aricos Account on behalf of a sender to your designated recipient. Only IDR-IDR transfers supported currently.

<aside class="notice">
   Please note that you are unable to cancel a remittance request once it has been made.
</aside>

## Create Remittance

```shell
POST https://dev-bankaccount.aricos.co.id/api/remittances
```

Sends a new remittance from your Aricos Account to a recipient. You’ll need to have created a customer representing the sender and a customer representing the recipient first.

Your Aricos account balance must be able to cover the payout amount and the transaction fees, or you’ll receive an “Insufficient Balance” error.

## Create Remittance Request

> Create Remittance Example Request:

```shell
curl --location --request POST 'https://dev-bankaccount.aricos.co.id/api/remittances' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5NGM5MjY0OS1hZTA2LTRmNmUtYjAzYi1iNWE0MzI3ZDBhNDgiLCJqdGkiOiJjNWMxNzVjMDAwOTE3ZjM3NmFlODQxN2YyNzExNzM0YzEyZTExYmIxOGNkNzBlYTMzZjRiMzM5MThmODQ5ZGIwMWMyNTA4ODI0NWEzN2M1NyIsImlhdCI6MTY0MjczMzE2Mi4yMTg2NTksIm5iZiI6MTY0MjczMzE2Mi4yMTg2NjcsImV4cCI6MTY3NDI2OTE2Mi4xOTA4NzUsInN1YiI6ImFlMzYwZjk2LWNkMjYtNGVlYy1hNzFlLTk1MTZkN2YzZjUwYSIsInNjb3BlcyI6W119.SSWzHI2hOKtWDzzwUCTqrZzs7uXK132BXmw5h_yDkIpAKQa91TdxdMTU-VhWMunmsQ8aAHRB2tlj-lyQk5P1XYXqeXCpajKgLHIL-P-r7PkXdHQmg8l8qamy_Vrz26zCtuSgD7YhqaTax7IxEXQL4mR9ixZnJ2wvUWz-lDIV0AbxxB5uQqspYcq-8kRjgMEr_wJvPcNW7gg9cPpznHIMcKP5XKpjjzvkn0LxKDkVB5mnAESpknchTdaMIeqFRQ_u3-kLuIm3Qp7Ri-4iiDY4I0N0MqGH93i-W-bOeF_MVI-CIa0AwLuBac-7gnsCVoxfi5QwJrs-pf1VbwsTTw6RSyxnFhp_DDiwC2pZFkoeyIu5hqPgq-u40wWsdHhCmXrurZJVntRDeMER_aC6nIo5WrMxSb_taqYLrzxuQ_ytht8N9ftkcIGt12xpp10jMcNzpECs5Of1Oc8cz5GudgkwOCpX98btstkVYjG-nu_QU0FI_Fxpv-XGGBJ6sbR9ZY96FRBLmjMfUEX7HPQ-HDo44TonabBvv0UhiEbTTYYman0F9PHWRctuc5Xi31m8fnWpOlRcr5dHKmOqxa2YTZgSzhMsZw2gAOXhmH49ef4TNm3ly2bbMHZqDcx6GwTa-rdIK2TZ4uXU9MwZ6fWliu3O5oKOYu2dcLQLBZyeN_BOPak' \
--data-raw '{
    "reference_id": "XXX-3344",
    "method": "A2C",
    "amount": 50000,
    "purpose_code": "FAMILY",
    "source_of_funds": "PERSONAL_SAVINGS",
    "description": "Transfer untuk ibu",
    "sender_customer_id": "9564d736-8852-4e4a-ad8a-0f40d14acb69",
    "recipient_customer_id": "9564d7a6-f5d3-4dd4-911f-4d13144e8311",
    "agent_id": "0620b618-b2ab-46cf-ab23-679a78945b5e"
}'
   ```

Parameter | Description
--------- | -----------
external_id </br><small><span style="color:grey">*required* </span></small>| `string` A unique ID for your remittance. We validate this to protect against accidental duplicate remittances.</br></br> <span style="color:grey">`Characters` <small>Special and alphanumeric</small></br> `Maximum length` <small>100 characters</small></span>
method </br><small><span style="color:grey">*required* </span></small>| `string` A fix value method flag for Bank Account Transaction. We validate this to make sure your remittance run in `Bank Account`  transaction.</br></br> <span style="color:grey">Use Fix Value `A2A` <small>always use the fix value when sending remittance request</small></span>
amount </br><small><span style="color:grey">*required* </span></small>| `number` Transfer amount</br></br> <span style="color:grey">`Characters` <small>Numerical integers, no decimals</small></br> `Maximum limit (BCA, Mandiri, BRI, BNI, BNI Syariah, CIMB, CIMB_UUS, PERMATA)` <small>No Limit**</small></br> `Minimum limit (BCA, Mandiri, BRI, BNI, BNI Syariah, CIMB, CIMB_UUS, PERMATA)` <small>No Limit**</small></br> `Maximum limit (Other banks)` <small>Rp.50.000.000***</small></br> `Minimum limit (Other banks)` <small>Rp. 10.000</small></br></br></span> <small>** While there is theoretically no maximum transfer limit for transfers to these banks, please note that we may have to report all transaction amounts above Rp 100.000.000 to the financial authorities in Indonesia along with supporting documentation regarding the underlying transactions.</small></br></br> <small>*** Disbursements above Rp 50.000.000 to banks other than BCA, Mandiri, BNI, BNI Syariah, BRI, Permata will be processed between 8am-2pm (UTC+07:00) on bank working days. The disbursement can be expected to arrive by the next business day. (Processing times vary by financial institution and is subject to change.)</small>
description </br><small><span style="color:grey">*required* </span></small>| `string` Description to send with the remittance. The recipient may see this e.g., in their bank statement (if supported) or in email receipts we send on your behalf.</br></br> <span style="color:grey">`Maximum length` <small>512 characters</small></br></br></span> <small></span>
sender_customer_id </br><small><span style="color:grey">*required* </span></small>| `string` The id of the sender customer (as returned by Aricos’s Create Customer endpoint).</br></br> The following fields are required in the sender customer object: `given_name` OR `business_name`, `customer_type`, `country_code`
recipient_customer_id </br><small><span style="color:grey">*required* </span></small>| `string` The id of the recipient customer (as returned by Aricos's Create Customer endpoint).</br></br> The following fields are required in the recipient customer object: `given_name` OR `business_name`, `customer_type`, `country_code`, `account_code`, `account_number`, `account_holder_name`
source_of_funds </br><small><span style="color:grey">*required* </span></small>| `string` Source of funds. Refer to our list of [Source of Funds Codes](#source-of-funds)
purpose_code </br><small><span style="color:grey">*required* </span></small>| `string` Purpose of the remittance. Refer to our list of [Purpose Codes](#purpose-codes)
agent_id </br><small><span style="color:grey">*required* </span></small>| `string` The destination Bank ID of your remittance. Refer to our list of [Bank Lists](#bank-lists)

## Create Remittance Response

> Create Remittance Example Response:

```shell
{
    "data": {
        "id": "956685f1-e12b-4085-ba72-5b66ab568eb9",
        "reference_id": "1638158760806-54",
        "method": "A2A",
        "amount": 90000,
        "purpose_code": "FAMILY",
        "source_of_funds": "PERSONAL_SAVINGS",
        "description": "Transfer ke kampung",
        "transaction_status": "PENDING_RISK_ASSESSMENT",
        "sender": {
            "id": "9560ea7c-a505-47a9-8482-c2063ba64ae7",
            "reference_id": "x-7986",
            "customer_type": "INDIVIDUAL",
            "given_name": "Cika Jerika",
            "surname": "Cijer",
            "gender": "Female",
            "occupation": "OTHER",
            "fax": {
                "number": "02199991111",
                "country_code": "62"
            },
            "address": {
                "country_code": "ID",
                "province_id": "31",
                "city_id": "3171",
                "line_1": "Jl. Senayan 1 No.15",
                "line_2": "Komplek BNI",
                "postal_code": "16320"
            },
            "date_of_birth": "1990-11-01",
            "place_of_birth": "Prabumulih",
            "nationality": "ID",
            "identifications": [
                {
                    "identification_type": "ktp",
                    "identification_number": "1025456545454545",
                    "identification_country": "ID"
                },
                {
                    "identification_type": "npwp",
                    "identification_number": "254545465425489",
                    "identification_country": "ID"
                }
            ],
            "account_details": {
                "id": "9560ea7c-ad42-4ef9-8d71-39a42f24d1c5",
                "account_code": "BNI",
                "account_number": "123456789",
                "account_holder_name": "Cika Jerika"
            },
            "email": "cijer@email.com",
            "mobile": {
                "country_code": "62",
                "number": "08111555777"
            },
            "phone": {
                "country_code": "62",
                "number": "02199990000"
            }
        },
        "recipient": {
            "id": "9560e576-28b1-4fe2-9c7c-fb75f5fe40a0",
            "reference_id": "x-7984",
            "customer_type": "INDIVIDUAL",
            "given_name": "Mamang Daya",
            "surname": "Mangday",
            "gender": "Male",
            "occupation": "PILOT",
            "fax": {
                "number": "02199991111",
                "country_code": "62"
            },
            "address": {
                "country_code": "ID",
                "province_id": "31",
                "city_id": "3171",
                "line_1": "Jl. Senayan 1 No.15",
                "line_2": "Komplek BNI",
                "postal_code": "16320"
            },
            "date_of_birth": "1990-11-01",
            "place_of_birth": "Prabumulih",
            "nationality": "ID",
            "identifications": [
                {
                    "identification_type": "ktp",
                    "identification_number": "1025456545454545",
                    "identification_country": "ID"
                },
                {
                    "identification_type": "npwp",
                    "identification_number": "254545465425489",
                    "identification_country": "ID"
                }
            ],
            "account_details": {
                "id": "9560e576-2efa-4e7a-8553-567bfdbaf3e8",
                "account_code": "BNI",
                "account_number": "00987654321",
                "account_holder_name": "Mamang Daya"
            },
            "email": "dewi@email.com",
            "mobile": {
                "country_code": "62",
                "number": "08111555777"
            },
            "phone": {
                "country_code": "62",
                "number": "02199990000"
            }
        }
    }
}
```

We return a response with additional fields described below if there were no initial errors with the remittance creation (request formatted incorrectly, invalid purpose code, insufficient funds, etc). The status of the remittance will be initially marked as `PENDING_RISK_ASSESSMENT`.

Parameter | Description
--------- | -----------
status | `string` Status of the remittance. Default is `PENDING_RISK_ASSESSMENT`: Request is being processed and assessed in the risk scoring system. See [Remittance Statuses](#remittance-statuses)
created | `string` An ISO timestamp that tracks when the remittance was created
updated | `string` An ISO timestamp that tracks when the remittance was updated
id | `string` Unique remittance ID

### Create Remittance Errors

Error Code | Description
--------- | -----------
API_VALIDATION_ERROR</br> <span class="badge">400</span>| Inputs are failing validation. The errors field contains details about which fields are violating validation.</br> <span class="badge error">No retry</span>
INVALID_JSON_FORMAT</br> <span class="badge">400</span>| The request body is not a valid JSON format.</br> <span class="badge error">No retry</span>
DUPLICATE_REMITTANCE_ERROR</br> <span class="badge">400</span>| External ID has been used before. Use a unique External ID and try again.</br> <span class="badge error">No retry</span>
RECIPIENT_AMOUNT_ERROR</br> <span class="badge">400</span>| The transfer amount requested is lower than the prescribed minimum for the recipient bank. Amend the transfer amount before retrying.</br> <span class="badge error">No retry</span>
MAXIMUM_TRANSFER_LIMIT_ERROR</br> <span class="badge">400</span>| The transfer amount requested is higher than the prescribed maximum for the recipient bank. Amend the transfer amount before retrying.</br> <span class="badge error">No retry</span>
SENDER_CUSTOMER_VALIDATION_ERROR</br> <span class="badge">400</span>| There are missing inputs for this customer which are required for the remittance. The errors field contains details about which fields are violating validation.</br> <span class="badge error">No retry</span>
RECIPIENT_CUSTOMER_VALIDATION_ERROR</br> <span class="badge">400</span>| There are missing inputs for this customer which are required for the remittance. The errors field contains details about which fields are violating validation.</br> <span class="badge error">No retry</span>
SENDER_CUSTOMER_NOT_FOUND_ERROR</br> <span class="badge">400</span>| Could not find customer.</br> <span class="badge error">No retry</span>
RECIPIENT_CUSTOMER_NOT_FOUND_ERROR</br> <span class="badge">400</span>| Could not find customer.</br> <span class="badge error">No retry</span>
SERVER_ERROR</br> <span class="badge">500</span>| Error connecting to our server. Please use Get remittance by external_id API to check whether the remittance has already been created. If you receive an empty array, the remittance has not been created; please retry the remittance request in 1-2 hours.</br> <span class="badge error">No retry</span>

## Get Remittance With external_id Request

```shell
GET https://dev-bankaccount.aricos.co.id/api/remittances/{external_id}
```

Returns an array with a single object which contains the remittance corresponding to the unique external_id. Returns an empty array if there is no remittance corresponding to the external_id.

> Get Customer With external_id Example Request:

```shell
curl --location --request GET 'https://dev-bankaccount.aricos.co.id/api/remittances/XXX-2233' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5NGM5MjY0OS1hZTA2LTRmNmUtYjAzYi1iNWE0MzI3ZDBhNDgiLCJqdGkiOiJjNWMxNzVjMDAwOTE3ZjM3NmFlODQxN2YyNzExNzM0YzEyZTExYmIxOGNkNzBlYTMzZjRiMzM5MThmODQ5ZGIwMWMyNTA4ODI0NWEzN2M1NyIsImlhdCI6MTY0MjczMzE2Mi4yMTg2NTksIm5iZiI6MTY0MjczMzE2Mi4yMTg2NjcsImV4cCI6MTY3NDI2OTE2Mi4xOTA4NzUsInN1YiI6ImFlMzYwZjk2LWNkMjYtNGVlYy1hNzFlLTk1MTZkN2YzZjUwYSIsInNjb3BlcyI6W119.SSWzHI2hOKtWDzzwUCTqrZzs7uXK132BXmw5h_yDkIpAKQa91TdxdMTU-VhWMunmsQ8aAHRB2tlj-lyQk5P1XYXqeXCpajKgLHIL-P-r7PkXdHQmg8l8qamy_Vrz26zCtuSgD7YhqaTax7IxEXQL4mR9ixZnJ2wvUWz-lDIV0AbxxB5uQqspYcq-8kRjgMEr_wJvPcNW7gg9cPpznHIMcKP5XKpjjzvkn0LxKDkVB5mnAESpknchTdaMIeqFRQ_u3-kLuIm3Qp7Ri-4iiDY4I0N0MqGH93i-W-bOeF_MVI-CIa0AwLuBac-7gnsCVoxfi5QwJrs-pf1VbwsTTw6RSyxnFhp_DDiwC2pZFkoeyIu5hqPgq-u40wWsdHhCmXrurZJVntRDeMER_aC6nIo5WrMxSb_taqYLrzxuQ_ytht8N9ftkcIGt12xpp10jMcNzpECs5Of1Oc8cz5GudgkwOCpX98btstkVYjG-nu_QU0FI_Fxpv-XGGBJ6sbR9ZY96FRBLmjMfUEX7HPQ-HDo44TonabBvv0UhiEbTTYYman0F9PHWRctuc5Xi31m8fnWpOlRcr5dHKmOqxa2YTZgSzhMsZw2gAOXhmH49ef4TNm3ly2bbMHZqDcx6GwTa-rdIK2TZ4uXU9MwZ6fWliu3O5oKOYu2dcLQLBZyeN_BOPak'
```

> Get Remittance With external_id Example Response:

```shell
{
	"status": "PENDING_RISK_ASSESSMENT",
	"external_id": "XXX10",
	"amount": 300000,
	"purpose_code": "FAMILY",
	"source_of_funds": "PERSONAL_SAVINGS",
	"description": "Transfer ke kampung via Bank Account",
	"sender_customer_id": "de7ae696-f7b8-4576-ac41ad8bdf680704",
	"recipient_customer_id": "a6f19ba7-cc86-4747-a9de125eebbb074f",
	"created": "2022-01-06T15:16:51.505Z",
	"updated": "2022-01-06T15:16:51.505Z",
	"id": "61d707e3914969153a346ca3"
}
```

Parameter | Description
--------- | -----------
external_id </br><small><span style="color:grey">*required* </span></small>| `string` Unique ID you provided in the Create Remittance request</br> <span style="color:grey"><small>The external_id must match the external_id used at remittance creation precisely</small></span>
