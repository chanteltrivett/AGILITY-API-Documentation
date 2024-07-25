## AGILITY Release Notes

## Iteration 66

### What’s New

*   AGILITY’s new **Flow Extractions** tab allows you to accelerate protocol-level issue isolation. The Flow Extractions tab supports all of the existing network services in AGILITY, including:
*   _Voice and Video over LTE_ \*
*   Voice and Video over New radio
*   4G & 5G NSA connectivity\*
*   5G SA Connectivity\*
*   5G SA Mobility (EPSfallback)
*   5G SA Data (might delete)
*   Special Services - e911
*   The **Per Protocol Level Analysis** tab was added to the Call Flow Details page to allow users to view a summary of the selected call flow. It provides a bird' s-eye view of every protocol within the selected flow, making it an excellent starting point for quick, low-effort analyses that provide significant actionable insights.
*   The Analyzed Call Flows list was made collapsable to improve user viability of the Call Flow Details page.
*   A user feedback survey was added to AGILITY to gather insights for continuous product optimization.

  

### Bug Fixes

*   The expandable **Elements Detailed Information** panel now contains Message Attributes.
*   Labels were created to help users easily identify when newly uploaded files (PCAPs uploaded for analysis) have failed to process.
*   Sample files for mock predictions were restored.
*   Comprehensive Service Coverage was enabled to support troubleshooting across services, including:
*   Support for 5G SA Connectivity Service\*
*   Support for 4G & 5G NSA Connectivity \*
*   Support for VONR
*   Support for Special Services E911
*   Support for 5G SA Mobility EPSFallback
*   Support for 5G SA Data (if available)
*   Internal sign-up options were removed from the sign-up flow for increased usability.
*   The expandable Element’s Detailed Information panel was added to the Sequence Diagram to display network elements' Descriptions and Details.

  

## Iteration 67

### What’s New

*   Reintroduction of Legacy features on the new UI, including:
*   The ability to select specific results to explore them in depth.
*   Tallys of the total number of call flows, the total number of network elements, the total number of protocols, and the total number of procedures.
*   The **Call Flow Details** card displays the Start Date and Time, Duration, IMSI, MSISDN, Device Type, B Number, Call Lag, and Header Size.
*   The Results tab includes Protocol Level Analysis, Flow Extractions, Call Flow (multi-view), and KPI Analysis.
*   Call Flow Details can be expanded and collapsed, allowing users to zone in on Call Flow diagrams (the Sequence Diagram & Topology Diagram), ProtocolLevel Analysis, Flow Extractons, and Diagnostics.
*     
    

### Bug Fixes

*   Resolved unresponsiveness on the Per Protocol Evaluation level for 5G SA connectivity.
*   Resolved the unintuitive scrolling direction encountered on the Play feature for the Call Flow visualization tab.
*   Ensured compatibility with .cap file uploads on AGILITY.
*   Restored labeling functionality to Failed call flows that were missing labels.
*   Remedied Topology Diagram views wherein the Network functions per domain were misrepresented.

  

## Iteration 68

### What’s New

*   AGILITY’s new High-Level Summary page allows you to identify analyses with the highest failure rates at the outset of the troubleshooting process. (Individual subscribers are classified by Impacted International Subscriber Identity (IMSI number).
*   Track, visualize & analyze subscriber-specific activity for network troubleshooting & optimization.
*   Improved fonts for increased readability.

  

### Bug Fixes

*   User access to partially completed ML analysis sessions has been blocked to prevent user-end confusion. Partially completed analyses will remain “In Progress” while the backend retries the prediction multiple times before determining that the analysis has failed.

  

## Iteration 69

### What’s New

*   **Isolate Root Casues with Diagnostics:** Users can now view the root causes for network errors; AGILITY’s new Diagnostics tab uses deep root cause analysis to expose the root causes for network errors.
*   Enhanced readability of Protocol Level Analysis HTTP2 sublabels.
*   Added HTTP2 Details to Callflow Visualizer and Flow Extractions. On the Sequence Diagram, users can filter by HTTP2 if the protocol is http2 or SIP. On the Call Flow Details page, under the Flow Extractions tab, users can select a sequence and then select the message’s Attributes button to view metadata for the selected frame number.

  

### What We’re Doing Behind the Scenes

*   **Monitoring and Observability:** We’ve created a dashboard with stats that monitor our tool's performance, including:
*   average time spent parsing each chunk of call flows,
*   average time spent preparing analytics
*   **Test automation:** We enhanced test automation by adding 19 new automated tests covering Auto Detection, 5G Mobility service, and High-Level Summary.
*   Added VONR Call detection based on HTTP2, VoLTE to our ML model library.
*   Created a VS Code SME Tool kit to help troubleshoot offsite
*   Set up end-to-end (E2E) test automation for sequence and topology diagrams.

  

### Bug Fixes

*   Resolved an issue wherein AGILITY’s backend service accepted null and undefined user IDs.
*   Remedied inaccurate depictions of connections between disconnected network elements on the Topology diagram (Such as connections between User Equipment and the Mobility Management Entity.

  

## Iteration 70

### What’s New

*   **View Colleagues' Analyses:** We’ve increased knowledge sharing and transparency by adding the “Others' Analyses” tab to the My Analyses page. The “Others' Analyses” tab allows users to access analyses conducted by other team members.
*   **Email Notifications for Analysis Results:** We’re creating a User Settings page to facilitate Email Notification configuration. From the User Settings page, users will be able to:
*   Create and modify email notification lists for analysis result dissemination
*   Set their own email notification receipt preferences.
*   **Easily Identify Call Flows with Network Errors:** On the My Analyses list, we’ve added red exclamation point error icons beside Call Flows containing network errors so that users can fast-track troubleshooting by sporting network issues quickly. We’ve also added Yellow exclamation point error icons.
*   **Filter by Message:** On the sequence Diagram, users can use the Messages filter to refine the results depicted on the diagram.
*   **Comprehensive Protocol Level Analysis:** On the Call Flow Details page, under the Protocol Level Analysis tab, we’ve exposed more protocol attributes. Initially, the Protocol Level Analysis tab exposed SIP & HTTP2 protocols. Now, the feature also exposes PFCP, GTPV, S1AP\_NAS, and more.
*   **Service Auto Detection Update**: We’ve added a popup on our new Service Auto Detection Feature to inform users that occasional processing errors may occur as we continue to improve the feature’s performance.
*   **Unification of our Service Models on AGILITY:** We’ve migrated all of our Service Models from the Legacy edition of AGILITY to the New AGILITY.

  

### What We’re Doing Behind the Scenes

*   To ensure accuracy, additional validation was added for AGILITY’s Topology and Sequence diagrams. 
*   **AGILITY Registry:**  We’ve created a repository with a Python script that allows all agility applications to be in one central authority. 
*   **Service Auto-Detection Beta Warning:** To improve the accuracy of our Service Auto-Detection feature, we set up a registry for cross-referencing.

  

### Bug Fixes

*   We resolved a glitch where uploads of VoNR PCAPs were producing duplicate network element depictions on the Sequence Diagram.  

  

## Iteration 71

### What’s New

*   **Multi-File Processing:** AGILITY now allows users to process multiple files uploaded in a zip in a single analysis.
*   **Multi-File Processing Email Notifications:** We’ve set up new email notifications that complement multi-file processing. Users who process (a) network analysis/analyses receive a notification email summarizing the analysis/analyses run. The email notification also lists files where call flows weren’t detected, prompting users to take remedial action when necessary.
*   **User Feedback on Predictions:** For continuous ML Model improvement, users can now provide feedback concerning the accuracy of call flow analysis results. Feedback icons are located on the Call Flow Details screen, where users can select thumbs up to agree with the analysis result or thumbs down to disagree.
*   **Display Analysis Results for Partially Analyzed Call Flows:** Now, AGILITY displays partial results for incomplete analyses. This means that data will still be available for review when a file is stuck in the processing status.
*     
    

### What We’re Doing Behind the Scenes

*   **Expanded Coverage to all Services:** Coverage now includes the following Service types;
*   4g-5g-NSA
*   5g-SA
*   5g-Mobility
*   VoNR
*   VoNR
*   **Improved Execution Time:** We migrated our test suit framework to Playwright to improve execution time:
*   4g-5g-NSA
*   5g-SA
*   5g-Mobility
*   VoNR-Cisco​
*   VoNR-Dish​

  

### Bug Fixes

*   **Functional Prediction Failure Procedures:**
*   Previously:
*    Analysis reports were systematically discarded when a prediction failed
*   Now:
*   Reports are downloaded for any analysis/analyses that encounter prediction failures.
*   AGILITY depicts the call flows within the files uploaded for any analysis/analyses.
*   On the Call Flow Details page, we rectified duplicate messages appearing on the Message filter drop-down located on the Call Flow Details page.