<h1>Iteration 1: Establish Overall System Structure</h1>

<h2>Step 1: Review Inputs</h2>

<table>
<tr>
<td>Category</td>
<td colspan="3">Details</td>
</tr>
<tr>
<td>Design Purpose</td>
<td colspan="3">The AIDAP project is a brownfield system in a mature domain (conversational AI + academic systems). The purpose is to design a platform that integrates with existing university systems while providing novel, student-centric functionality.</td>
</tr>
<tr>
<td rowspan="4">Primary Functional Requirements</td>
<td colspan="3">From the use cases, the primary ones were determined to be:</td>
</tr>
<tr>
<td colspan="3">UC-1: As it directly supports the assistant's core business. Students and lecturers rely on it to retrieve schedules, grades, deadlines, and course data (see QA-1: Performance and QA-4: Usability).</td>
</tr>
<tr>
<td colspan="3">UC-2: As it ensures engagement and communication. Critical for deadlines, anomalies, and campus-wide announcements. Linked to QA-4: Usability.</td>
</tr>
<tr>
<td colspan="3">UC-6: Chosen because of the technical issues associated with scalability, uptime, and monitoring (QA-2: Availability). It underpins reliability and institutional Trust</td>
</tr>
<tr>
<td rowspan="6">Quality Attribute Scenarios</td>
<td colspan="3"></td>
</tr>
<tr>
<td>Scenario ID</td>
<td>Importance to Customer</td>
<td>Difficulty of Implementation According to the Architect</td>
</tr>
<tr>
<td>QA-1</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>QA-2</td>
<td>High</td>
<td>Medium</td>
</tr>
<tr>
<td>QA-3</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>QA-4</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>Constraints</td>
<td colspan="3">All constraints were chosen to be architectural drivers.</td>
</tr>
</table>

<h2>Step 2: Establish the iteration goal by selecting drivers</h2>

<ul>
<li>QA-1: Performance</li>
<li>QA-2: Availability</li>
<li>QA-3: Security</li>
<li>QA-4: Usability</li>
<li>CON-1: The system must comply with institutional security and privacy regulations, ensuring protection of the users' data.</li>
<li>CON-2: AIDAP must be integrated into existing university systems (LMS, registration, calendars, and email) with secure APIs.</li>
<li>CON-3: The system must offer high availability (99.5% monthly uptime) and scalability for 5,000 concurrent users as a minimum.</li>
<li>CON-4: The system must ensure secure authentication and authorization via institutional Single Sign-On (SSO) and role-based permission.</li>
<li>CON-6: The system must be deployable as a cloud-native environment with continuous deployment and auto-failover recovery capability.</li>
<li>CRN-1: Data Privacy and Security</li>
<li>CRN-2: Scalability and Performance</li>
<li>CRN-3: Integration Reliability</li>
<li>CRN-5: Availability and Fault Tolerance</li>
</ul>

<h2>Step 3: Choose one or more elements to decompose</h2>

<ul>
<li><strong>Conversational Interface Layer</strong> – Handles text/voice input, NLP, and multilingual support</li>
<li><strong>Data Layer (Data Access Services)</strong> – Connects to LMS, registration, calendars, and email</li>
<li><strong>Cross-Cutting</strong> – Manages SSO, role-based access, and compliance</li>
<li><strong>Notification and Event Module</strong> – Pushes reminders, announcements, anomaly alerts</li>
<li><strong>Analytics and Personalization Engine</strong> – Provides dashboards, performance summaries, and anomaly detection</li>
<li><strong>System Management and Monitoring Module</strong> – Tracks uptime, latency, errors, and supports failover</li>
</ul>

<h2>Step 4: Choose one or more design concepts that satisfy the selected driver</h2>

<table>
  <tr>
    <td>Design Decision</td>
    <td>Rationale</td>
  </tr>
  <tr>
    <td>Rich Internet Application (RIA) Reference Architecture</td>
    <td>
      Supports conversational multi-device interfaces (text, voice, mobile, web). Enables client-side business logic and caching while connecting to institutional services (LMS, registration, calendars) using service interfaces. Directly fulfils requirements for interoperability (R3, RD2), usability (RS9, RS12), and performance (RS10). Security and operational management components match privacy and availability requirements (R8, RS7, RA5, RA6).
    </td>
  </tr>
  <tr>
    <td>Three-Tier Distributed Deployment Pattern</td>
    <td>
      Separates presentation, business, and integration tiers. Supports scalability (RA7), high availability (RA6), and performance (RS10). Aligns with cloud-native deployment (R7) and allows independent scaling of tiers. Integration tier is critical for connecting to external university systems (RD1–RD4).
    </td>
  </tr>
  <tr>
    <td>Discarded Alternatives</td>
    <td>
      <table>
        <tr>
          <td>Alternative</td>
          <td>Reason for Discarding</td>
        </tr>
        <tr>
          <td>Web Applications</td>
          <td>Bring portability and ease of deployment but fall short in offering a rich, conversational UI experience across modalities (voice, text, multi-language). Lack advanced interaction and personalisation features expected in AIDAP.</td>
        </tr>
        <tr>
          <td>Rich Client Applications</td>
          <td>Provide high interactivity but require installation and maintenance on every user's device. Too heavy for AIDAP, which must be cloud-native and available across mobile, web, and voice assistants. Complicates deployment and updates.</td>
        </tr>
        <tr>
          <td>Mobile Applications</td>
          <td>Useful for handheld devices but narrow in scope. Do not enrich the multi-channel conversational interface required by AIDAP. Strongly rely on device resources and connectivity, conflicting with accessibility and scalability requirements.</td>
        </tr>
      </table>
    </td>
  </tr>
</table>


<h2>Step 5: Instantiate architectural elements, allocate responsibilities, and define interfaces</h2>

<table>
  <tr>
    <td>Design Decision</td>
    <td>Rationale</td>
  </tr>
  <tr>
    <td>Instantiate the Presentation + Rich UI Engine from the Rich Internet Application reference architecture for the client side.</td>
    <td>
      Provides conversational, multi-device access (web, mobile, voice) and supports personalisation and caching. Directly satisfies RS9, RS12, RS14.
    </td>
  </tr>
  <tr>
    <td>Create Service Interfaces and Domain Objects in the server tier.</td>
    <td>
      Service Interfaces abstract external systems (LMS, registration, calendars, mail) while Domain Objects encapsulate academic entities (Course, Schedule, Announcement). This supports interoperability (R3, RD2) and modifiability (RM5).
    </td>
  </tr>
  <tr>
    <td>Define a Data Mapper layer with cross-cutting Security and Operational Management components.</td>
    <td>
      Data Mapper handles persistence of personalisation/history (R2, RS5). Security ensures SSO, privacy, and compliance (RS7, RS8, RA5). Operational Management supports monitoring, logging, and availability (RA4, RA6).
    </td>
  </tr>
</table>
