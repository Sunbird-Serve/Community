# Configuration for Various Use Case

* **Need Type:** Defines the type of the need being fulfilled (e.g., **Online Teaching** or **Disaster Relief Support**).
* **Volunteer Skills:** Determines the required capabilities of volunteers.
* **Taxonomy:** Defines how tasks or content are categorized.
* **Input Parameters:** Custom fields needed for each scenario.

***

### **Use Case 1: Online Teaching (Education Sector)**

**Scenario:** A state government wants to connect volunteers with rural students for **live online classes**.

#### **Step 1: Configuring "Need Type" for Online Teaching**

Modify `needType.json`:

```json
jsonCopyEdit{
  "needType": "ONLINE TEACHING",
  "description": "Conduct live teaching sessions for students in rural schools"
}
```

***

#### **Step 2: Defining Volunteer Skills**

Modify `volunteerSkills.json`:

```json
jsonCopyEdit{
  "needType": "ONLINE TEACHING",
  "skills": ["Mathematics", "Science", "English", "Coding"],
  "experienceLevel": ["Beginner", "Intermediate", "Expert"]
}
```

***

#### **Step 3: Configuring Taxonomy for Educational Content**

Modify `taxonomy.json`:

```json
jsonCopyEdit{
  "needType": "ONLINE TEACHING",
  "taxonomy": {
    "grade": ["1st", "2nd", "3rd", "4th"],
    "subjects": ["Mathematics", "Science", "English"],
    "medium": ["English", "Hindi", "Kannada"]
  }
}
```

***

#### **Step 4: Defining Input Parameters for Session Configuration**

Modify `inputParameters.json`:

```json
jsonCopyEdit{
  "needType": "ONLINE TEACHING",
  "parameters": [
    { "name": "sessionMode", "type": "dropdown", "values": ["Zoom", "Google Meet"] },
    { "name": "sessionDuration", "type": "number", "unit": "minutes" },
    { "name": "preferredTimings", "type": "timeslot", "format": "HH:mm - HH:mm" },
    { "name": "languagePreference", "type": "dropdown", "values": ["English", "Hindi", "Kannada"] }
  ]
}
```

✅ **Outcome:**

* **Volunteer profiles** filter by subjects.
* **Session preferences** (Zoom, time slots) are stored dynamically.

***

### **Use Case 2: Disaster Relief Support (Non-Education Sector)**

**Scenario:** An NGO wants to manage **disaster relief volunteers** and assign them to affected areas.

#### **Step 1: Configuring "Need Type" for Disaster Relief**

Modify `needType.json`:

```json
jsonCopyEdit{
  "needType": "DISASTER_RELIEF",
  "description": "Assign volunteers to provide relief during floods, earthquakes, etc."
}
```

***

#### **Step 2: Defining Volunteer Skills**

Modify `volunteerSkills.json`:

```json
jsonCopyEdit{
  "needType": "DISASTER_RELIEF",
  "skills": ["First Aid", "Food Distribution", "Rescue Operations", "Logistics"],
  "experienceLevel": ["Beginner", "Trained", "Expert"]
}
```

***

#### **Step 3: Configuring Taxonomy for Relief Efforts**

Modify `taxonomy.json`:

```json
jsonCopyEdit{
  "needType": "DISASTER_RELIEF",
  "taxonomy": {
    "disasterType": ["Flood", "Earthquake", "Cyclone"],
    "reliefType": ["Medical", "Food", "Shelter"],
    "urgencyLevel": ["High", "Medium", "Low"]
  }
}
```

***

#### **Step 4: Defining Input Parameters for Disaster Response**

Modify `inputParameters.json`:

```json
jsonCopyEdit{
  "needType": "DISASTER_RELIEF",
  "parameters": [
    { "name": "location", "type": "text" },
    { "name": "requiredVolunteers", "type": "number" },
    { "name": "reliefCategory", "type": "dropdown", "values": ["Medical", "Food", "Shelter"] },
    { "name": "equipmentNeeded", "type": "multi-select", "values": ["First Aid Kit", "Blankets", "Food Packets"] }
  ]
}
```

✅ **Outcome:**

* **Volunteers register with skills** (First Aid, Rescue, etc.).
* **Disaster sites are categorized** (Flood, Medical Relief).

### **Use Case 3: In-Kind Donation (Non-Education Sector)**

**Scenario:** A charitable organization wants to manage **donations of goods (books, food, clothes, medical kits, etc.)** and match them with beneficiaries (schools, disaster-hit areas, orphanages).

***

#### **Step 1: Configuring "Need Type" for In-Kind Donations**

Modify `needType.json`:

```json
jsonCopyEdit{
  "needType": "IN_KIND_DONATION",
  "description": "Facilitate donation of goods such as books, clothes, food, and medical supplies."
}
```

***

#### **Step 2: Defining Volunteer Skills**

Modify `volunteerSkills.json`:

```json
jsonCopyEdit{
  "needType": "IN_KIND_DONATION",
  "skills": ["Logistics Coordination", "Inventory Management", "Community Outreach"],
  "experienceLevel": ["Beginner", "Experienced", "Expert"]
}
```

***

#### **Step 3: Configuring Taxonomy for Donation Items**

Modify `taxonomy.json`:

```json
jsonCopyEdit{
  "needType": "IN_KIND_DONATION",
  "taxonomy": {
    "donationCategory": ["Books", "Clothes", "Food", "Medical Supplies"],
    "urgencyLevel": ["Immediate", "Within a Week", "Ongoing"],
    "intendedBeneficiary": ["Schools", "Orphanages", "Disaster Relief Camps"]
  }
}
```

***

#### **Step 4: Defining Input Parameters for Donation Matching**

Modify `inputParameters.json`:

```json
jsonCopyEdit{
  "needType": "IN_KIND_DONATION",
  "parameters": [
    { "name": "donorName", "type": "text" },
    { "name": "donationType", "type": "dropdown", "values": ["Books", "Clothes", "Food", "Medical Supplies"] },
    { "name": "quantity", "type": "number", "unit": "units" },
    { "name": "pickupLocation", "type": "text" },
    { "name": "dropoffLocation", "type": "text" },
    { "name": "expectedDeliveryDate", "type": "date" }
  ]
}
```



***

### **Final Comparison of All Three Use Cases**

| Feature              | Online Teaching        | Disaster Relief               | In-Kind Donation                |
| -------------------- | ---------------------- | ----------------------------- | ------------------------------- |
| **Need Type**        | ONLINE\_TEACHING       | DISASTER\_RELIEF              | IN\_KIND\_DONATION              |
| **Volunteer Skills** | Math, Science, Coding  | First Aid, Logistics          | Logistics, Inventory Management |
| **Taxonomy**         | Grade, Subject, Medium | Disaster Type, Urgency        | Donation Type, Beneficiary      |
| **Input Parameters** | Session Mode, Duration | Location, Required Volunteers | Donor Details, Pickup & Dropoff |
