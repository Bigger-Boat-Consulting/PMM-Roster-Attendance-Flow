# Taking rostered attendance via a Flow in SFDO's Program Management Module (PMM)

## Overview
<p>This repository contains an unmanaged declarative screen Flow that assists with taking roster-based attendance as part of <a href="https://powerofus.force.com/s/article/PMM-Documentation">Salesforce's Program Management Module (PMM)</a>.</p>
<p>SFDO's PMM version 1.17 (11/05/2020) included new functionality for Service Schedules, Service Participants, and Service Sessions. Expanding on this new functionality, this screen Flow allows users to take roster-based attendance for an entire Service Session at once for all Service Participants, rather than one-by-one through Service Deliveries or Bulk Service Deliveries as currently configured through PMM.</p>
<p>The flow finds all Service Participants for a particular Service Session and asks the user which participants attended that session. A secondary flow screen is displayed for each individual that was not selected as "attended." This screen allows the user to select whether the absence was a "no show" or "excused." The flow then mass creates Service Delivery records with the attendance status added to the Service Delivery with a default quantity of 1 for attendees and 0 for absentees.</p> 
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
<p>This screen Flow is launched using an Action (included in this package) from the Service Session record and finds all Service Participants for the parent Service Schedule. This package also includes a Lightning Page with for the Service Session with the Action included.</p>
<p>The Flow finds the parent Service Schedule for this Session and gathers all Service Participants for that Schedule (<em>Note: by default, the Flow finds only Service Participants with a sign-up date of prior to this Service Session---though this can be edited in the Flow.</em>).</p>
<p>The user is displayed a list of those participants and asked to mark who attended this session. The Flow then loops through the list of participants and sets output variables of 1 for quantity and "Attended" for those selected. Any individuals that were not selected are displayed on subsequent screens, where the user is asked to select their absence type: "Excused" or "No show." Those answers (along with those from the attendees) are written to an output variable.</p>
<p>The Flow ends with Service Delivery records created en masse (outside the loop for bulkification purposes) with the appropriate client and attendance status, as well as a quantity of 1 for attendees and 0 for absentees.</p>

<a href="https://githubsfdeploy.herokuapp.com/app/githubdeploy/907pine/PMM_Attendance_Flow">
  <img src="https://raw.githubusercontent.com/afawcett/githubsfdeploy/master/src/main/webapp/resources/img/deploy.png" alt="Deploy to Salesforce" />
</a>
