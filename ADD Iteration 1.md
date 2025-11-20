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
<th>Design Decisions and Location</th>
<th colspan="2">Rationale</th>
</tr>
<tr>
<td>Logically structure the system using the Rich Internet Application (RIA) reference architecture.</td>
<td colspan="2">The reference architecture RIA supports the necessary conversational multi-device interfaces of AIDAP, namely text, voice, mobile, and web. It enables client-side business logic and caching while connecting to institutional services (LMS, registration, calendars) using service interfaces.</td>
</tr>
<tr>
<td rowspan="3"></td>
<td colspan="2">Discarded Alternatives</td>
</tr>
<tr>
<td>Alternative</td>
<td>Reason for Discarding</td>
</tr>
<tr>
<td>Web Applications</td>
<td>Although web applications bring portability and ease of deployment, they fall short in offering a rich, conversational UI experience across modalities.</td>
</tr>
<tr>
<td>Rich Client Applications</td>
<td>Require installation and maintenance on every user's device. Too heavy for AIDAP.</td>
</tr>
<tr>
<td>Mobile Applications</td>
<td>Narrow in scope, rely on device resources, conflict with accessibility and scalability requirements.</td>
</tr>
</table>

<!-- More tables and figures continue in the same format... -->
