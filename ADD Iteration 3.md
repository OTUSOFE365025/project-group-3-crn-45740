<h2>Iteration 3: Addressing Quality Attribute Scenario Driver (QA-3)</h2>

<h3>Step 1: Review Inputs</h3>
<p>(Already done in prior iterations).</p>

<h3>Step 2: Establish the Iteration Goal by Selecting Drivers</h3>
<p>
For this iteration, the primary focus will be on <strong>QA-2 Availability Scenario</strong>:  
If a fault or system failure is detected, AIDAP will back up and recover the data.  
The system should maintain an uptime of 99.5% per month.  
The other quality attributes, QA-1 Performance and QA-4 Usability, will also be addressed.
</p>

<h3>Step 3: Choose one or more elements of the system to refine</h3>
<ul>
  <li><strong>Services Layer</strong>
    <ul>
      <li><strong>Monitoring Service</strong> – selected because availability requires proactive detection of anomalies and service health. By refining this element, latency, errors, and heartbeat signals can be continuously tracked and addressed.</li>
    </ul>
  </li>
  <li><strong>Data Layer</strong>
    <ul>
      <li><strong>Backup/Recovery Module</strong> – chosen because recovery from faults is essential to availability. This module ensures data integrity and service continuity through redundancy, rollback, and synchronization tactics.</li>
    </ul>
  </li>
</ul>

<h3>Step 4: Choose one or more design concepts that satisfy the selected drivers</h3>
<table>
  <tr>
    <th>Design Decision and Location</th>
    <th>Rationale</th>
  </tr>
  <tr>
    <td>Implement the condition monitoring tactic by adding a ConditionMonitor module inside the Monitoring Service.</td>
    <td>Detects anomalies and errors so administrators can trace and resolve problems quickly.</td>
  </tr>
  <tr>
    <td>Introduce the monitor tactic by adding the HealthMonitor module inside the Monitoring Service.</td>
    <td>Provides constant updates on system health metrics, detects non-responsive nodes, and logs uptime/downtime events.</td>
  </tr>
  <tr>
    <td>Implement redundant spare and rollback tactic by replicating database servers and maintaining them.</td>
    <td>Ensures duplicated database servers can take over if the primary server fails, supporting recovery and continuity.</td>
  </tr>
</table>

<h3>Step 5: Instantiate architectural elements, allocate responsibilities, and define interfaces</h3>
<table>
  <tr>
    <th>Element</th>
    <th>Responsibility</th>
  </tr>
  <tr>
    <td>ConditionMonitor module</td>
    <td>Collects system metrics (CPU, latency, error rates) and evaluates them against thresholds to detect anomalies.</td>
  </tr>
  <tr>
    <td>HealthMonitor module</td>
    <td>Monitors system components, detects non-responsive nodes, and logs uptime/downtime events.</td>
  </tr>
  <tr>
    <td>Backup/Recovery module</td>
    <td>Maintains redundant database replicas, performs rollback to last known good state, and synchronizes replicas after recovery.</td>
  </tr>
  <tr>
    <td>Availability Manager</td>
    <td>Coordinates failover and scaling actions when faults are detected.</td>
  </tr>
</table>

<h3>Step 6: Sketch views and record design decisions</h3>

<img width="1775" height="1293" alt="image" src="https://github.com/user-attachments/assets/c390432c-baa6-4dc3-9f1d-8eacfd130235" />

Refined Deployment Diagram


<img width="1847" height="1406" alt="image" src="https://github.com/user-attachments/assets/b7674332-dc11-4471-957f-b23e7adcd428" />

Sequence diagram of the user performing an operation. The user must log in, and the operation is securely stored.

           

<h3>Step 7: Perform analysis of current design and review iteration goal and design objectives</h3>
<table>
  <tr>
    <th>Not Addressed</th>
    <th>Partially Addressed</th>
    <th>Completely Addressed</th>
    <th>Design Decisions Made During Iteration</th>
  </tr>
  <tr>
    <td></td>
    <td>QA-1 Performance</td>
    <td></td>
    <td>Monitoring service collects performance metrics, enabling future query optimization.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>QA-2 Availability</td>
    <td>Monitoring service refined with ConditionMonitor and HealthMonitor modules. Backup/Recovery module supports replication, rollback, and state sync. Availability Manager coordinates failover.</td>
  </tr>
  <tr>
    <td>QA-3 Security</td>
    <td></td>
    <td></td>
    <td>Security tactics deferred to future iteration.</td>
  </tr>
  <tr>
    <td></td>
    <td>QA-4 Usability</td>
    <td></td>
    <td>Availability and recovery improvements reduce user disruption and improve reliability.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>CON-3 High Availability and Scalability</td>
    <td>Replication and load balancing support 5000 concurrent users.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>CON-5 Response ≤ 2s</td>
    <td>Latency metrics are collected.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>CON-6 Cloud-Native Deployment</td>
    <td>Auto-failover is defined in deployment.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>CRN-2 Scalability and Performance</td>
    <td>Monitoring supports performance tracking. Scalability addressed via CON-3.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>CRN-4 AI Accuracy and Adaptability</td>
    <td>Monitoring supports anomaly detection.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>CRN-5 Availability and Fault Tolerance</td>
    <td>Availability Manager + Backup/Recovery module ensures resilience and recovery.</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>UC-6 Manage system performance and operation</td>
    <td>Health metrics provided by Monitoring Service. Availability Manager ensures recovery. Backup/Recovery module supports continuous service for 5000+ users.</td>
  </tr>
</table>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<h2>ATAM Risk Assessment</h2>

<h4>Risks</h4>
<table>
  <tr>
    <th>ID</th>
    <th>Architectural Decision</th>
    <th>Explanation</th>
  </tr>
  <tr>
    <td>R1</td>
    <td>Continuous Monitoring Service</td>
    <td>If checks aren't frequent enough, failures may be missed.</td>
  </tr>
  <tr>
    <td>R2</td>
    <td>Backup/Recovery Module</td>
    <td>Recovery may take longer than acceptable if rollback involves too much data.</td>
  </tr>
  <tr>
    <td>R3</td>
    <td>Availability Manager</td>
    <td>Switching over during failover could cause a short service break.</td>
  </tr>
  <tr>
    <td>R4</td>
    <td>Cloud-native Deployment</td>
    <td>Replication at scale may cost more and add complexity.</td>
  </tr>
</table>

<h4>Sensitivities</h4>
<table>
  <tr>
    <th>ID</th>
    <th>Architectural Decision</th>
    <th>Explanation</th>
  </tr>
  <tr>
    <td>S1</td>
    <td>Continuous Monitoring Service</td>
    <td>Frequency of checking affects speed of failure detection.</td>
  </tr>
  <tr>
    <td>S2</td>
    <td>Backup/Recovery Module</td>
    <td>Recovery speed depends on rollback method chosen.</td>
  </tr>
  <tr>
    <td>S3</td>
    <td>Availability Manager</td>
    <td>Downtime depends on how fast failover is triggered.</td>
  </tr>
  <tr>
    <td>S4</td>
    <td>Cloud Deployment</td>
    <td>Availability depends on number and location of replicas.</td>
  </tr>
</table>

<h4>Tradeoffs</h4>
<table>
  <tr>
    <th>ID</th>
    <th>Architectural Decision</th>
    <th>Explanation</th>
  </tr>
  <tr>
    <td>T1</td>
    <td>Continuous Monitoring Service</td>
    <td>More checks allow faster detection but increase system load.</td>
  </tr>
  <tr>
    <td>T2</td>
    <td>Backup/Recovery Module</td>
    <td>Higher redundancy provides better uptime but increases cost.</td>
  </tr>
  <tr>
    <td>T3</td>
    <td>Availability Manager</td>
    <td>Faster failover decreases downtime but risks incomplete recovery.</td>
  </tr>
  <tr>
    <td>T4</td>
    <td>Cloud Deployment</td>
    <td>Higher scaling increases availability but makes data consistency harder.</td>
  </tr>
</table>


<h3>ATAM Table – Analyzing Scenario QA-2</h3>

<table>
  <tr>
    <th>Scenario</th>
    <td colspan="3">If there is any detected fault or system failure, AIDAP will back up and recover the data. The system should maintain an uptime of 99.5% per month.</td>
  </tr>
  <tr>
    <th>Attribute</th>
    <td colspan="3">Availability</td>
  </tr>
  <tr>
    <th>Stimulus</th>
    <td colspan="3">Failure or fault detected by the system.</td>
  </tr>
  <tr>
    <th>Environment</th>
    <td colspan="3">Normal operation</td>
  </tr>
  <tr>
    <th>Response</th>
    <td colspan="3">AIDAP will back up and recover the data.</td>
  </tr>
  <tr>
    <th>Architecture Decision</th>
    <th>Risk</th>
    <th>Sensitivity</th>
    <th>Tradeoff</th>
  </tr>
  <tr>
    <td>Continuous Monitoring Service</td>
    <td>R1</td>
    <td>S1</td>
    <td>T1</td>
  </tr>
  <tr>
    <td>Backup/Recovery Module</td>
    <td>R2</td>
    <td>S2</td>
    <td>T2</td>
  </tr>
  <tr>
    <td>Availability Manager</td>
    <td>R3</td>
    <td>S3</td>
    <td>T3</td>
  </tr>
  <tr>
    <td>Cloud Deployment</td>
    <td>R4</td>
    <td>S4</td>
    <td>T4</td>
  </tr>
</table>


<h3>Utility Tree</h3>

<img width="1558" height="893" alt="image" src="https://github.com/user-attachments/assets/3f1c69f6-d09a-4a80-be02-cdc155dbd9f3" />
