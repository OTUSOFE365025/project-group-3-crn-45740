**Add Iteration 1**

Step 1: Review Inputs

<h1>Iteration 1: Establish Overall System Structure</h1>

<h2>Step 1: Review Inputs</h2>

<table>
  <tr>
    <td>Category</td>
    <td colspan="3">Details</td>
  </tr>
  <tr>
    <td>Design Purpose</td>
    <td colspan="3">
      The AIDAP project is a brownfield system in a mature domain (conversational AI + academic systems).
      The purpose is to design a platform that integrates with existing university systems while providing
      novel, student-centric functionality.
    </td>
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
</table>

<h2>Step 2: Establish the iteration goal by selecting drivers</h2>

<ul>
  <li>QA-1: Performance</li>
  <li>QA-2: Availability</li>
  <li>QA-3: Security</li>
  <li>QA-4: Usability</li>
  <li>CON-1: The system must comply with institutional security and privacy regulations, ensuring protection of the users' data.</li>
  <li>CON-2: AIDAP must be integrated into existing university systems (LMS, registration, calendars, and email) with secure APIs.</li>
</ul>
