# Taking rostered attendance via a Flow in SFDO's Program Management Module

## Overview
<p>This repository contains an unmanaged declarative screen Flow that assists with taking roster-based attendance as part of <a href="https://powerofus.force.com/s/article/PMM-Documentation">Salesforce's Program Management Module (PMM)</a>.</p>
<p>PMM version 1.17 (11/05/2020) included new functionality for Service Schedules, Service Participants, and Service Sessions. Expanding on this new functionality, this screen Flow allows users to take roster-based attendance for an entire Service Session at once for all Service Participants, rather than one-by-one through Service Deliveries or Bulk Service Deliveries as currently configured through PMM.</p>
<p><em>Note: PMM is required to be installed in order for this add-on to work in your org. Download/install PMM on <a href="https://install.salesforce.org/products/">Salesforce.org's Product Page</a>.</em></p>


## Included Custom Fields
<p>The following custom fields are included as part of this deployment:</p>
<ul>
  <li><strong>Service Delivery object -- Status (Picklist)</strong></li>
    <ul><li>Provides the ability to denote the attendance status via "Attended," "Absent - No Show," and "Absent - Excused" options</li></ul>
  <li><strong>Service Participant object -- Contact Name (Formula Text)</strong></li>
    <ul><li>Concatenated version of First Name and Last Name. This allows the Flow to display the full name of the client using a single field for attendance purposes</li></ul>
  <li><strong>Service Session object -- Start Date (Formula Date)</strong></li>
    <ul><li>Used to convert Date/Time of Session Start Date to a Date field in order to filter out Participants who signed up <em>after</em> the date of this session</li></ul>
</ul>

## Flow Details
<p>This Flow is launched using an action (included) from the Service Session record and finds all Service Participants for the parent Service Schedule. Note: by default, the Flow finds only Service Participants with a sign-up date of prior to this Service Session---though this can be edited in the Flow.<p>

<a href="https://githubsfdeploy.herokuapp.com/app/githubdeploy/907pine/PMM_Attendance_Flow">
  <img src="https://raw.githubusercontent.com/afawcett/githubsfdeploy/master/src/main/webapp/resources/img/deploy.png" alt="Deploy to Salesforce" />
</a>
