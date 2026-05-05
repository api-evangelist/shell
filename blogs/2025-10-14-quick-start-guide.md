---
title: "Quick Start Guide"
url: "https://developer.shell.com/api-catalog/shell-lube-monitor-marine-engine-monitoring-api/quick-start-guide"
date: "Tue, 14 Oct 2025 04:35:39 +0000"
author: "Anonymous"
feed_url: "https://developer.shell.com/rss.xml"
---
<span>Quick Start Guide</span>

            <div class="has-button has-list field field--body field--label-hidden field__item"><h1>Shell Lube Monitor Marine Engine Monitoring API</h1>
<h2>Overview</h2>
<p>The Shell Lube Monitor Marine Engine Monitoring API is a RESTful API that provides engine monitoring data and inspection insights for marine vessels. This API offers access to onboard engine data including cylinder logbook data, running hours, and operational metrics, as well as inspection insights based on piston ring images after cleaning to determine deposit presence.</p>
<p><strong>Version:</strong> 1.0.0<br />
<strong>Base URL:</strong> <code>https://api.shell.com/gcc/lubemonitor</code></p>
<h2>Authentication</h2>
<p>All API endpoints require the following authentication headers:</p>
<table>
<thead>
<tr>
<th>Header</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Username</code></td>
<td>string</td>
<td>Yes</td>
<td>Username for authentication</td>
</tr>
<tr>
<td><code>Password</code></td>
<td>string</td>
<td>Yes</td>
<td>Password for authentication</td>
</tr>
<tr>
<td><code>Authorization</code></td>
<td>string</td>
<td>Yes</td>
<td>Bearer OAuth 2.0 Token</td>
</tr>
</tbody>
</table>
<p><strong>Example:</strong></p>
<pre><code>Username: user@shell.com
Password: password123
Authorization: Bearer hbGciOiJSUzI1NiIsImtpZCI6</code></pre>
<h2>API Endpoints</h2>
<h3>1. Get Onboard Engine Monitoring Data</h3>
<p>Retrieves engine monitoring data captured onboard for marine vessels, including cylinder logbook data, running hours, and operational data.</p>
<p><strong>Endpoint:</strong> <code>GET /onboard-sample</code></p>
<h4>Parameters</h4>
<h5>Required Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Location</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>laVesselCode</code></td>
<td>string</td>
<td>query</td>
<td>Unique code identifying the vessel</td>
</tr>
<tr>
<td><code>engineNo</code></td>
<td>integer</td>
<td>query</td>
<td>Identifier for the specific engine on the vessel</td>
</tr>
</tbody>
</table>
<h5>Optional Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Location</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>dateCaptured</code></td>
<td>string (ISO 8601)</td>
<td>query</td>
<td>Specific date for which the data is requested</td>
</tr>
<tr>
<td><code>lastNSamples</code></td>
<td>integer (1-20)</td>
<td>query</td>
<td>Number of recent samples to retrieve (maximum 20)</td>
</tr>
<tr>
<td><code>latestSample</code></td>
<td>boolean</td>
<td>query</td>
<td>Flag to indicate if only the latest sample is needed</td>
</tr>
</tbody>
</table>
<h4>Validation Rules</h4>
<p>At least one of the following must be provided:</p>
<ul>
<li><code>dateCaptured</code></li>
<li><code>lastNSamples</code></li>
<li><code>latestSample</code></li>
</ul>
<h4>Use Case Examples</h4>
<ul>
<li><strong>Latest engine data:</strong> Set <code>latestSample=true</code></li>
<li><strong>Last 10 samples:</strong> Set <code>lastNSamples=10</code></li>
<li><strong>Specific date data:</strong> Set <code>dateCaptured=2025-09-01T00:00:00.000Z</code></li>
</ul>
<h4>Sample Request</h4>
<pre><code class="language-http">GET /onboard-sample?laVesselCode=61301&amp;engineNo=1&amp;latestSample=true
Host: api.shell.com/gcc/lubemonitor
Username: user@shell.com
Password: password123
Authorization: Bearer hbGciOiJSUzI1NiIsImtpZCI6</code></pre>
<h4>Response Schema</h4>
<p><strong>Success Response (200):</strong></p>
<pre><code class="language-json">[
  {
    "vesselIdText": "136246",
    "noOfEngines": 2,
    "customerName": "THENAMARIS LNG ",
    "marineCenter": "Hellenic Mariners (Greece)",
    "mainEngine": "Wartsila X72 DF",
    "reportAlertLevel": "Attention",
    "cylinderCondition": "Cylinder(s) 4,5 are in the Normal area, Cylinder(s) 1,2,3 are in the Attention area",
    "summary": "save comments and exit 3uL",
    "engineNo": 1,
    "dateCaptured": "2025-10-03T00:00:00.000Z",
    "updatedBy": "COOL RACER",
    "portLocation": "SEA",
    "cylinderData": [
      {
        "cylinderNo": 1,
        "pMax": 21,
        "fuelIndex": 30,
        "coolingTempCOut": 41,
        "linerWallTempCMin": 26,
        "linerWallTempCMax": 26,
        "magneticIron": 26,
        "feedrateSetpoint": 0.4,
        "bnMeasuresOnboard": 22,
        "corrosiveIron": 26,
        "onboardTotalIron": 52
      }
    ],
    "runningHourData": [
      {
        "cylinderNo": 1,
        "pistonRing": 1,
        "pCrown": 1,
        "pistonCrown": 3,
        "comments": "AA"
      }
    ],
    "runningData": {
      "comments": "Test 123",
      "oilGrade": "Alexia 40 (40 BN)",
      "oilDensity": 0.915,
      "totalEngineHours": 1222,
      "rpm": 100,
      "power": 6000,
      "sulphur": 0.1,
      "catfines": 40,
      "vanadiumContent": 30,
      "fuelConsumption": 22,
      "relHum": 32,
      "ambientTemperature": 30,
      "scavAirTemp": 26,
      "engineRoomTC": 26,
      "cylinderOilCons": 122,
      "sampleSentToLab": "Yes",
      "noOfTurboInUse": 2,
      "feedRateCalculated": 0.775
    },
    "recommendation": {
      "participation": "Engine Inspections - Monthly.Onboard Samples - Weekly and 48 hours after change of fuel bunker, feed rate adjustment or change in load more than +/-10%.Lab Samples - Monthly.For lab samples - first test onboard, note results in the logbook. Then land the same set of samples for laboratory analysis.",
      "onboardSampling": null
    }
  }
]</code></pre>
<hr />
<h3>2. Get Engine Inspection Deposits Data</h3>
<p>Provides inspection insights based on piston ring images after cleaning to determine whether deposits are present on the piston rings.</p>
<p><strong>Endpoint:</strong> <code>GET /inspection-deposits</code></p>
<h4>Parameters</h4>
<h5>Required Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Location</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>laVesselCode</code></td>
<td>string</td>
<td>query</td>
<td>Unique code identifying the vessel</td>
</tr>
<tr>
<td><code>engineNo</code></td>
<td>integer</td>
<td>query</td>
<td>Identifier for the specific engine on the vessel</td>
</tr>
</tbody>
</table>
<h5>Optional Parameters</h5>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Location</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>dateCaptured</code></td>
<td>string (ISO 8601)</td>
<td>query</td>
<td>Specific date for which inspection data is requested</td>
</tr>
<tr>
<td><code>lastNSamples</code></td>
<td>integer (1-20)</td>
<td>query</td>
<td>Number of recent inspection samples to retrieve (maximum 20)</td>
</tr>
<tr>
<td><code>latestSample</code></td>
<td>boolean</td>
<td>query</td>
<td>Flag to indicate if only the latest inspection result is needed</td>
</tr>
</tbody>
</table>
<h4>Validation Rules</h4>
<p>At least one of the following must be provided:</p>
<ul>
<li><code>dateCaptured</code></li>
<li><code>lastNSamples</code></li>
<li><code>latestSample</code></li>
</ul>
<h4>Use Case Examples</h4>
<ul>
<li><strong>Most recent inspection:</strong> Set <code>latestSample=true</code></li>
<li><strong>Inspection trends:</strong> Set <code>lastNSamples=5</code></li>
<li><strong>Specific date inspection:</strong> Set <code>dateCaptured=2025-03-07T00:00:00.000Z</code></li>
</ul>
<h4>Sample Request</h4>
<pre><code class="language-http">GET /inspection-deposits?laVesselCode=136246&amp;engineNo=1&amp;latestSample=true
Host: api.shell.com/gcc/lubemonitor
Username: user@shell.com
Password: password123
Authorization: Bearer hbGciOiJSUzI1NiIsImtpZCI6</code></pre>
<h4>Response Schema</h4>
<p><strong>Success Response (200):</strong></p>
<pre><code class="language-json">[
  {
    "vesselIdText": "136246",
    "vesselName": "COOL RACER",
    "customerName": "THENAMARIS LNG ",
    "dateCaptured": "2025-03-07T00:00:00.000Z",
    "engineNo": 1,
    "cylinderData": [
      {
        "cylinderNo": 1,
        "deposit": "Yes"
      },
      {
        "cylinderNo": 2,
        "deposit": "No"
      },
      {
        "cylinderNo": 3,
        "deposit": "Yes"
      },
      {
        "cylinderNo": 4,
        "deposit": "No"
      },
      {
        "cylinderNo": 5,
        "deposit": "Yes"
      }
    ],
    "comments": "test"
  }
]</code></pre>
<hr />
<h2>Error Handling</h2>
<p>The API uses standard HTTP status codes and provides detailed error information in the response body.</p>
<h3>HTTP Status Codes</h3>
<table>
<thead>
<tr>
<th>Status Code</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>200</td>
<td>Success</td>
</tr>
<tr>
<td>400</td>
<td>Bad Request - Invalid parameters or validation rule not met</td>
</tr>
<tr>
<td>401</td>
<td>Unauthorized - Authentication failed</td>
</tr>
<tr>
<td>403</td>
<td>Forbidden - Access denied</td>
</tr>
<tr>
<td>404</td>
<td>Not Found - Path not found</td>
</tr>
<tr>
<td>500</td>
<td>Internal Server Error</td>
</tr>
</tbody>
</table>
<h3>Error Response Formats</h3>
<h4>400 Bad Request</h4>
<pre><code class="language-json">{
  "error": {
    "errorCode": "BAD_REQUEST",
    "errorDateTime": "2025-10-10T12:00:00.000Z",
    "errorMessage": "At least one of dateCaptured, lastNSamples, or latestSample must be provided",
    "errorDescription": "The request parameters do not meet the validation requirements"
  }
}</code></pre>
<h4>401 Unauthorized</h4>
<pre><code class="language-json">{
  "fault": {
    "faultstring": "Invalid Access Token",
    "detail": {
      "errorcode": "keymanagement.service.invalid_access_token"
    }
  }
}</code></pre>
<h4>403 Forbidden</h4>
<pre><code class="language-json">{
  "error": {
    "errorCode": "FORBIDDEN",
    "errorDateTime": "2025-10-10T07:11:56.984Z",
    "errorMessage": "Access denied to the requested resource",
    "errorDescription": "Client does not have access to the selected resource",
    "additionalProp1": {}
  },
  "additionalProp1": {}
}</code></pre>
<h4>404 Not Found</h4>
<pre><code class="language-json">{
  "fault": {
    "faultstring": "/onboard-sample not found",
    "detail": {
      "errorcode": "PathNotFound"
    }
  }
}</code></pre>
<h4>500 Internal Server Error</h4>
<pre><code class="language-json">{
  "error": {
    "errorCode": "INTERNAL_SERVER_ERROR",
    "errorDateTime": "2025-10-10T07:11:56.984Z",
    "errorMessage": "The request could not be completed due to an internal error",
    "errorDescription": "Internal server error",
    "additionalProp1": {}
  },
  "additionalProp1": {}
}</code></pre>
<hr />
<h2>Data Models</h2>
<h3>Cylinder Data (Onboard)</h3>
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
<td><code>cylinderNo</code></td>
<td>integer</td>
<td>Cylinder number</td>
</tr>
<tr>
<td><code>pMax</code></td>
<td>number</td>
<td>Maximum pressure</td>
</tr>
<tr>
<td><code>fuelIndex</code></td>
<td>number</td>
<td>Fuel index value</td>
</tr>
<tr>
<td><code>coolingTempCOut</code></td>
<td>number</td>
<td>Cooling temperature outlet in Celsius</td>
</tr>
<tr>
<td><code>linerWallTempCMin</code></td>
<td>number</td>
<td>Minimum liner wall temperature in Celsius</td>
</tr>
<tr>
<td><code>linerWallTempCMax</code></td>
<td>number</td>
<td>Maximum liner wall temperature in Celsius</td>
</tr>
<tr>
<td><code>magneticIron</code></td>
<td>number</td>
<td>Magnetic iron content</td>
</tr>
<tr>
<td><code>feedrateSetpoint</code></td>
<td>number</td>
<td>Feed rate setpoint</td>
</tr>
<tr>
<td><code>bnMeasuresOnboard</code></td>
<td>number</td>
<td>BN measures onboard</td>
</tr>
<tr>
<td><code>corrosiveIron</code></td>
<td>number</td>
<td>Corrosive iron content</td>
</tr>
<tr>
<td><code>onboardTotalIron</code></td>
<td>number</td>
<td>Total iron content onboard</td>
</tr>
</tbody>
</table>
<h3>Running Data</h3>
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
<td><code>comments</code></td>
<td>string</td>
<td>General comments</td>
</tr>
<tr>
<td><code>oilGrade</code></td>
<td>string</td>
<td>Oil grade used</td>
</tr>
<tr>
<td><code>oilDensity</code></td>
<td>number</td>
<td>Oil density</td>
</tr>
<tr>
<td><code>totalEngineHours</code></td>
<td>number</td>
<td>Total engine running hours</td>
</tr>
<tr>
<td><code>rpm</code></td>
<td>number</td>
<td>Engine RPM</td>
</tr>
<tr>
<td><code>power</code></td>
<td>number</td>
<td>Engine power output</td>
</tr>
<tr>
<td><code>sulphur</code></td>
<td>number</td>
<td>Sulphur content</td>
</tr>
<tr>
<td><code>catfines</code></td>
<td>number</td>
<td>Cat fines content</td>
</tr>
<tr>
<td><code>vanadiumContent</code></td>
<td>number</td>
<td>Vanadium content</td>
</tr>
<tr>
<td><code>fuelConsumption</code></td>
<td>number</td>
<td>Fuel consumption rate</td>
</tr>
<tr>
<td><code>relHum</code></td>
<td>number</td>
<td>Relative humidity</td>
</tr>
<tr>
<td><code>ambientTemperature</code></td>
<td>number</td>
<td>Ambient temperature</td>
</tr>
<tr>
<td><code>scavAirTemp</code></td>
<td>number</td>
<td>Scavenge air temperature</td>
</tr>
<tr>
<td><code>engineRoomTC</code></td>
<td>number</td>
<td>Engine room temperature</td>
</tr>
<tr>
<td><code>cylinderOilCons</code></td>
<td>number</td>
<td>Cylinder oil consumption</td>
</tr>
<tr>
<td><code>sampleSentToLab</code></td>
<td>string</td>
<td>Whether sample was sent to lab ("Yes"/"No")</td>
</tr>
<tr>
<td><code>noOfTurboInUse</code></td>
<td>number</td>
<td>Number of turbos in use</td>
</tr>
<tr>
<td><code>feedRateCalculated</code></td>
<td>number</td>
<td>Calculated feed rate</td>
</tr>
</tbody>
</table>
<h3>Cylinder Data (Inspection)</h3>
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
<td><code>cylinderNo</code></td>
<td>integer</td>
<td>Cylinder number being inspected</td>
</tr>
<tr>
<td><code>deposit</code></td>
<td>string</td>
<td>Whether deposits were detected ("Yes"/"No")</td>
</tr>
</tbody>
</table>
<hr />
<h2>Rate Limiting</h2>
<p>Please refer to Shell Developer Portal for current rate limiting policies.</p>
<h2>Support</h2>
<p>For technical support and questions:</p>
<ul>
<li><strong>Email:</strong> LubesAPI@shell.com</li>
<li><strong>Documentation:</strong> <a href="https://developer.shell.com">Shell Developer Portal</a></li>
<li><strong>Support Portal:</strong> <a href="https://developer.shell.com/support">https://developer.shell.com/support</a></li>
</ul>
<h2>Terms of Service</h2>
<p>By using this API, you agree to the <a href="https://developer.shell.com/terms-of-use">Shell Terms of Use</a>.</p>
<hr />
<p><em>Last Updated: October 10, 2025</em></p></div>
      <span><span>Anonymous (not verified)</span></span>
<span><time datetime="2025-10-14T04:35:39+00:00" title="Tuesday, October 14, 2025 - 04:35">Tue, 10/14/2025 - 04:35</time>
</span>
