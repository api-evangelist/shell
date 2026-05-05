---
title: "Version Change Document"
url: "https://developer.shell.com/api-catalog/ev-public-locations/version-change-document"
date: "Fri, 30 Jan 2026 16:26:52 +0000"
author: ""
feed_url: "https://developer.shell.com/rss.xml"
---
<span>Version Change Document</span>

            <div class="has-button has-list field field--body field--label-hidden field__item"><h1 class="text-align-center"><strong>Version Change Document</strong></h1>
<p>There is a breaking change in the EV Location API. The current v1 endpoint will be decommissioned on <span><strong>31st March 2026</strong></span>. Customers using v1 are advised to plan their migration to v2.</p>
<p>The core API concepts remain unchanged; however, v2 introduces several technical adjustments, such as updated data types for certain parameters and the removal of non‑relevant or not consistently reliable fields.</p>
<p>The sections below explain the changes in detail.</p>
<h2><span><strong>Authentication</strong></span></h2>
<ol>
<li>The authentication endpoint is unchanged, and the existing OAuth endpoint remains in use.</li>
</ol>
<h2><span><strong>Versioning of the APIs</strong></span></h2>
<ol>
<li>Only the base URL for all four location endpoints has been updated from v1 to v2. The endpoint paths themselves remain unchanged.
<ol>
<li>Old Base URL - <a href="https://api.shell.com/ev/v1/locations">https://api.shell.com/ev/<span><strong>v1</strong></span>/locations</a></li>
<li>New Base URL - <a href="https://api.shell.com/ev/v2/locations">https://api.shell.com/ev/<span><strong>v2</strong></span>/locations</a></li>
</ol>
</li>
</ol>
<h2><span><strong>Change details on 3 endpoints: /locations, /id, /nearby</strong></span></h2>
<ol>
<li>Data Type changes in Response payload
<ol>
<li>The response now includes three UUID fields (Location UUID, EVSE UUID, Connector UUID). Previously, these values were provided as integers. They have now all been updated to string data types to ensure proper UUID formatting and consistency.</li>
<li>Below are the exact parameter names in the response payload.
<ol>
<li>Data.uid</li>
<li>Data.evses.uid</li>
<li>Data.evses.connectors.uuid</li>
</ol>
</li>
</ol>
</li>
<li>The following parameters have been removed in version v2.
<ol>
<li>Data.accessibility.remark</li>
<li>data.operatorComment</li>
<li>Data.evse.connectors.deleted</li>
<li>Data.evse.connectors.fixedCable</li>
<li><strong>Data.evse.connectors.tariff</strong></li>
<li>Data.evse.connectors.updated</li>
<li>Data.evse.connectors.updatedBy</li>
<li>Data.evse.deleted</li>
<li>Data.evse.physicalReference</li>
</ol>
</li>
</ol>
<blockquote><p>Please note that the tariff component is made available in <strong>/locations/id&nbsp;</strong>endpoint.<strong>&nbsp;</strong>Tariff information can be fetched only per location.&nbsp;</p>
</blockquote>
<h2><span><strong>Change details on /locations/markers endpoint</strong></span></h2>
<ol>
<li>Three parameters have been removed from the response payload in v2.
<ol>
<li>Data.geoHash</li>
<li>Data.markerType</li>
<li>Data.uniquekey</li>
</ol>
</li>
</ol>
<h2><span><strong>Tariff Details</strong></span></h2>
<p>The tariff details will be available only in the locations/id end point which means, tariff details can be fetched only per location and not in bulk. This change is due to the dynamic pricing feature that has been enabled in our product.&nbsp;</p>
<p>Also, to fetch the tariff info, <strong>ProviderID is mandatory in the query parameter</strong>. ProviderId will be shared by Shell.&nbsp;</p>
<p>Below is a sample tariff component for reference.&nbsp;</p>
<pre><code class="language-json hljs yaml"><span class="hljs-attr">"tariffs":</span> <span class="hljs-string">[</span>
    <span class="hljs-string">{</span>
      <span class="hljs-attr">"createdBy":</span> <span class="hljs-string">"STAGE_TEST1"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"currency":</span> <span class="hljs-string">""</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"elements":</span> <span class="hljs-string">[</span>
        <span class="hljs-string">{</span>
          <span class="hljs-attr">"priceComponents":</span> <span class="hljs-string">[</span>
            <span class="hljs-string">{</span>
              <span class="hljs-attr">"price":</span> <span class="hljs-number">1.7208002</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"stepSize":</span> <span class="hljs-number">1</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"type":</span> <span class="hljs-string">"ENERGY"</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"vat":</span> <span class="hljs-number">21</span>
            <span class="hljs-string">}</span>
          <span class="hljs-string">]</span>
        <span class="hljs-string">},</span>
        <span class="hljs-string">{</span>
          <span class="hljs-attr">"priceComponents":</span> <span class="hljs-string">[</span>
            <span class="hljs-string">{</span>
              <span class="hljs-attr">"price":</span> <span class="hljs-number">4.1202</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"stepSize":</span> <span class="hljs-number">10</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"type":</span> <span class="hljs-string">"TIME"</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"vat":</span> <span class="hljs-number">8</span>
            <span class="hljs-string">}</span>
          <span class="hljs-string">]</span>
        <span class="hljs-string">},</span>
        <span class="hljs-string">{</span>
          <span class="hljs-attr">"priceComponents":</span> <span class="hljs-string">[</span>
            <span class="hljs-string">{</span>
              <span class="hljs-attr">"price":</span> <span class="hljs-number">0.84033614</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"stepSize":</span> <span class="hljs-number">1</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"type":</span> <span class="hljs-string">"FLAT"</span><span class="hljs-string">,</span>
              <span class="hljs-attr">"vat":</span> <span class="hljs-number">19</span>
            <span class="hljs-string">}</span>
          <span class="hljs-string">]</span>
        <span class="hljs-string">}</span>
      <span class="hljs-string">],</span>
      <span class="hljs-attr">"endDateTime":</span> <span class="hljs-string">"2026-09-02T15:03:09Z"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"internalId":</span> <span class="hljs-string">"CH*FR*SHE*9ddc09f2-1a66-47e9-b6f3-40b0d55tt923"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"lastUpdated":</span> <span class="hljs-string">"2025-09-10T08:43:09Z"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"maxPrice":</span> <span class="hljs-number">999</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"minPrice":</span> <span class="hljs-number">0</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"operatorId":</span> <span class="hljs-string">"FR*SHE"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"powerRange":</span> <span class="hljs-string">{</span>
        <span class="hljs-attr">"max":</span> <span class="hljs-number">150</span><span class="hljs-string">,</span>
        <span class="hljs-attr">"min":</span> <span class="hljs-number">0</span>
      <span class="hljs-string">},</span>
      <span class="hljs-attr">"providerId":</span> <span class="hljs-string">"Shell_RP_2"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"startDateTime":</span> <span class="hljs-string">"2026-01-21T08:43:09Z"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"tariffAltText":</span> <span class="hljs-literal">null</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"tariffId":</span> <span class="hljs-string">"9ddc09f2-1a66-47e9-b6f3-40b0d55tt923"</span><span class="hljs-string">,</span>
      <span class="hljs-attr">"tariffType":</span> <span class="hljs-string">"DRIVER"</span>
    <span class="hljs-string">}</span>                              
<span class="hljs-string">]</span></code></pre><h2>Support</h2>
<ol>
<li>
<p>If you require assistance or have questions, please contact our technical team by raising a support ticket:</p>
<p class="text-align-center">&nbsp;<a href="https://developer.shell.com/support-tickets/create?request_topic=Request%20for%20information&amp;destination=/support"><span class="tag tag--outlined">Raise a ticket</span></a></p>
</li>
</ol>
</div>
      <span><time datetime="2026-01-30T16:26:52+00:00" title="Friday, January 30, 2026 - 16:26">Fri, 01/30/2026 - 16:26</time>
</span>
