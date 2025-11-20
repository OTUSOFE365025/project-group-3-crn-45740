<h1>Iteration 2: Identifying Structures to Support Primary Functionality</h1>

<h2>Step 1: Review Inputs</h2>

<table>
  <tr>
    <td>Category</td>
    <td colspan="3">Details</td>
  </tr>
  <tr>
    <td>Design Purpose</td>
    <td colspan="3">
      The AIDAP project is a brownfield system in a mature domain (conversational AI + academic systems). The purpose is to design a platform that integrates with existing university systems while providing novel, student-centric conversational functionality across text, voice, mobile, and web.
    </td>
  </tr>
  <tr>
    <td>Primary Functional Requirements</td>
    <td colspan="3">
      From the use cases, the primary ones were determined to be:<br>
      UC-1: Provide authoritative access to schedules, grades, deadlines, and course data (core assistant functionality).<br>
      UC-2: Support engagement and communication: push reminders, campus announcements, and anomaly alerts.<br>
      UC-6: Ensure scalability, uptime, and monitoring capabilities to support institutional reliability and trust.
    </td>
  </tr>
  <tr>
    <td rowspan="5">Quality Attribute Scenarios</td>
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
    <td>Constraint</td>
    <td colspan="3">
      The system must integrate with all university services via secure APIs while maintaining 99.5% uptime and supporting 5,000 concurrent users.
    </td>
  </tr>
  <tr>
    <td>Architectural Concern</td>
    <td colspan="3">
      The system must ensure reliable and secure communication between all modules, including adapters, caching, and SSO components, to maintain performance and fault tolerance.
    </td>
  </tr>
</table>
