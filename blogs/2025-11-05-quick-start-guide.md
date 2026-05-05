---
title: "Quick Start Guide"
url: "https://developer.shell.com/api-catalog/b2b-mobility-card-pin-management/quick-start-guide-13"
date: "Wed, 05 Nov 2025 05:56:57 +0000"
author: "Anonymous"
feed_url: "https://developer.shell.com/rss.xml"
---
<span>Quick Start Guide</span>

            <div class="has-button has-list field field--body field--label-hidden field__item"><h2>Getting Started with B2B Shell Card Pin Management</h2>
<p>B2B Shell Card Pin Management </p>
<p>Shell Card pin management has been updated with 2 major steps to be followed. </p>
<ol>
<li>Get the public RSA Key </li>
<li>Encrypt the desired pin along with the RSA Key in Shell provided encryption logic. </li>
<li>Send the encrypted values when ordering cards using our order card API. </li>
</ol>
<p>More detailed explanation is provided in this guide along with the clear representation of the flows. </p>
<div class="mermaid">
<p>sequenceDiagram
participant PartnerApplication 
participant Shell Authentication
participant Shell API
participant Shell Code Library
autonumber
alt Manual Process
rect rgb(200, 150, 255)
PartnerApplication -&gt;&gt;Shell Authentication: Request Client ID and Client Secret
activate Shell Authentication
Shell Authentication -&gt;&gt; PartnerApplication : Generate and provide Client ID and Client Secret
deactivate Shell Authentication
end
end
alt Authentication/Authorization
rect rgb(191, 223, 255)
PartnerApplication -&gt;&gt;Shell Authentication: Inititate request to OAuth end point
activate Shell Authentication
Note right of PartnerApplication: Client ID and Secret
Shell Authentication -&gt;&gt; PartnerApplication : (200-OK) Returns Bearer Token
deactivate Shell Authentication
Note left of Shell Authentication: Access Token
end
end
alt  pin-management/v1/generatepinkeys
rect rgb(200, 150, 255)
PartnerApplication -&gt;&gt;Shell API: Initiate request to get the public RSA key to encrypt PIN
activate Shell API
Note right of PartnerApplication: Access Token
Shell API -&gt;&gt; PartnerApplication : Returns a response on validation of the bearer token with RSA key
deactivate Shell API
Note left of Shell API: UID, value
end
end
alt  Shell PIN Encrypt Code Library 
rect rgb(191, 223, 255)
PartnerApplication -&gt;&gt; Shell Code Library: Use Code library provided by Shell to encrypt the PIN
activate Shell Code Library
Note right of PartnerApplication: UID, value, pin (which user wants to use)
Shell Code Library -&gt;&gt; PartnerApplication: Get all the encoded values after encryption 
deactivate Shell Code Library
Note left of Shell Code Library: UID, Encrypted base64 encoded message, Encrypted base64 encoded Details
end
end
alt  ONLY in UAT to test
rect rgb(200, 150, 255)
PartnerApplication -&gt;&gt;Shell API: Initiate request to pin-management/v1/validatepin API to verify the PIN encryption
activate Shell API
Note right of PartnerApplication: Access Token, UID, Encrypted base64 encoded message, Encrypted base64 encoded Details
Shell API -&gt;&gt; PartnerApplication : Returns a response with the pin used during encryption
deactivate Shell API
Note left of Shell API: pin
end
end
alt  card-management/v2/ordercard
rect rgb(191, 223, 255)
PartnerApplication -&gt;&gt;Shell API: Initiate request to order card along with the encrypted details<br />
activate Shell API
Note right of PartnerApplication: UID, Encrypted base64 encoded message, Encrypted base64 encoded Details
Shell API -&gt;&gt; PartnerApplication : Returns a response on validation for ordering card
deactivate Shell API
Note left of Shell API: CardReferences, OrderReference
end
end</p>
</div> 
<h2>Authentication</h2>
<p>Shell API’s are secured by OAuth 2.0. It uses the 'Client Credentials' Grant Type to allow the API consumer to access data. The end to end process is illustrated in the sequence diagram below.</p>
<p>This step is to generate the API Access Token using the unique Client ID and Client Secret provided by Shell. (Please note that this credentials is to validate the API request between Shell and its partner so its system to system access token)</p>
<h3>Key Request Parameters</h3>
<p>Once you receive the client ID &amp; Secret, next step is to call the <a href="https://api-test.shell.com/v1/oauth/token">https://api-test.shell.com/v1/oauth/token</a> endpoint to authenticate. Following are the key parameters-</p>
<ul>
<li>Method: POST</li>
<li>Authorization Type: OAuth 2.0</li>
<li>Auth URI: <a href="https://api-test.shell.com/v1/oauth/token">https://api-test.shell.com/v1/oauth/token</a></li>
<li>Client_Id: <strong>****</strong> (OAuth Client ID)</li>
<li>Client Secret: <strong>****</strong> (OAuth Client Secret)</li>
<li>Grant Type: client_credentials</li>
</ul>
<h3>Sample cURL Request</h3>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/v1/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'client_id=***********' \
--data-urlencode 'client_secret=*************' \
--data-urlencode 'grant_type=client_credentials'</code></pre>
<p>On receiving the request Shell Authorization system will verify all the parameters in the request and, if everything checks out, it will generate your access token and return it in the response.</p>
<h3>Sample Response</h3>
<pre><code class="language-json">{
    "access_token": "***********",
    "token_type": "Bearer",
    "expires_in": 899
}</code></pre>
<p>The response will contain the following parameters:</p>
<ul>
<li>access_token: The token to be used to call the functional APIs</li>
<li>expires_in: The amount of seconds until the access token expires.</li>
<li>token_type: Bearer</li>
</ul>
<h3>Exception Handling</h3>
<p>All error scenarios are returned with a response body and identifier.</p>
<pre><code class="language-json">{
      "error_descrription": "invalid client or client credentials",
      "error": "invalid_client"
}</code></pre>
<table>
<thead>
<tr>
<th>HTTP Code</th>
<th>Description</th>
<th>Scenarios</th>
</tr>
</thead>
<tbody>
<tr>
<td>400</td>
<td>Bad Request</td>
<td>If Invalid scope passed to Token url</td>
</tr>
<tr>
<td></td>
<td></td>
<td>Invalid grant type passed to Token url</td>
</tr>
<tr>
<td>401</td>
<td>Unauthorized</td>
<td>If Invalid id/secret passed to Token url</td>
</tr>
<tr>
<td></td>
<td></td>
<td>If Invalid or expired token passed to destination system’s API</td>
</tr>
</tbody>
</table>
<h2>Get Public RSA Key</h2>
<p>In this step a public RSA Key is generated which needs to be used in the pin encryption code library.</p>
<p>Only the authorization token need to be passed in this end point which will verify the user and provide 2 parameters in the response </p>
<ul>
<li>UUID  - Unique identifier generated for the request</li>
<li>Value - Base64 encoded RSA public key in PEM format</li>
</ul>
<h3>Key Request Parameters</h3>
<ul>
<li>Method: GET</li>
<li>Authorization Type: OAuth 2.0</li>
<li>Auth URI: <a href="https://api-test.shell.com/test/pin-management/v1/generatepinkeys">https://api-test.shell.com/test/pin-management/v1/generatepinkeys</a></li>
</ul>
<h3>Sample cURL Request</h3>
<pre><code class="language-curl">curl --location --request GET 'https://api-test.shell.com/test/pin-management/v1/generatepinkeys' \
--header 'Authorization: Bearer **************' </code></pre>
<h3>Sample Response</h3>
<pre><code class="language-json">{
    "uid": "2K83*******USsyHEnE8E1u979",
    "value": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQ0lEQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FnMEFNSUlDQ0FLQ0FnRUEyb2dVM0I2U0sxLytudy9IZUFwUwp4WDBDb1FCVTVKZXhMRThWc2F1KzA2RFBabURZZWwvNmtNYXYrallVTzllR1cvczVUemI1Zm1wVGI5WF***************************xWUV6ZXlVemNGb0cKVmxDODd1dW8wZDNad1Vnd0d5R1FQZEEzUFkzazNIQlhaN3J3Nm5udWtWdXlkTWRUUE5oUVpJbVB1aEFQV3g1SAo4eG80SEJDMDZ1aENsYm1xZ0dJM2tFWWZ4QXIvVm5hWUN1ckJZUm1NYTYwTmlteGcrZHlwVENTdS80ajQ3VnF0CldFaEp3Y2FhbTF1MkxiV3RWZGhwbDdjQ0FRTT0KLS0tLS1FTkQgUFVCTElDIEtFWS0tLS0tCg=="
}</code></pre>
<h2>Encyrpt the desired PIN using Shell Code Library</h2>
<p>Shell provides the technical solution in order to encrypt the desired PIN for the user using the Shell Code Library available in 
3 programming languages</p>
<ul>
<li>Javascript (Node.js)</li>
<li>C#</li>
<li>Java</li>
</ul>
<p>Also provided with the library is a simple HTML page which runs the library and prints the output for your reference. </p>
<p>The Code libraries for all above 3 languages can be downloaded from here - <a href="https://developer.shell.com/api-catalog/b2b-mobility-card-pin-management/code-libraries">Shell ePin Code Libraries</a></p>
<h3>Key Request Parameters</h3>
<p>The key parameters to be passed into the code library are </p>
<ol>
<li>UUID</li>
<li>Value (RSA Public Key)</li>
<li>PIN</li>
</ol>
<p><strong>Note</strong>: </p>
<ol>
<li>UUID and Value passed in the library needs to be generated from the previous step using endpoint - /generatepinkeys</li>
<li>Please note that there are set of Weak PIN validations that are recommeneded from Shell. </li>
</ol>
<h3>Key Response Parameters</h3>
<p>Once the code library is saved with all the above 3 values passed, then the HTML page needs to be opened in order to view the output. Below parameters are provided in the response. </p>
<ol>
<li>RSA public key UID</li>
<li>Encrypted base64 encoded message</li>
<li>Encrypted base64 encoded details</li>
</ol>
<h2>Verify the encrypted PIN</h2>
<pre><code class="language-diff">! Please note this process to verify the encyption is availbale strictly only in UAT environment</code></pre>
<p>In order to verify the encryption was executed as per Shell logic, this end point can be used in order to view the PIN. </p>
<h3>Key Request Parameters</h3>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/pin-management/v1/validatepin">https://api-test.shell.com/test/pin-management/v1/validatepin</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>Content-Type   : application/json </li>
</ul>
</li>
<li>Body : <ul>
<li>uid : Unique identifier for the request.</li>
<li>encrypted_pin : Base64 encoded and encrypted PIN block.</li>
<li>session_key : Base64 encoded and encrypted details for decryption.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/pin-management/v1/validatepin' \
--header 'Authorization: Bearer ' \
--header 'Content-Type: application/json' \
--data-raw '{
    "uid": "2K86mSOt4tHd*******6Ld5KpC1m1GKjI0",
    "encrypted_pin": "i+Qib**********ldxZsmpvpkS7fqynjjPd3KtLA+V5XtgXXwBrH1zTadMtF0+ks=",
    "session_key": "KZ8EHcq4gVuw8iGKPL4RqK2nH0R0P70iMj3IN8ZCxpgMmhJnPvAXSCoaLgURd943XlX9GpKlzhKkd/VIot2o3sN5P6lTpv1KVYWE6wrDiNpsWO2TVhvoD0+************+sYswJpGomiMkaF+Zq9CIveGFmhGU0csZa9+14X60eu2VMb4Q5JKcmydISxJ/61F3a5Xex6+IC1Cs3MeHBn55ayZcCSdkSSuvXB+R/aG84xSKmwUyWmmXstTNuYYIOiiNkCVtA1Wo1XQprGEJcGQ2FqlidFifeqX/*********+QIeo7VXv1Uu0zuBFj4fYuHOF4wAXL3u25JjK+PKUDXjAyAqq0h4C5jNnRLbNCM9yQKhFl3ayiiBtVRGe1P/YPedCXeRu8aRC6qnjSfzm8LlSiV8C7+27TP8f4zj/MuBC0CcZQ0XS2SbrVV93wTzbFBXQB3wir6z79eGZfshi1KGeB+lmRYTtTBTs2TBwiMVSO/be7ixf9XlgAESfN6FF7lP+yvKW1FtrJO8ZQBKKhJ9UZtKe4e/y70yNLQE/F8T/GrH6ebP+aUclLga0qIjIzi1hRX2dm4UhGiK23xfKuZKc7q3NGiX+Nm2Fd8="
}'
</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "pin": "1920"
}
</code></pre>
<h4>Error Response</h4>
<p>502 Bad Request - Returned when the user submits invalid or malformed encryption data.</p>
<h2>Order Card using the encrypted values</h2>
<p>Once the encryption is done all the below 3 parameters need to be included in the Order Card endpoint in order to receive the Shell card with the requested PIN.  </p>
<table>
<thead>
<tr>
<th>Parameters in Shell Code Library</th>
<th>Parameters in Card Order API</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>uid</td>
<td>SelfSelectedPINKeyID</td>
<td>Unique identifier for the request</td>
</tr>
<tr>
<td>encrypted_pin</td>
<td>SelfSelectedEncryptedPIN</td>
<td>Base64 encoded and encrypted PIN block</td>
</tr>
<tr>
<td>session_key</td>
<td>SelfSelectedPINSessionKey</td>
<td>Base64 encoded and encrypted details for decryption</td>
</tr>
</tbody>
</table>
<h3>Key Request Parameters</h3>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/fleetmanagement/v2/card/OrderCard">https://api-test.shell.com/test/fleetmanagement/v2/card/OrderCard</a></li>
<li>Headers :<ul>
<li>Authorization  : Uses Basic Authorization Scheme Passing base64 encoded ConsumerKey + Secret as Authorization.</li>
<li>apikey         : This is the API key of the specific environment which needs to be passed by the API client.</li>
<li>Content-Type   : application/json </li>
</ul>
</li>
<li>Body : <ul>
<li>SelfSelectedPINKeyID : Unique identifier for the request (uid)</li>
<li>SelfSelectedEncryptedPIN  : Base64 encoded and encrypted PIN block (encrypted_pin)</li>
<li>SelfSelectedPINSessionKey  : Base64 encoded and encrypted details for decryption (session_key)</li>
</ul>
</li>
</ul>
<h3>Sample cURL Request</h3>
<pre><code class="language-curl">curl -X 'POST' \
  'https://api-test.shell.com/fleetmanagement/v2/card/OrderCard' \
  -H 'accept: application/json' \
  -H 'RequestId: 2b0cbe11-f109-4c43-9201-49af0370df1c' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer **********' \
  -d '{
  "CardDetails": [
    {
      "ColCoCode": 5,
      "PayerNumber": "GB00000003",
      "AccountNumber": "GB00000003",
      "CardTypeId": 503,
      "DriverName": "John Smith",
      "TokenTypeId": 500,
      "EmbossText": "JSMITH",
      "PurchaseCategoryId": 104,  
      "SelfSelectedEncryptedPIN": "0hCx7wfFp3z8QkW8dElhHiMwCwC1",
      "SelfSelectedPINKeyID": "123aaa33198dc8f3s4k77dsc78",
      "SelfSelectedPINSessionKey": "WoWB+8UEd71+8QXwuE75flkAQ /4Q6gDFSn027oJ/0ne6LmzVIxJ87yoeqKS /C+OIBJ7bTvasLH+xvDSZtzoOZHr 7wfFmpfSyet8KnKjnagSicrUgpGk 7qFyOw3iA9/Qd6Oy9djYR3C3cDWEpj /YREZ1lBGReb9fqdSpoKx8mnGuPAw7",
      "CardDeliveryType": 1,
      "CardContact": {
        "DeliveryContactTitle": "Mr.",
        "DeliveryContactName": "Robert",
        "DeliveryCompanyName": "WILTON AUFDERHAR ",
        "DeliveryAddressLine1": "Herrn Dieter Whausen Lansstrab ",
        "DeliveryAddressLine2": "10th avenue",
        "DeliveryAddressLine3": "makati city",
        "DeliveryZipCode": "12130",
        "DeliveryCity": "manila",
        "DeliveryRegionId": 43,
        "DeliveryRegion": "Philippines",
        "DeliveryCountry": "WILTON AUFDERHAR",
        "PhoneNumber": 99999999999,
        "EmailAddress": "xxxxx@example.com",
        "SaveForCardReissue": false
      },
      "PINDeliveryAddressType": 1,
      "PINAdviceType": 1,
      "PINContact": {
        "DeliveryContactTitle": "Mr.",
        "DeliveryContactName": "Robert",
        "DeliveryCompanyName": "WILTON AUFDERHAR ",
        "DeliveryAddressLine1": "Herrn Dieter Whausen Lansstrab ",
        "DeliveryAddressLine2": "10th avenue",
        "DeliveryAddressLine3": "makati city",
        "DeliveryZipCode": "12130",
        "DeliveryCity": "manila",
        "DeliveryRegionId": 43,
        "DeliveryRegion": "Philippines",
        "DeliveryCountry": "WILTON AUFDERHAR",
        "PhoneNumber": 99999999999,
        "EmailAddress": "xxxxx@example.com",
        "SaveForPINReminder": false
      }
    }
  ],
  "RequestId": "ed557f02 - c7d7 - 4c01 - b3e5 - 11bf3239c8ed"
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
  "CardReferences": [
    {
      "DriverAndVRN": "John Smith;1234",
      "OrderCardReference": 229781
    }
  ],
  "OrderReference": 181565,
}
</code></pre></div>
      <span><span>Anonymous (not verified)</span></span>
<span><time datetime="2025-11-05T05:56:57+00:00" title="Wednesday, November 5, 2025 - 05:56">Wed, 11/05/2025 - 05:56</time>
</span>
