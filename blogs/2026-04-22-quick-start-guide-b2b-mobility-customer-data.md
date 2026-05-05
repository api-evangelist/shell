---
title: "Quick Start Guide B2B Mobility Customer Data"
url: "https://developer.shell.com/api-catalog/b2b-mobility-customer-data/quick-start-guide-b2b-mobility-customer-data"
date: "Wed, 22 Apr 2026 07:28:04 +0000"
author: ""
feed_url: "https://developer.shell.com/rss.xml"
---
<span>Quick Start Guide B2B Mobility Customer Data</span>

            <div class="has-button has-list field field--body field--label-hidden field__item"><h1>B2B Mobility Customer Data Quickstart</h1>
<h2>Introduction</h2>
<p>The B2B Mobility Customer Data API is a RESTful service that enables you to query and manage customer account details, card groups, and related configurations within the Shell Cards Platform. This API provides flexible search capabilities, supports pagination, and allows you to retrieve account information, card delivery addresses, price lists, and card types. It also supports operations for creating and updating card groups, as well as moving cards between groups.</p>
<table>
<thead>
<tr>
<th>Benefit</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Comprehensive Account Management</strong></td>
<td>Access detailed customer account information including billing, card summaries, and status</td>
</tr>
<tr>
<td><strong>Card Group Operations</strong></td>
<td>Create, update, and terminate card groups with flexible card movement capabilities</td>
</tr>
<tr>
<td><strong>Price List Access</strong></td>
<td>Retrieve national and international price lists with customer-specific discounts</td>
</tr>
<tr>
<td><strong>Flexible Search</strong></td>
<td>Query data with multiple search criteria and pagination support</td>
</tr>
</tbody>
</table>
<h2>Authentication</h2>
<p>This API supports both Basic Authentication and OAuth 2.0. OAuth 2.0 is the recommended authentication method for enhanced security.</p>
<h4>Migration Note</h4>
<p>The API now supports OAuth 2.0 authentication. If you are currently using Basic Authentication, we recommend migrating to OAuth 2.0 for improved security. The Base URL has been updated, and all endpoints are now versioned under the /v1 path. Please refer to the OAuth 2.0 Migration Support for detailed migration guidance.</p>
<h4>Authorization flow</h4>
<ol>
<li><strong>Request Client ID and Secret</strong></li>
</ol>
<p>Contact Shell API Team in order to request access to OAuth authentication. The Shell API team will provide a Client ID and Secret.</p>
<ol start="2">
<li><strong>Request Bearer token</strong></li>
</ol>
<p>Once you get the credentials, make a request to the <a href="https://developer.shell.com/api-catalog/v1.0.1/shell-authentication#/OAuth%20token">Shell Authentication API's OAuth token endpoint</a> with your credentials.</p>
<p>Example request:</p>
<pre><code class="language-apache language-curl hljs php">curl --location --request POST <span class="hljs-string">'https://api-test.shell.com/v2/oauth/token'</span> \
--header <span class="hljs-string">'Content-Type: application/x-www-form-urlencoded'</span> \
--data-urlencode <span class="hljs-string">'client_id=**************'</span> \
--data-urlencode <span class="hljs-string">'client_secret=**************'</span> \
--data-urlencode <span class="hljs-string">'grant_type=client_credentials'</span></code></pre><p>You'll receive a Bearer token in the response:</p>
<pre><code class="language-json hljs php">{
   <span class="hljs-string">"access_token"</span>: <span class="hljs-string">"**************"</span>,
   <span class="hljs-string">"expires_in"</span>: <span class="hljs-string">"899"</span>,
   <span class="hljs-string">"token_type"</span>: <span class="hljs-string">"Bearer"</span>
}</code></pre><p>Note: The bearer token expiration time is provided in seconds.</p>
<ol start="3">
<li><strong>Authorize API requests</strong></li>
</ol>
<p>When calling Shell APIs, include the following in the header of the request.</p>
<pre><code class="language-apache language-curl hljs yaml"><span class="hljs-attr">Authorization:</span> <span class="hljs-string">Bearer</span> <span class="hljs-string">access_token</span></code></pre><h2>Base URLs</h2>
<table>
<thead>
<tr>
<th>Environment</th>
<th>URL</th>
</tr>
</thead>
<tbody>
<tr>
<td>Test</td>
<td><a href="https://api-test.shell.com/test">https://api-test.shell.com/test</a></td>
</tr>
<tr>
<td>Production</td>
<td><a href="https://api.shell.com">https://api.shell.com</a></td>
</tr>
</tbody>
</table>
<h2>Core Integration</h2>
<h3>1. Get Logged-In User Details</h3>
<p><strong>Description:</strong> This endpoint retrieves the user data of the logged-in user, including accessible payers, accounts, and roles. This operation should be called after successful authentication to obtain the PayerId needed for subsequent API calls.</p>
<p><strong>Path:</strong> <code class=" hljs ">POST /user-management/v1/loggedinuser</code></p>
<h5>Sample Request</h5>
<pre><code class="language-apache language-curl hljs protobuf">curl --location 'https:<span class="hljs-comment">//api-test.shell.com/test/user-management/v1/loggedinuser' \</span>
--header 'RequestId: <span class="hljs-number">2</span>b0cbe11-f109-<span class="hljs-number">4</span>c43-<span class="hljs-number">9201</span>-<span class="hljs-number">49</span>af0370df1c' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
  <span class="hljs-string">"Filters"</span>: {
    <span class="hljs-string">"IncludePayerGroup"</span>: <span class="hljs-literal">false</span>,
    <span class="hljs-string">"IncludeEIDDetails"</span>: <span class="hljs-literal">false</span>,
    <span class="hljs-string">"RequestedAPIName"</span>: <span class="hljs-string">"v1/Card/OrderCard"</span>
  }
}'</code></pre><h5>Request Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>RequestId</td>
<td>string</td>
<td>Yes</td>
<td>Mandatory UUID (RFC 4122) for request tracking</td>
</tr>
<tr>
<td>IncludePayerGroup</td>
<td>boolean</td>
<td>No</td>
<td>Include payer group information when true (default: false)</td>
</tr>
<tr>
<td>IncludeEIDDetails</td>
<td>boolean</td>
<td>No</td>
<td>Include Electronic Invoice Data when true (default: false)</td>
</tr>
</tbody>
</table>
<h5>Sample Response</h5>
<pre><code class="language-json hljs php">{
  <span class="hljs-string">"RequestId"</span>: <span class="hljs-string">"2b0cbe11-f109-4c43-9201-49af0370df1c"</span>,
  <span class="hljs-string">"Status"</span>: <span class="hljs-string">"SUCCESS"</span>,
  <span class="hljs-string">"Data"</span>: [
    {
      <span class="hljs-string">"UserName"</span>: <span class="hljs-string">"John123"</span>,
      <span class="hljs-string">"DisplayName"</span>: <span class="hljs-string">"John A."</span>,
      <span class="hljs-string">"HasAPIAccess"</span>: <span class="hljs-keyword">true</span>,
      <span class="hljs-string">"Payers"</span>: [
        {
          <span class="hljs-string">"IsDefault"</span>: <span class="hljs-keyword">true</span>,
          <span class="hljs-string">"ColcoId"</span>: <span class="hljs-number">1</span>,
          <span class="hljs-string">"ColcoCode"</span>: <span class="hljs-number">86</span>,
          <span class="hljs-string">"PayerId"</span>: <span class="hljs-number">1234</span>,
          <span class="hljs-string">"PayerNumber"</span>: <span class="hljs-string">"GB000000123"</span>,
          <span class="hljs-string">"PayerName"</span>: <span class="hljs-string">"MATTHEW ALGIE &amp;amp; COMPANY LIMITED"</span>
        }
      ]
    }
  ]
}</code></pre><h5>Response Fields</h5>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>UserName</td>
<td>string</td>
<td>Logged in user identifier</td>
</tr>
<tr>
<td>DisplayName</td>
<td>string</td>
<td>Name of the logged in user</td>
</tr>
<tr>
<td>HasAPIAccess</td>
<td>boolean</td>
<td>True if user has access to the requested API</td>
</tr>
<tr>
<td>PayerId</td>
<td>integer</td>
<td>Payer Id for use in subsequent requests</td>
</tr>
<tr>
<td>PayerNumber</td>
<td>string</td>
<td>Payer Number for use in subsequent requests</td>
</tr>
</tbody>
</table>
<h3>2. Query Customer Accounts</h3>
<p><strong>Description:</strong> This endpoint allows querying customer account details from the Shell Cards Platform with flexible search criteria and pagination support. Use the PayerId obtained from the previous step.</p>
<p><strong>Path:</strong> <code class=" hljs ">POST /customer-management/v1/accounts</code></p>
<h5>Sample Request</h5>
<pre><code class="language-apache language-curl hljs protobuf">curl --location 'https:<span class="hljs-comment">//api-test.shell.com/test/customer-management/v1/accounts' \</span>
--header 'RequestId: <span class="hljs-number">2</span>b0cbe11-f109-<span class="hljs-number">4</span>c43-<span class="hljs-number">9201</span>-<span class="hljs-number">49</span>af0370df1c' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
  <span class="hljs-string">"Filters"</span>: {
    <span class="hljs-string">"ColCoCode"</span>: <span class="hljs-number">86</span>,
    <span class="hljs-string">"PayerNumber"</span>: <span class="hljs-string">"GB000000123"</span>,
    <span class="hljs-string">"Status"</span>: <span class="hljs-string">"ACTIVE"</span>,
    <span class="hljs-string">"IncludeCardSummary"</span>: <span class="hljs-literal">true</span>
  },
  <span class="hljs-string">"Page"</span>: <span class="hljs-number">1</span>,
  <span class="hljs-string">"PageSize"</span>: <span class="hljs-number">50</span>
}'</code></pre><h5>Request Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>ColCoCode</td>
<td>integer</td>
<td>Yes</td>
<td>Collecting Company Code (Shell Code)</td>
</tr>
<tr>
<td>PayerNumber</td>
<td>string</td>
<td>Yes</td>
<td>Payer Number of the customer</td>
</tr>
<tr>
<td>Status</td>
<td>string</td>
<td>No</td>
<td>Account status filter (ACTIVE, BLOCKED, CANCELLED, etc.)</td>
</tr>
<tr>
<td>IncludeCardSummary</td>
<td>boolean</td>
<td>No</td>
<td>Include card summary details (default: true)</td>
</tr>
<tr>
<td>Page</td>
<td>integer</td>
<td>No</td>
<td>Page number (default: 1)</td>
</tr>
<tr>
<td>PageSize</td>
<td>integer</td>
<td>No</td>
<td>Records per page (default: 50)</td>
</tr>
</tbody>
</table>
<h5>Sample Response</h5>
<pre><code class="language-json hljs yaml"><span class="hljs-string">{</span>
  <span class="hljs-attr">"RequestId":</span> <span class="hljs-string">"2b0cbe11-f109-4c43-9201-49af0370df1c"</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"Status":</span> <span class="hljs-string">"SUCCESS"</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"Data":</span> <span class="hljs-string">[</span>
    <span class="hljs-string">{</span>
      <span class="hljs-attr">"AccountId":</span> <span class="hljs-number">1</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"AccountNumber":</span> <span class="hljs-string">"GB000000124"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"AccountFullName":</span> <span class="hljs-string">"Acme Corporation"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"Status":</span> <span class="hljs-string">"Active"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"CurrencyCode":</span> <span class="hljs-string">"EUR"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"TotalCards":</span> <span class="hljs-number">1000</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"TotalActiveCards":</span> <span class="hljs-number">500</span>
    <span class="hljs-string">}</span>
  <span class="hljs-string">],</span>
  <span class="hljs-attr">"Page":</span> <span class="hljs-number">1</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"TotalRecords":</span> <span class="hljs-number">100</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"TotalPages":</span> <span class="hljs-number">2</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"PageSize":</span> <span class="hljs-number">50</span>
<span class="hljs-string">}</span></code></pre><h5>Response Fields</h5>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>AccountId</td>
<td>integer</td>
<td>Account identifier</td>
</tr>
<tr>
<td>AccountNumber</td>
<td>string</td>
<td>Account number</td>
</tr>
<tr>
<td>AccountFullName</td>
<td>string</td>
<td>Full name of the account</td>
</tr>
<tr>
<td>Status</td>
<td>string</td>
<td>Current account status</td>
</tr>
<tr>
<td>CurrencyCode</td>
<td>string</td>
<td>ISO currency code</td>
</tr>
<tr>
<td>TotalCards</td>
<td>integer</td>
<td>Total number of cards under the account</td>
</tr>
<tr>
<td>TotalActiveCards</td>
<td>integer</td>
<td>Number of active cards</td>
</tr>
</tbody>
</table>
<h3>3. Query Card Groups</h3>
<p><strong>Description:</strong> This endpoint retrieves card group details from the Shell Cards Platform with flexible search criteria and pagination. Card groups help organize cards within an account.</p>
<p><strong>Path:</strong> <code class=" hljs ">POST /customer-management/v1/cardgroups</code></p>
<h5>Sample Request</h5>
<pre><code class="language-apache language-curl hljs protobuf">curl --location 'https:<span class="hljs-comment">//api-test.shell.com/test/customer-management/v1/cardgroups' \</span>
--header 'RequestId: <span class="hljs-number">2</span>b0cbe11-f109-<span class="hljs-number">4</span>c43-<span class="hljs-number">9201</span>-<span class="hljs-number">49</span>af0370df1c' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
  <span class="hljs-string">"Filters"</span>: {
    <span class="hljs-string">"ColCoCode"</span>: <span class="hljs-number">86</span>,
    <span class="hljs-string">"PayerNumber"</span>: <span class="hljs-string">"GB000000123"</span>,
    <span class="hljs-string">"Status"</span>: <span class="hljs-string">"ACTIVE"</span>
  },
  <span class="hljs-string">"Page"</span>: <span class="hljs-number">1</span>,
  <span class="hljs-string">"PageSize"</span>: <span class="hljs-number">50</span>
}'</code></pre><h5>Request Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>ColCoCode</td>
<td>integer</td>
<td>Yes</td>
<td>Collecting Company Code</td>
</tr>
<tr>
<td>PayerNumber</td>
<td>string</td>
<td>Yes</td>
<td>Payer Number of the customer</td>
</tr>
<tr>
<td>Status</td>
<td>string</td>
<td>Yes</td>
<td>Card group status (ACTIVE, TERMINATED, ALL)</td>
</tr>
<tr>
<td>CardGroupName</td>
<td>string</td>
<td>No</td>
<td>Filter by card group name (min 2 characters)</td>
</tr>
</tbody>
</table>
<h5>Sample Response</h5>
<pre><code class="language-json hljs yaml"><span class="hljs-string">{</span>
  <span class="hljs-attr">"RequestId":</span> <span class="hljs-string">"2b0cbe11-f109-4c43-9201-49af0370df1c"</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"Status":</span> <span class="hljs-string">"SUCCESS"</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"Data":</span> <span class="hljs-string">[</span>
    <span class="hljs-string">{</span>
      <span class="hljs-attr">"CardGroupId":</span> <span class="hljs-number">40000</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"CardGroupName":</span> <span class="hljs-string">"006240 FIRE BRIGHT SOLUTIONS"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"Status":</span> <span class="hljs-string">"ACTIVE"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"PrintOnCard":</span> <span class="hljs-literal">true</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"CardTypeId":</span> <span class="hljs-number">1234</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"TotalCards":</span> <span class="hljs-number">1234</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"ActiveCards":</span> <span class="hljs-number">999</span>
    <span class="hljs-string">}</span>
  <span class="hljs-string">],</span>
  <span class="hljs-attr">"Page":</span> <span class="hljs-number">1</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"TotalRecords":</span> <span class="hljs-number">100</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"TotalPages":</span> <span class="hljs-number">2</span><span class="hljs-string">,</span>
  <span class="hljs-attr">"PageSize":</span> <span class="hljs-number">50</span>
<span class="hljs-string">}</span></code></pre><h5>Response Fields</h5>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>CardGroupId</td>
<td>integer</td>
<td>Card group identifier</td>
</tr>
<tr>
<td>CardGroupName</td>
<td>string</td>
<td>Name of the card group</td>
</tr>
<tr>
<td>Status</td>
<td>string</td>
<td>Status of the card group</td>
</tr>
<tr>
<td>TotalCards</td>
<td>integer</td>
<td>Total number of cards in the group</td>
</tr>
<tr>
<td>ActiveCards</td>
<td>integer</td>
<td>Number of active cards in the group</td>
</tr>
</tbody>
</table>
<h3>4. Create Card Group</h3>
<p><strong>Description:</strong> This endpoint creates a new card group in the Shell Cards Platform and optionally moves up to 500 cards into the newly created group. Move card requests are queued after validation.</p>
<p><strong>Path:</strong> <code class=" hljs ">POST /customer-management/v1/createcardgroup</code></p>
<h5>Sample Request</h5>
<pre><code class="language-apache language-curl hljs protobuf">curl --location 'https:<span class="hljs-comment">//api-test.shell.com/test/customer-management/v1/createcardgroup' \</span>
--header 'RequestId: <span class="hljs-number">2</span>b0cbe11-f109-<span class="hljs-number">4</span>c43-<span class="hljs-number">9201</span>-<span class="hljs-number">49</span>af0370df1c' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
  <span class="hljs-string">"ColCoCode"</span>: <span class="hljs-number">86</span>,
  <span class="hljs-string">"PayerNumber"</span>: <span class="hljs-string">"GB000000123"</span>,
  <span class="hljs-string">"AccountNumber"</span>: <span class="hljs-string">"GB000000124"</span>,
  <span class="hljs-string">"CardGroupName"</span>: <span class="hljs-string">"006240 FIRE BRIGHT SOLUTIONS"</span>,
  <span class="hljs-string">"PrintOnCard"</span>: <span class="hljs-literal">true</span>,
  <span class="hljs-string">"Cards"</span>: [
    {
      <span class="hljs-string">"AccountNumber"</span>: <span class="hljs-string">"GB99215176"</span>,
      <span class="hljs-string">"PAN"</span>: <span class="hljs-string">"7002051006629890645"</span>
    }
  ]
}'</code></pre><h5>Request Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>ColCoCode</td>
<td>integer</td>
<td>Yes</td>
<td>Collecting Company Code</td>
</tr>
<tr>
<td>PayerNumber</td>
<td>string</td>
<td>Yes</td>
<td>Payer Number of the customer</td>
</tr>
<tr>
<td>AccountNumber</td>
<td>string</td>
<td>Yes</td>
<td>Account Number of the customer</td>
</tr>
<tr>
<td>CardGroupName</td>
<td>string</td>
<td>Yes</td>
<td>Name of the new card group (1-40 characters)</td>
</tr>
<tr>
<td>PrintOnCard</td>
<td>boolean</td>
<td>Yes</td>
<td>Whether to emboss card group name on cards</td>
</tr>
<tr>
<td>Cards</td>
<td>array</td>
<td>No</td>
<td>List of cards to move (max 500)</td>
</tr>
</tbody>
</table>
<h5>Sample Response</h5>
<pre><code class="language-json hljs php">{
  <span class="hljs-string">"RequestId"</span>: <span class="hljs-string">"2b0cbe11-f109-4c43-9201-49af0370df1c"</span>,
  <span class="hljs-string">"Status"</span>: <span class="hljs-string">"SUCCESS"</span>,
  <span class="hljs-string">"Data"</span>: [
    {
      <span class="hljs-string">"MainReference"</span>: <span class="hljs-number">1234</span>,
      <span class="hljs-string">"NewCardGroupReference"</span>: <span class="hljs-number">5672</span>,
      <span class="hljs-string">"SuccessfulRequests"</span>: [
        {
          <span class="hljs-string">"PAN"</span>: <span class="hljs-string">"7002051123456789145"</span>,
          <span class="hljs-string">"Reference"</span>: <span class="hljs-number">12345</span>
        }
      ],
      <span class="hljs-string">"ErrorCards"</span>: []
    }
  ]
}</code></pre><h5>Response Fields</h5>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>MainReference</td>
<td>integer</td>
<td>Reference number for tracking the overall request</td>
</tr>
<tr>
<td>NewCardGroupReference</td>
<td>integer</td>
<td>Reference number for the card group creation</td>
</tr>
<tr>
<td>SuccessfulRequests</td>
<td>array</td>
<td>List of successfully queued card move requests</td>
</tr>
<tr>
<td>ErrorCards</td>
<td>array</td>
<td>List of cards that failed validation</td>
</tr>
</tbody>
</table>
<h2>Error Handling</h2>
<p>The API uses standard HTTP status codes. In case of an error, additional details will be provided in the response body.</p>
<table>
<thead>
<tr>
<th>Error Code</th>
<th>Description</th>
<th>Solution</th>
</tr>
</thead>
<tbody>
<tr>
<td>E0001</td>
<td>Validation Error</td>
<td>Check the request parameters for missing or invalid values</td>
</tr>
<tr>
<td>E0003</td>
<td>Unauthorized</td>
<td>Verify credentials and ensure user has access to the operation</td>
</tr>
<tr>
<td>E0005</td>
<td>Resource Not Found</td>
<td>Confirm the requested resource exists and is accessible</td>
</tr>
<tr>
<td>9015</td>
<td>Duplicate Card Group Name</td>
<td>Use a unique card group name for the customer</td>
</tr>
</tbody>
</table>
</div>
      <span><time datetime="2026-04-22T07:28:04+00:00" title="Wednesday, April 22, 2026 - 07:28">Wed, 04/22/2026 - 07:28</time>
</span>
