# WeMush MCP Tool Reference

Complete reference for all 33 MCP tools available through the WeMush Research MCP Server.

## Research Project Tools

### list_research_projects

List available research projects.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `status` | No | Filter: "active", "completed", "draft" |
| `visibility` | No | Filter: "public", "private" |
| `limit` | No | Max results (default 20) |
| `offset` | No | Pagination offset |

**Returns:** Array of project summaries with ID, title, status, participant count.

---

### get_research_project

Get detailed information about a specific research project.

| Parameter   | Required | Description                                                       |
| ----------- | -------- | ----------------------------------------------------------------- |
| `projectId` | Yes      | The project ID                                                    |

**Returns:** Full project details including description, protocol, strains, enrollment status.

---

### enroll_in_project

Join a research project as a participant.

| Parameter   | Required | Description            |
| ----------- | -------- | ---------------------- |
| `projectId` | Yes      | The project ID to join |

**Returns:** Enrollment confirmation with participant ID.

---

### withdraw_from_project

Leave a research project.

| Parameter   | Required | Description             |
| ----------- | -------- | ----------------------- |
| `projectId` | Yes      | The project ID to leave |

**Returns:** Withdrawal confirmation.

---

### create_research_project

Create a new research project.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `title` | Yes | Project title |
| `description` | Yes | Detailed description |
| `targetStrainIds` | Yes | Array of strain IDs to study |
| `protocol` | Yes | Research protocol object |
| `visibility` | No | "public" or "private" |
| `startDate` | No | Project start date |
| `endDate` | No | Project end date |

**Returns:** Created project details with ID.

---

### publish_research_project

Make a draft project public and open for enrollment.

| Parameter   | Required | Description               |
| ----------- | -------- | ------------------------- |
| `projectId` | Yes      | The project ID to publish |

**Returns:** Updated project with published status.

---

## Observation Tools

### create_observation

Submit a new observation for a research project.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | Yes | The research project ID |
| `specimenId` | Yes | The specimen being observed |
| `observationType` | Yes | Type of observation |
| `data` | Yes | Observation data object |
| `notes` | No | Additional notes |
| `images` | No | Array of image URLs |

**Returns:** Created observation with ID.

---

### list_my_observations

List observations submitted by the current user.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | No | Filter by project |
| `specimenId` | No | Filter by specimen |
| `startDate` | No | Filter by date range start |
| `endDate` | No | Filter by date range end |
| `limit` | No | Max results |
| `offset` | No | Pagination offset |

**Returns:** Array of observation summaries.

---

### get_observation

Get detailed information about a specific observation.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `observationId` | Yes | The observation ID |

**Returns:** Full observation details including data, images, metadata.

---

### update_observation

Update an existing observation.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `observationId` | Yes | The observation ID |
| `data` | No | Updated observation data |
| `notes` | No | Updated notes |
| `images` | No | Updated images |

**Returns:** Updated observation.

---

### delete_observation

Delete an observation (soft delete).

| Parameter       | Required | Description         |
| --------------- | -------- | ------------------- |
| `observationId` | Yes      | The observation ID  |

**Returns:** Deletion confirmation.

---

## Specimen Tools

### list_my_specimens

List specimens accessible to the current user.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `status` | No | Filter: "active", "archived", "transferred" |
| `strainId` | No | Filter by strain |
| `organizationId` | No | Filter by organization |
| `limit` | No | Max results |
| `offset` | No | Pagination offset |

**Returns:** Array of specimen summaries.

---

### get_specimen_details

Get detailed information about a specific specimen.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `specimenId` | Yes | The specimen ID |

**Returns:** Full specimen details including strain, status, lineage info, observation count.

---

### get_specimen_lineage

Get the ancestry and descendants of a specimen.

| Parameter    | Required | Description                                   |
| ------------ | -------- | --------------------------------------------- |
| `specimenId` | Yes      | The specimen ID                               |
| `depth`      | No       | How many generations to traverse (default 3)  |

**Returns:** Lineage tree with parent/child relationships.

---

### record_specimen_observation

Record a cultivation observation for a specimen.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `specimenId` | Yes | The specimen ID |
| `observationType` | Yes | Type: "growth", "health", "environmental", "harvest" |
| `measurements` | No | Measurement data object |
| `conditions` | No | Environmental conditions |
| `healthStatus` | No | Health assessment |
| `notes` | No | Additional notes |
| `images` | No | Array of image URLs |

**Returns:** Created observation with ID.

---

## Analytics Tools

> **Note:** Analytics tools are protected by k-anonymity (k=5). Returns null if fewer than 5 participants.

### get_project_analytics

Get aggregate analytics for a research project.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | Yes | The project ID |

**Returns:** Analytics including participant count, observation rates, completion stats.

---

### get_outcome_breakdown

Get outcome statistics broken down by category.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | Yes | The project ID |
| `groupBy` | No | Group by: "strain", "technique", "substrate", "equipment" |

**Returns:** Outcome distributions with success/failure rates per category.

---

### get_equipment_analysis

Analyze equipment correlation with outcomes.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | Yes | The project ID |

**Returns:** Equipment usage statistics and outcome correlations.

---

### get_group_comparison

Compare outcomes between participant groups.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | Yes | The project ID |
| `groupField` | Yes | Field to group by |

**Returns:** Comparative statistics between groups.

---

### get_research_trends

Get trend data over time for a project.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `projectId` | Yes | The project ID |
| `metric` | Yes | Metric: "observations", "participants", "outcomes" |
| `interval` | No | Time interval: "day", "week", "month" |
| `startDate` | No | Trend start date |
| `endDate` | No | Trend end date |

**Returns:** Time series data for the specified metric.

---

## Catalog Tools

### search_strains

Search the mushroom strain catalog.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `query` | Yes | Search query |
| `speciesId` | No | Filter by species |
| `difficulty` | No | Filter: "beginner", "intermediate", "advanced" |
| `limit` | No | Max results |
| `offset` | No | Pagination offset |

**Returns:** Array of matching strains with basic info.

---

### search_species

Search the mushroom species catalog.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `query` | Yes | Search query |
| `genusId` | No | Filter by genus |
| `limit` | No | Max results |
| `offset` | No | Pagination offset |

**Returns:** Array of matching species with basic info.

---

### get_strain_details

Get detailed information about a specific strain.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `strainId` | Yes | The strain ID |

**Returns:** Full strain details including taxonomy, cultivation requirements, characteristics.

---

### get_species_details

Get detailed information about a specific species.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `speciesId` | Yes | The species ID |

**Returns:** Full species details including taxonomy, description, known strains.

---

## Profile Tools

### get_my_research_profile

Get the current user's research profile.

**Parameters:** None

**Returns:** Profile including research history, project memberships, contribution stats.

---

### get_research_activity_feed

Get recent activity across user's projects.

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `limit` | No | Max items (default 20) |
| `offset` | No | Pagination offset |

**Returns:** Array of recent activities (observations, enrollments, project updates).

---

## MCP Prompts

The WeMush MCP server provides these prompts:

| Prompt | Description |
| ------ | ----------- |
| `research_guidance` | Get personalized research recommendations based on experience level |
| `strain_recommendation` | Get strain suggestions based on goals and skill level |
| `troubleshooting_help` | Diagnose cultivation issues from symptoms |
| `observation_template` | Generate observation templates for consistent data collection |
| `analytics_interpretation` | Help interpret research analytics and statistics |

---

## MCP Resources

Available data resources:

| Resource | URI | Description |
| -------- | --- | ----------- |
| `research_protocol_templates` | `wemush://protocols` | Standard research protocol templates |
| `cultivation_best_practices` | `wemush://best-practices` | Community-vetted cultivation guides |
| `mycology_glossary` | `wemush://glossary` | Mycology terminology definitions |

---

## Error Codes

| Code | Meaning |
| ---- | ------- |
| `AUTH_REQUIRED` | OAuth token missing or expired |
| `INSUFFICIENT_SCOPE` | Token lacks required scope |
| `NOT_FOUND` | Resource not found |
| `FORBIDDEN` | User lacks permission |
| `K_ANONYMITY_THRESHOLD` | Not enough data for privacy-safe analytics |
| `VALIDATION_ERROR` | Invalid input parameters |
| `RATE_LIMITED` | Too many requests |
