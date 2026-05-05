---
title: "Quick Start Guide"
url: "https://developer.shell.com/api-catalog/b2b-mobility-card-recent-transaction/quick-start-guide-7"
date: "Mon, 16 Feb 2026 08:38:53 +0000"
author: "Anonymous"
feed_url: "https://developer.shell.com/rss.xml"
---
<span>Quick Start Guide</span>

            <div class="has-button has-list field field--body field--label-hidden field__item"><h2>Getting Started with B2B Mobility Card Recent Transactions</h2>
<p>B2B Mobility Card Recent Transactions endpoint allows querying last 48 hours of transaction data of Shell Card (i.e. Priced, Billed, Unbilled etc. sales items). It provides a flexible search criteria and supports pagination. E.g., if the request is made at 08:30 AM on 18 Aug 2022 then transactions until 16 Aug 2022 08:30 AM (including) can be retrieved.</p>
<h2>Authentication</h2>
<p>Shell API’s are secured by OAuth 2.0. It uses the 'Client Credentials' Grant Type to allow the API consumer to access data. The end to end process is illustrated in the sequence diagram below.</p>
<div class="mermaid">
<p>sequenceDiagram
participant PartnerApplication 
participant Shell 
autonumber
alt Manual Process
rect rgb(200, 150, 255)
PartnerApplication -&gt;&gt;Shell: Request Client ID and Client Secret
activate Shell
Shell -&gt;&gt; PartnerApplication : Generate and provide Client ID and Client Secret
deactivate Shell
end
end
alt Authentication/Authorization
rect rgb(191, 223, 255)
PartnerApplication -&gt;&gt;Shell: Inititate request to OAuth end point with credentials
activate Shell
Shell -&gt;&gt; PartnerApplication : (200-OK) Returns Bearer Token
deactivate Shell
end
end
alt Call Functional Endpoint
rect rgb(200, 150, 255)
PartnerApplication -&gt;&gt;Shell: Initiate request to functional endpoint along with bearer token received from previous step
activate Shell
Shell -&gt;&gt; PartnerApplication : Returns a response on validation of the bearer token
deactivate Shell
end
end</p>
</div> 
<p>This step is to generate the API Access Token using the unique Client ID and Client Secret provided by Shell. (Please note that this credentials is to validate the API request between Shell and its partner so its system to system access token)</p>
<h3>Key Request Parameters</h3>
<p>Once you receive the client ID &amp; Secret, next step is to call the <a href="https://api-test.shell.com/oauth/v1/mobility/token">https://api-test.shell.com/oauth/v1/mobility/token</a> endpoint to authenticate. Following are the key parameters-</p>
<ul>
<li>Method: POST</li>
<li>Authorization Type: OAuth 2.0</li>
<li>Auth URI: <a href="https://api-test.shell.com/oauth/v1/mobility/token">https://api-test.shell.com/oauth/v1/mobility/token</a></li>
<li>Client_Id: <strong>****</strong> (OAuth Client ID)</li>
<li>Client Secret: <strong>****</strong> (OAuth Client Secret)</li>
<li>Grant Type: client_credentials</li>
</ul>
<h3>Sample cURL Request</h3>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/oauth/v1/mobility/token' \
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
<h2>Get Recent Transactions Data</h2>
<p>This end point allows querying last 48 hours of transaction data of Shell Card (i.e. Priced, Billed, Unbilled etc. sales items). It provides a flexible search criteria and supports pagination.</p>
<p>Supported operations</p>
<ul>
<li>Search by Date and Time range (within the last 48 hours only)</li>
<li>Search by Payer and/or Account number</li>
<li>Search by Card</li>
<li>Search by Purchased Country</li>
<li>Search by Transaction posting date</li>
<li>Search by Driver Name or Vehicle registration number</li>
<li>Search by Fuel only transactions</li>
<li>Search by Product and/or Product group</li>
</ul>
<h3>Business Case - 1</h3>
<p>Customer wants to download the complete list of recent transactions for the last 48 hours for <strong>all his accounts</strong> (Based on single Payer Number)</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
</ul>
</li>
<li>Optional Parameters<ul>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>ColumnList : <strong>All</strong> to be passed to view all the response parameters.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer ********' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 2,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
    "ColumnList" : "All"
 }
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 142,
    "TotalPages": 71,
    "Data": [
        {
            "AccountNumber": "GB99214035",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "69.56",
            "EuroshellSiteNumber": "",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": "",
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "",
            "PayerNumber": "GB99213576",
            "Longitude": "",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "9089           ",
            "SiteName": "",
            "Network": "2002296826",
            "DelcoCode": "",
            "OdometerInput": "123",
            "OdometerReadingKm": "198.06763285024155",
            "OdometerReadingMiles": "123",
            "CardPAN": "700205*******320615",
            "PINIndicator": "Y",
            "POIReceiptNumber": "",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "0",
            "FuelVolume": "37.22",
            "SfgwCardDateOfExpiry": "2025-12",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "092688",
            "TransactionDate": "2022-08-31",
            "TransactionDateTime": "2022-08-31 11:34:44.000",
            "TransactionId": "1135575003",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "11:34:44",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.86",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "10:34:44",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD FLT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD FLT NAT MULTI  - CHIP",
            "EmbossType": "Vehicle"
        },
        {
            "AccountNumber": "GB20000315",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "106.09",
            "EuroshellSiteNumber": "0623",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": 32934,
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "53.37200",
            "PayerNumber": "GB99213576",
            "Longitude": "-1.38892",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "GB0623000000000",
            "SiteName": "EG CREST SERVICE STATION",
            "Network": "0000000826",
            "DelcoCode": "005",
            "OdometerInput": "74601",
            "OdometerReadingKm": "120130.4347826087",
            "OdometerReadingMiles": "74601",
            "CardPAN": "700205*******152607",
            "PINIndicator": "Y",
            "POIReceiptNumber": "0000071175",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "4",
            "FuelVolume": "57.07",
            "SfgwCardDateOfExpiry": "2025-03",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "806977",
            "TransactionDate": "2022-08-31",
            "TransactionDateTime": "2022-08-31 11:26:40.000",
            "TransactionId": "1135579241",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "Shell U.K. Oil Products Limited",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "11:26:40",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.859",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "10:26:40",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD FLT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD FLT NAT MULTI  - CHIP",
            "EmbossType": "Vehicle"
        }
    ]
}
</code></pre>
<h3>Business Case - 2</h3>
<p>Customer wants to download the complete list of recent transactions for the last 48 hours for all a <strong>particular account number</strong>.</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
<li>AccountNumber - Account number for which data needs to be requested. </li>
</ul>
</li>
<li>Optional Parameters<ul>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>AccountNumber : Account number of the selected payer.</li>
<li>ColumnList : <strong>All</strong> to be passed to view all the response parameters.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer *********' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 1,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
    "AccountNumber": "GB99214035",
    "ColumnList" : "All"
 }
}'
</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 71,
    "TotalPages": 71,
    "Data": [
        {
            "AccountNumber": "GB99214035",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "235.59",
            "EuroshellSiteNumber": "2163",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": 33200,
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "53.13739",
            "PayerNumber": "GB99213576",
            "Longitude": "-1.33362",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "GB2163000000000",
            "SiteName": "SHELL CHESTERFIELD NORTH",
            "Network": "0000000826",
            "DelcoCode": "005",
            "OdometerInput": "",
            "OdometerReadingKm": "",
            "OdometerReadingMiles": "",
            "CardPAN": "707705*******510330",
            "PINIndicator": "Y",
            "POIReceiptNumber": "0000066970",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "d",
            "FuelVolume": "120.26",
            "SfgwCardDateOfExpiry": "2025-04",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "845571",
            "TransactionDate": "2022-08-31",
            "TransactionDateTime": "2022-08-31 12:21:27.000",
            "TransactionId": "1135622161",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "Shell U.K. Oil Products Limited",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "12:21:27",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.959",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "11:21:27",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD CRT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD CRT NAT MULTI - CHIP",
            "EmbossType": "Vehicle"
        }
    ]
}
</code></pre>
<h3>Business Case - 3</h3>
<p>Customer wants to download the complete list of recent transactions for the last 48 hours for all a <strong>particular card</strong> .</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
<li>CardPAN - Card number for which data needs to be requested. </li>
</ul>
</li>
<li>Optional Parameters<ul>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>CardPAN : Card number of the selected payer.</li>
<li>ColumnList : <strong>All</strong> to be passed to view all the response parameters.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer **********' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 1,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
    "CardPAN": "7002057036251320730",
    "ColumnList" : "All"
 }
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 2,
    "TotalPages": 2,
    "Data": [
        {
            "AccountNumber": "GB99214035",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "90.48",
            "EuroshellSiteNumber": "0477",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": 32741,
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "52.06807",
            "PayerNumber": "GB99213576",
            "Longitude": "-0.73669",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "GB0477000000000",
            "SiteName": "SHELL BLAKELANDS",
            "Network": "0000000826",
            "DelcoCode": "005",
            "OdometerInput": "",
            "OdometerReadingKm": "",
            "OdometerReadingMiles": "",
            "CardPAN": "700205*******320730",
            "PINIndicator": "Y",
            "POIReceiptNumber": "0000085491",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "d",
            "FuelVolume": "49.2",
            "SfgwCardDateOfExpiry": "2026-05",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "237684",
            "TransactionDate": "2022-08-31",
            "TransactionDateTime": "2022-08-31 06:16:04.000",
            "TransactionId": "1135221633",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "Shell U.K. Oil Products Limited",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "06:16:04",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.839",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "05:16:04",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD FLT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD FLT NAT MULTI  - CHIP",
            "EmbossType": "Vehicle"
        }
    ]
}</code></pre>
<h3>Business Case - 4</h3>
<p>Customer wants to download the complete list of recent transactions for a <strong>particular time range within the last 48 hours</strong>. Eg : Get the data for the last 6 hours</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
<li>FromDateTime - Start Date and Time (UTC) to be provided</li>
<li>ToDateTime - End Date and Time (UTC) to be provided</li>
</ul>
</li>
<li>Optional Parameters<ul>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>FromDateTime - Start Date and Time (UTC) to be provided</li>
<li>ToDateTime - End Date and Time (UTC) to be provided</li>
<li>ColumnList : <strong>All</strong> to be passed to view all the response parameters.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer ********' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 1,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
    "FromDateTime":"2018-08-30 10:19:24.000",
    "ToDateTime":"2022-08-30 12:53:00.000",
    "ColumnList" : "All"    
 }
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 58,
    "TotalPages": 58,
    "Data": [
        {
            "AccountNumber": "GB99214035",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "65.47",
            "EuroshellSiteNumber": "2484",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": 33498,
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "53.42442",
            "PayerNumber": "GB99213576",
            "Longitude": "-1.25623",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "GB2484000000000",
            "SiteName": "SHELL BRAMLEY",
            "Network": "0000000826",
            "DelcoCode": "005",
            "OdometerInput": "",
            "OdometerReadingKm": "",
            "OdometerReadingMiles": "",
            "CardPAN": "700205*******320375",
            "PINIndicator": "Y",
            "POIReceiptNumber": "0000073310",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "d",
            "FuelVolume": "35.99",
            "SfgwCardDateOfExpiry": "2025-06",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "899053",
            "TransactionDate": "2022-08-30",
            "TransactionDateTime": "2022-08-30 12:47:45.000",
            "TransactionId": "1134649977",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "Shell U.K. Oil Products Limited",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "12:47:45",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.819",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "11:47:45",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD FLT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD FLT NAT MULTI  - CHIP",
            "EmbossType": "Vehicle"
        }
    ]
}</code></pre>
<h3>Business Case - 5</h3>
<p>Customer wants to download the complete list of recent transactions for the last 48 hours for all a <strong>particular Vehicle registration number</strong> .</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
<li>VehicleRegistrationNumber - Vehicle Registration number for which data needs to be requested. </li>
</ul>
</li>
<li>Optional Parameters<ul>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>VehicleRegistrationNumber : Vehicle Registration number of the selected payer.</li>
<li>ColumnList : <strong>All</strong> to be passed to view all the response parameters.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer **********' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 1,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
            "VehicleRegistrationNumber": "WD XXXX",
    "ColumnList" : "All"    
 }
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 1,
    "TotalPages": 1,
    "Data": [
        {
            "AccountNumber": "GB70365100",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "107.67",
            "EuroshellSiteNumber": "0330",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": 32740,
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "52.04970",
            "PayerNumber": "GB99213576",
            "Longitude": "-0.79944",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "GB0330000000000",
            "SiteName": "SHELL STACEY BUSHES",
            "Network": "0000000826",
            "DelcoCode": "005",
            "OdometerInput": "",
            "OdometerReadingKm": "",
            "OdometerReadingMiles": "",
            "CardPAN": "700205*******004392",
            "PINIndicator": "Y",
            "POIReceiptNumber": "0000184567",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "d",
            "FuelVolume": "58.55",
            "SfgwCardDateOfExpiry": "2025-12",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "089063",
            "TransactionDate": "2022-08-31",
            "TransactionDateTime": "2022-08-31 06:14:20.000",
            "TransactionId": "1135220930",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "Shell U.K. Oil Products Limited",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "06:14:20",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.839",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "05:14:20",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD FLT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD FLT NAT MULTI  - CHIP",
            "EmbossType": "Vehicle"
        }
    ]
}</code></pre>
<h3>Business Case - 6</h3>
<p>Customer wants to download the complete list of recent transactions for the last 48 hours for all  <strong>fuel only transactions</strong> .</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
<li>FuelOnly - Fuel Only flag needs to be set as <code>true</code>. </li>
</ul>
</li>
<li>Optional Parameters<ul>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>FuelOnly : Fuel Only flag needs to be set as <code>true</code>.</li>
<li>ColumnList : <strong>All</strong> to be passed to view all the response parameters.</li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer **********' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 1,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
    "FuelOnly": "True",
    "ColumnList" : "All"    
 }
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 171,
    "TotalPages": 171,
    "Data": [
        {
            "AccountNumber": "GB99214035",
            "CardIssueNumber": "1",
            "CollectingCompanyCurrencyIsoCode": "GBP",
            "CustDataCustomerEntered": "",
            "CustDataDriverId": "",
            "CustDataFleetDescription": "",
            "FleetIdInput": "",
            "Amount": "135.41",
            "EuroshellSiteNumber": "0013",
            "IncomingProductCode": "",
            "ProductCode": "30",
            "ProductName": "Diesel AGO",
            "SiteCode": 32966,
            "HostingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "HostingCollectingCompanyNumber": "05",
            "IccdataTranTypeCode": "00",
            "TransactionType": "Purchase Request",
            "ColCoCode": 5,
            "Latitude": "53.62698",
            "PayerNumber": "GB99213576",
            "Longitude": "-1.23802",
            "MerchantCategory": "5541",
            "MerchantCategoryDescription": "",
            "PurchasedInCountry": "United Kingdom",
            "MerchantId": "GB0013000000000",
            "SiteName": "SHELL BARNSDALE BAR STH",
            "Network": "0000000826",
            "DelcoCode": "005",
            "OdometerInput": "",
            "OdometerReadingKm": "",
            "OdometerReadingMiles": "",
            "CardPAN": "700205*******320813",
            "PINIndicator": "Y",
            "POIReceiptNumber": "0000113060",
            "ProductsCodeAdditional": "",
            "ProductsTaxCode": "d",
            "FuelVolume": "72.45",
            "SfgwCardDateOfExpiry": "2026-08",
            "SiteCurrencyISOCode": "GBP",
            "CardId": "353323",
            "TransactionDate": "2022-08-31",
            "TransactionDateTime": "2022-08-31 15:38:20.000",
            "TransactionId": "1135832587",
            "TransactionStatus": "APPROVED",
            "UnitOfMeasure": "L",
            "VehicleRegistrationNumber": "WD XXXX",
            "DeclinedReason": "",
            "NetworkDelcoName": "Shell U.K. Oil Products Limited",
            "ProductGroupName": "Automotive Gas Oil",
            "FuelProduct": "All Fuels",
            "AccountCustomerName": "XYZ",
            "PayerName": "XYZ",
            "TransactionTime": "15:38:20",
            "TransactionCurrencySymbol": "£",
            "UnitPrice": "1.869",
            "AuthorisedFlag": "Y",
            "TransactionTimeGMT": "14:38:20",
            "ReasonCode": "00",
            "IssuerActionCode": "",
            "IssuerActionCodeDescription": "",
            "CardStatusReasonDescription": "Approved or completed successfully",
            "TransactionCountry": "826",
            "IssuingCollectingCompanyName": "Shell U.K. Oil Products Limited",
            "CardIssuerName": "H3-United Kingdom",
            "DriverName": "",
            "BearerDescription": "",
            "CardCategoryDescription": "Vehicle Card",
            "CardTypeDescription": "GB STD FLT NAT MULTI R7",
            "CardTokenTypeDescription": "GB STD FLT NAT MULTI  - CHIP",
            "EmbossType": "Vehicle"
        }
    ]
}
</code></pre>
<h3>Business Case - 7</h3>
<p>Customer wants to download the complete list of recent transactions for the last 48 hours for all  <strong>and receive only specific parameters in the response</strong> .</p>
<h4>Introduction</h4>
<ul>
<li>Mandatory Parameters<ul>
<li>Note that the API has pagination implemented and the the number records to be viewed in the response can be set in the request with PageSize parameter. (Minimum = 1 and Maximum = 1000)</li>
<li>Also the page number for which the records needs to viewed needs to be passed in the request. </li>
<li>ColCoCode - Collecting company code of the selected payer needs to be always passed in the request.</li>
<li>PayerNumber - Payer Number of the selected payer needs to be always passed in the request. </li>
<li>ColumnList - by deafult "All" is set in the API where all the parameters will be provided in the response. If you need specific parameters, then all the parameters to be passed as comma separated string.  </li>
</ul>
</li>
</ul>
<h4>Key Request Parameters</h4>
<ul>
<li>Method : POST</li>
<li>URI : <a href="https://api-test.shell.com/test/transaction-data/v1/recent">https://api-test.shell.com/test/transaction-data/v1/recent</a></li>
<li>Headers :<ul>
<li>Authorization  : Bearer <strong>access_token</strong> (Access Token generated from the OAuth end point)</li>
<li>RequestId      : GUID in order to track and trace the request </li>
</ul>
</li>
<li>Body : <ul>
<li>PageSize : Number of records per page (Eg: 2).</li>
<li>Page : Page number.</li>
<li>ColCoCode : ColCoCode of the selected payer.</li>
<li>PayerNumber : Payer Number of the selected payer.</li>
<li>ColumnList : <code>PayerNumber,AccountNumber,CardPAN,DriverName,Amount,FuelVolume,UnitOfMeasure,TransactionDateTime</code> to be passed in request to get only these parameters in the response. <strong>Please note that PayerNumber needs to be mandatory when you want to have a specific response</strong></li>
</ul>
</li>
</ul>
<h4>Sample cURL Request</h4>
<pre><code class="language-curl">curl --location --request POST 'https://api-test.shell.com/test/transaction-data/v1/recent' \
--header 'RequestId: 233e4567-e89b-12d3-a456-426614174000' \
--header 'Authorization: Bearer ****************' \
--header 'Content-Type: application/json' \
--data-raw '{
  "PageSize": 1,
  "Page": 1,
  "Filters": {
    "ColCoCode": 5,
    "PayerNumber": "GB99213576",
    "ColumnList" : "AccountNumber,PayerNumber,CardPAN,DriverName,Amount,FuelVolume,UnitOfMeasure,TransactionDateTime"    
 }
}'</code></pre>
<h4>Sample Response</h4>
<pre><code class="language-json">{
    "RequestId": "233e4567-e89b-12d3-a456-426614174000",
    "Status": "SUCCESS",
    "CurrentPage": 1,
    "RowCount": 172,
    "TotalPages": 172,
    "Data": [
        {
            "CardPAN": "7002057******320813",
            "DriverName": "",
            "UnitOfMeasure": "L",
            "TransactionDateTime": "2022-08-31 15:38:20.000",
            "FuelVolume": "72.45",
            "PayerNumber": "GB99213576",
            "Amount": "135.41",
            "AccountNumber": "GB99214035"
        }
    ]
}</code></pre></div>
      <span><span>Anonymous (not verified)</span></span>
<span><time datetime="2026-02-16T08:38:53+00:00" title="Monday, February 16, 2026 - 08:38">Mon, 02/16/2026 - 08:38</time>
</span>
