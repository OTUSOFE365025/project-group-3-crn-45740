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


<h2>Step 2: Establish the iteration goal by selecting drivers</h2>

<ul>
  <li><strong>QA-1: Performance</strong> – Ensure the system responds within 2 seconds for typical queries; optimize read-heavy endpoints via caching.</li>
  <li><strong>QA-2: Availability</strong> – Achieve 99.5% uptime; implement autoscaling, health checks, and failover strategies across all tiers.</li>
  <li><strong>QA-3: Security</strong> – Complete SSO integration; implement token validation and role-based access control.</li>
  <li><strong>CRN-3: Integration Reliability</strong> – Ensure adapters handle retries, errors, and rate limits.</li>
  <li><strong>CON-2: Integration with University Systems</strong> – Use secure, standardized APIs for all external system integrations without disrupting workflows.</li>
  <li><strong>CON-6: Cloud-Native Deployment</strong> – Deploy system to the cloud using CI/CD pipelines; support containerized services and auto-failover.</li>
</ul>


<h2>Step 3: Choose one or more elements to decompose</h2>

<ul>
  <li><strong>Services Layer</strong>
    <ul>
      <li>API Gateway / Backend-for-Frontend – entry points for client requests</li>
      <li>Authentication Service – manages SSO, role-based access</li>
      <li>Notification Service – handles announcements, reminders, anomaly alerts</li>
      <li>Query Service – provides course schedules, deadlines, and analytics</li>
      <li>Monitoring Service – exposes system health, latency, and usage metrics</li>
    </ul>
  </li>
  <li><strong>Business Layer</strong>
    <ul>
      <li>Natural Language Processing Module – interprets user queries</li>
      <li>Response Composition Module – combines stored history with live data</li>
      <li>Workflow Manager – manages reminders, broadcasts, anomaly detection</li>
      <li>Policy Enforcer – enforces global rules (privacy, compliance, role restrictions)</li>
      <li>Business Entities – core domain objects: course, schedule, announcement, user, role</li>
    </ul>
  </li>
  <li><strong>Data Layer</strong>
    <ul>
      <li>Persistence of interactions – stores historical conversations and preferences</li>
      <li>Course/Schedule/Announcement Repository – maintains academic data</li>
      <li>Notification/Event Repository – stores announcements, reminders, anomaly events</li>
      <li>Preferences Repository – saves user settings</li>
      <li>Cache – fast retrieval and offline support</li>
      <li>Backup/Recovery Module – ensures high availability and backup recovery</li>
      <li>Integration Data Adapters – sync data from LMS, Registration, Calendar, Email</li>
    </ul>
  </li>
</ul>


<h2>Step 4: Choose one or more design concepts that satisfy the selected driver</h2>

<table>
  <tr>
    <th>Design Decision</th>
    <th>Rationale</th>
  </tr>
  <tr>
    <td>Cache-aside Pattern with Redis</td>
    <td>Optimizes read-heavy endpoints (schedules, announcements), improving QA-1 Performance by reducing external system calls.</td>
  </tr>
  <tr>
    <td>SSO Integration (OIDC/SAML)</td>
    <td>Completes QA-3 Security by authenticating users via institutional IdP and enforcing role-based access control.</td>
  </tr>
  <tr>
    <td>Autoscaling &amp; Health Checks</td>
    <td>Ensures QA-2 Availability with automatic scaling, failover, and health monitoring of all tiers.</td>
  </tr>
  <tr>
    <td>Monitoring &amp; Logging</td>
    <td>Provides observability into latency, errors, and uptime; supports operational decision-making and early detection of integration failures (QA-2, CRN-3).</td>
  </tr>
  <tr>
    <td>Distributed Deployment / Cloud-Native</td>
    <td>Supports scalability and reliability requirements (CON-6); allows independent scaling of presentation, business, and integration tiers.</td>
  </tr>
</table>


<h2>Step 5: Instantiate architectural elements, allocate responsibilities, and define interfaces</h2>

<table>
  <tr>
    <th>Design Decision</th>
    <th>Rationale</th>
  </tr>
  <tr>
    <td>Introduce integration adapters (LMS, Registration, Calendar, Email) in the Integration Layer</td>
    <td>
      Abstract external APIs, handle retries, error logging, and rate limiting. Supports CRN-3 (integration reliability) and CON-2 (secure integration).
    </td>
  </tr>
  <tr>
    <td>Create Domain Objects (Course, Schedule, Announcement, User, Role, Event) in the Business Logic Layer</td>
    <td>
      Encapsulate academic entities to provide a consistent internal representation. Supports UC-1, UC-2, UC-6.
    </td>
  </tr>
  <tr>
    <td>Implement the Cache-aside pattern with Redis in the Data Layer</td>
    <td>
      Optimize read-heavy endpoints (schedules, announcements), improving QA-1 (performance).
    </td>
  </tr>
  <tr>
    <td>Instantiate the security and identity module with OIDC/SAML</td>
    <td>
      Completes QA-3 (Security) by authenticating users via institutional IdP and enforcing role-based access control.
    </td>
  </tr>
  <tr>
    <td>Add Monitoring &amp; Logging Subsystem in the System Management Layer</td>
    <td>
      Provides observability into latency, errors, and uptime; supports QA-2 (availability) and CRN-5 (fault tolerance).
    </td>
  </tr>
</table>

<h2>Step 6: Sketch views and record design decisions</h2>

Reference Architecture:

<img width="500" height="900" alt="image" src="https://github.com/user-attachments/assets/823998ff-ce9f-4b65-af0e-d6635d495140" />



<h4>Client Side Components</h4>
<table>
  <tr>
    <th>Component</th>
    <th>Responsibility</th>
  </tr>
  <tr>
    <td>ConversationController</td>
    <td>Manages chat panel, voice input, and text queries.</td>
  </tr>
  <tr>
    <td>DashboardController</td>
    <td>Displays widgets, schedules, analytics, and notifications.</td>
  </tr>
  <tr>
    <td>PreferencesUI</td>
    <td>Allow users to set language, notification, and personalization options.</td>
  </tr>
  <tr>
    <td>NotificationCenterUI</td>
    <td>Shows announcements, reminders, and alerts.</td>
  </tr>
  <tr>
    <td>LocalStorageAdapter</td>
    <td>Interfaces with browser IndexedDB for offline cache.</td>
  </tr>
</table>

<h4>Server Components</h4>
<table>
  <tr>
    <th>Component</th>
    <th>Responsibility</th>
  </tr>
  <tr>
    <td>APIGateway</td>
    <td>Routes client requests to backend services (REST/GraphQL, WebSocket).</td>
  </tr>
  <tr>
    <td>AuthService</td>
    <td>Handles SSO login, token validation, and role enforcement.</td>
  </tr>
  <tr>
    <td>NotificationService</td>
    <td>Manages announcements, reminders, and anomaly alerts.</td>
  </tr>
  <tr>
    <td>QueryService</td>
    <td>Provides course schedules, deadlines, and analytics.</td>
  </tr>
  <tr>
    <td>MonitoringService</td>
    <td>Collects system health, latency, and usage metrics.</td>
  </tr>
  <tr>
    <td>NLPProcessor</td>
    <td>Interprets natural-language queries.</td>
  </tr>
  <tr>
    <td>ResponseComposer</td>
    <td>Builds contextual answers using history.</td>
  </tr>
  <tr>
    <td>WorkflowManager</td>
    <td>Manages reminders, broadcasts, and anomaly detection.</td>
  </tr>
  <tr>
    <td>PolicyManager</td>
    <td>Enforces privacy, compliance, and role restrictions.</td>
  </tr>
  <tr>
    <td>SessionManager</td>
    <td>Maintains active user sessions and roles.</td>
  </tr>
  <tr>
    <td>BusinessEntities</td>
    <td>Domain objects: course, schedule, announcement, user, role.</td>
  </tr>
  <tr>
    <td>InteractionRepository</td>
    <td>Stores historical conversations and interactions.</td>
  </tr>
  <tr>
    <td>CourseRepository</td>
    <td>Maintains course data and schedules.</td>
  </tr>
  <tr>
    <td>AnnouncementRepository</td>
    <td>Persists announcements and notifications.</td>
  </tr>
  <tr>
    <td>PreferencesRepository</td>
    <td>Saves user settings.</td>
  </tr>
  <tr>
    <td>BackupManager</td>
    <td>Ensures high availability and disaster recovery.</td>
  </tr>
  <tr>
    <td>ValidationUtility</td>
    <td>Input validation, multilingual support, formatting.</td>
  </tr>
  <tr>
    <td>DataAdapters</td>
    <td>Normalize and sync data from LMS, Registration, Calendar, Email.</td>
  </tr>
  <tr>
    <td>SecurityModule</td>
    <td>Enforces authentication, authorization, and compliance.</td>
  </tr>
  <tr>
    <td>OperationalMonitor</td>
    <td>Logging, monitoring, error handling.</td>
  </tr>
  <tr>
    <td>CommunicationSDK</td>
    <td>Provides standardized libraries for communication, notifications, and work modules.</td>
  </tr>
</table>

-----------------------------------------------------------------------------------------------------------------------------

Sequence Diagram for UC-1: Provide authoritative access to schedules, grades, deadlines, and course data (core assistant functionality).

<img width="1500" height="325" alt="image" src="https://github.com/user-attachments/assets/3aebc326-b7ac-422f-a6b9-a42acb046523" />

-----------------------------------------------------------------------------------------------------------------------------

Sequence Diagram for UC-2: Support engagement and communication: push reminders, campus announcements, and anomaly alerts.

<img width="1500" height="325" alt="image" src="https://github.com/user-attachments/assets/6481c1df-ecc1-40a1-99f2-d79ebf54a891" />

-----------------------------------------------------------------------------------------------------------------------------

Sequence Diagram for UC-6: Ensure scalability, uptime, and monitoring capabilities to support institutional reliability and trust.

Monitoring:

<img width="1500" height="325" alt="image" src="https://github.com/user-attachments/assets/359a2a98-5d67-4184-a67c-074aa235817a" />

-----------------------------------------------------------------------------------------------------------------------------

Failure Detection and Recovery:

<img width="1500" height="325" alt="image" src="https://github.com/user-attachments/assets/f0887fcf-6e41-40bc-a365-e73ecbe73e43" />



