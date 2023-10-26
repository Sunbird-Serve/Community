# Telemetry Events

### **Start** - This API is used to log telemetry when users initiate Volunteer Signup

**Serve** - **Use Case: Logging Telemetry for Volunteer Signup**

**Description**: Captures telemetry when a user initiates the process of signing up as a volunteer on the Serve platform.

**Request Arguments**:

* **config**: Configuration object containing user-related information.
* **contentId**: ID of the content (not directly relevant to this use case, but can be used to represent a unique identifier for the signup process).
* **contentVer**: Version of the content (defaulting to "1.0" as it's not critical for this use case).
* **data**:
  * **type**: "app" (as it's a fundamental app-related action).
  * **mode**: "preview" (indicating that the user is exploring the volunteer signup process).
  * **stageid**: A unique stage identifier representing the starting point of the signup process.

**Customization**:

* **User ID**: In the config object, can have the user's ID, representing the user initiating the volunteer signup. It's not explicitly mentioned in the data structure, but it's assumed to be part of the configuration.

**Explanation**:

In this use case, when a user begins the process of signing up as a volunteer on the Serve platform, the "Start" event is triggered and logged. This event is identified by its type "app," indicating a fundamental app-related action.

The "mode" is set to "preview" to signify that the user is in the initial stage of exploring the volunteer signup process.

The "stageid" represents a unique identifier for the starting point of the volunteer signup process. For example, it could be the ID of the landing page or the first step of the signup form.

By customizing the event with the relevant user ID and other user-specific details, can track and analyze the volunteer signup process, making it easier to gather insights and optimize the user experience on the Serve platform.



### **Impression** - This API is used to log telemetry when users visit a specific page.

**Serve** -  This API is used to log telemetry when the users explores the need.

\
**Use Case: Logging Telemetry for User Page Visit - Explore Need**

**Event Name**: "PageVisit"&#x20;

**Description**: Captures telemetry when a user explores need on the Serve platform.

**Request Arguments**:

* **data**: An object containing the following information:
  * **type**: Describes the type of the impression, such as "list," "detail," "view," "edit," "workflow," or "search."
  * **subtype**: (Optional) Can provide additional information related to the impression, such as "Paginate" or "Scroll."
  * **pageid**: Represents the unique ID of the page being visited.
  * **itype**: (Optional) Indicates the type of interaction that led to the page visit, which could be "SWIPE," "SCRUB," or "AUTO."
  * **stageto**: (Optional) Refers to the game level or stage associated with the page ID to which navigation was done.

**Customization**:

* **User ID**: Although not explicitly mentioned in the request arguments, you would typically associate the user's ID with this event to track which users are visiting which pages.

**Explanation**:

In this use case, the event is triggered when a user visits explore need page on the Serve platform. The event captures details about the type of impression (e.g., viewing a list of need type or exploring the need), any additional subtypes (e.g., scrolling through the list), the unique page ID, the type of interaction (e.g., swiping or auto-scrolling), and the stage associated with the visited page.

By customizing this event with the user's ID, user interactions can be tracked with different pages on the platform, gain insights into which pages are most frequently visited, and understand how users navigate through the platform. This data can be valuable for optimizing the user experience.

