# Technical Sequence

Raise Need, Create Need Details, Fetch Need and Fetch Need Type

<figure><img src="../../../.gitbook/assets/Serve V1 - Sprint 1-Tech Sequence.drawio (8).png" alt=""><figcaption></figcaption></figure>

Need Plan and Need Deliverable Generation



<figure><img src="../../../.gitbook/assets/Serve V1 - Sprint 1-Need Plan &#x26; Deliverable - Tech Sequence.drawio.png" alt=""><figcaption></figcaption></figure>

Need Plan and Deliverable Flow is as follows:&#x20;

1. **Need Plan Generation**:
   * System generates Need Plan once a nomination has been approved by the nCoordinator.
   * The plan's details, including the plan's name, need ID, assigned user ID, status, and occurrence details (frequency, start date, end date, time slot, days) would all be fetched from Need and Nomination schema
2. **Generating Need Deliverables**:
   * As part of the "Need Plan" creation process, automatically generate one or more "Need Deliverables" using the "Need Deliverable" schema.
   * Each "Need Deliverable" references the `needPlanId` of the associated "Need Plan."
   * Set properties for each deliverable, such as deliverable type, session number, status, and comments. Session Number gets calculated based on the frequency and start and end date. Status will be Not Started Initially and nCoordinator will be able to update the status, finally deliverable type would be passed through the api request header when need plan is generated.&#x20;
3. **Managing Deliverables within Need Plan**:
   * Within each "Need Plan," manage the list of generated "Need Deliverables," tracking their progress and status changes.
   * Keep the association between "Need Deliverables" and their parent "Need Plan."
4. **Progressing Need Deliverables**:
   * Progress the status of "Need Deliverables" from "Not Started" to "Scheduled," "In Progress," "Completed," or "Cancelled" based on their fulfillment status.
5. **Recording Detailed Deliverable Information**:
   * For each "Need Deliverable," create a corresponding "Deliverables" entry using the "Deliverables" schema.
   * Reference the `needDeliverableId` of the associated "Need Deliverable."
   * Provide additional details about the deliverable, such as its status, deliverable type, comments, and detailed information from the "DeliverableDetails" schema.
6. **Capturing Deliverable Details**:
   * Use the "DeliverableDetails" schema to capture input parameters, output details, and outcomes for each "Deliverables" entry.
   * Record information like delivery dates, start and end times, due dates, priority, URLs, and remarks.
7. **Updating Deliverables and Plan**:
   * Update the status, details, and other properties of both "Need Deliverables" and "Deliverables" as needed.
   * Maintain the linkage between "Deliverables" and "Need Deliverables" through their respective identifiers.
8. **System Field Tracking**:
   * Use system fields (`osCreatedAt`, `osUpdatedAt`, `osCreatedBy`, `osUpdatedBy`) in all schemas to track creation, updates, and creators/updaters.

\
