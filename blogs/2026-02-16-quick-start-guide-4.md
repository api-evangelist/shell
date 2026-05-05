---
title: "Quick Start Guide"
url: "https://developer.shell.com/api-catalog/b2b-mobility-card-management/quick-start-guide-21"
date: "Mon, 16 Feb 2026 08:38:43 +0000"
author: "Anonymous"
feed_url: "https://developer.shell.com/rss.xml"
---
<span>Quick Start Guide</span>

            <div class="has-button has-list field field--body field--label-hidden field__item"><h2>Card Management Push Notifications</h2>
<p>Card Management Push notification API sends status information of the card order, block and unblock  Notifications messages to Partner system once the process has been completed at shell side.</p>
<h2>Subscription Process</h2>
<p><b> Step 1 </b></p>
<p>To subscribe this feature certain details required from Partner side such as  API details and authentication information.</p>
<p>Shell notifications API will push the notifications to Partner provided REST API. Notifications API schema differs based on functionality (ordercard, updatestatus..) so individual API required from partner side to receive respective notifications.</p>
<p>The below details required from partner system to push Card notifications</p>
<table>
<thead>
<tr>
<th>API Details</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td>API URL</td>
<td>API URL  which will<br />receive the notifications<br />messages from shell<br />systems</td>
<td><a href="https://hostname/ordercard/notifications">https://hostname/ordercard/notifications</a></td>
</tr>
<tr>
<td>Authentication Details</td>
<td>Authentication information of the API which is going to receive notifications</td>
<td>Basic Auth , API key based</td>
</tr>
<tr>
<td>Mandatory<br />headers<br />information</td>
<td>If there is any specific header required at partner system side while pushing the notifications</td>
<td>Custom headers<br />"system":"shellfleet"</td>
</tr>
</tbody>
</table>
<p><b>Step 2 </b></p>
<p>Send the above mentioned details to api@shell.com to enable notifications at shell side.</p>
<p><b> Step 3 </b></p>
<p>Once the Notifications enabled at our side we will send the confirmation mail  with the relevant details about the notification </p>
<p>Notification message structure and schema definitions please refer the Card Management Notifications OpenAPI spec</p></div>
      <span><span>Anonymous (not verified)</span></span>
<span><time datetime="2026-02-16T08:38:43+00:00" title="Monday, February 16, 2026 - 08:38">Mon, 02/16/2026 - 08:38</time>
</span>
