# Eurotrip Orchestrator Skill

**Triggers:** Project management, task delegation, multi-agent coordination for Eurotrip 2026 planning

**Use when:**
- User asks to plan/create/update multiple destinations
- User wants to coordinate work across development and itinerary planning
- User needs to delegate tasks to specialized agents
- User wants to manage the overall Eurotrip project workflow

---

## Overview

This skill orchestrates the Eurotrip 2026 planning project by delegating work to specialized agents:

1. **Dev Agent** - Handles styles, HTML/CSS, framework rules, home page updates
2. **Itinerary Agent** - Creates destination itineraries following the trip-itinerary-generator skill

---

## Workflow

### Step 1: Understand the Request

Determine what type of work is needed:

**Development Tasks:**
- Style/CSS updates
- HTML generation or fixes
- Framework modifications
- Home page (index.html) updates
- Timeline or UI components
- Bug fixes in visual elements

**Itinerary Planning Tasks:**
- New destination itineraries
- Updating existing itineraries
- JSON structure validation
- Food recommendations
- Activity planning
- Budget calculations

**Hybrid Tasks:**
- Complete destination setup (itinerary + HTML generation)
- Multi-city planning that requires both agents

### Step 2: Delegate to Appropriate Agent(s)

#### For Development Tasks → Launch Dev Agent

**Agent Type:** `general`

**Prompt Template:**
```
You are the Eurotrip Dev Agent. Your role is to handle all development, styling, and framework tasks.

**Current Task:** [describe the task]

**Context:**
- Project root: C:\Users\marti\Documents\Personal\Eurotrip
- Framework: Custom Eurotrip 2026 Planning Framework
- Files you may need to modify:
  - index.html (home page with timeline)
  - [city]/[city]_itinerary.html (destination HTML pages)
  - .agents/FOR_AGENTS.md (framework rules)
  - README.md (project documentation)

**Framework Style Guidelines:**
- Barcelona: Terracotta orange (#c25e00)
- Paris: Royal blue (#2c5aa0)
- Bruges: Medieval gold (#d4af37)
- Amsterdam: Vibrant orange (#ff6b35)
- Berlin: Bold red (#e63946)
- Prague: Czech blue (#457b9d)
- Vienna: Imperial burgundy (#8b1538)
- Italy: Mediterranean green (#06a77d)
- Madrid: Spanish gold (#ffbe0b)

**Requirements:**
- Use 24-hour time format
- Mobile-responsive design
- Smooth transitions and hover effects
- Consistent with existing itinerary HTML files

**Deliverables:**
[Specify what should be delivered]

Follow the framework standards and ensure consistency with existing work.
```

#### For Itinerary Planning → Launch Itinerary Agent

**Agent Type:** `general`

**Prompt Template:**
```
You are the Eurotrip Itinerary Planning Agent. Your role is to create complete destination itineraries following the trip-itinerary-generator skill.

**Current Task:** Create itinerary for [CITY]

**Destination Details:**
- City: [CITY NAME]
- Country: [COUNTRY]
- Arrival Date: [YYYY-MM-DD]
- Departure Date: [YYYY-MM-DD]
- Previous City: [CITY]
- Next City: [CITY]
- Accommodation: [NAME & ADDRESS or "TBD - please research"]

**Framework:**
Read and follow `.agents/FOR_AGENTS.md` for complete instructions.

**Required Skills:**
Load the following skills:
1. trip-itinerary-generator (for creating structured itineraries)
2. itinerary-to-json (for JSON export)
3. itinerary-formatter (for emoji tags and formatting)

**Process:**
1. Confirm dates with the user
2. Research the destination
3. Create day-by-day itinerary with activities
4. Add food recommendations (dual-language)
5. Include logistics (transport, emergencies, tips)
6. Generate JSON following the schema
7. Validate against destination-data-schema.json
8. Report back with summary and any alternatives considered

**Deliverables:**
- [city]/[city]_itinerary.json (complete JSON file)
- Summary of what was created
- Budget estimate
- Any recommendations or alternatives

Start by confirming the dates, then proceed with research and itinerary creation.
```

#### For Hybrid Tasks → Launch Both Agents in Parallel

Use multiple Task tool calls in a single message to launch both agents simultaneously.

**Example:**
```
Task 1 (Itinerary Agent): Create Paris itinerary JSON
Task 2 (Dev Agent): Generate Paris HTML once JSON is ready
```

### Step 3: Coordinate and Integrate

After agents complete their work:

1. **Verify completeness** - Check that all deliverables were produced
2. **Validate consistency** - Ensure JSON and HTML match
3. **Update home page** - Add new destination to index.html timeline
4. **Update README** - Mark destination as complete
5. **Report to user** - Provide summary and next steps

---

## Task Categories

### Development Tasks (→ Dev Agent)

- Fix timeline hover bugs
- Update color schemes
- Create new UI components
- Modify home page layout
- Fix responsive design issues
- Update navigation
- Generate HTML from JSON
- CSS debugging
- Framework documentation updates

### Itinerary Tasks (→ Itinerary Agent)

- Plan new destination itinerary
- Research activities and attractions
- Create food recommendations
- Calculate budgets
- Find accommodation options
- Plan transport connections
- Generate daily schedules
- Create Google Maps routes
- Validate JSON structure

### Coordination Tasks (→ Orchestrator)

- Plan multiple cities at once
- Update project status across files
- Coordinate between dev and itinerary work
- Manage timeline and milestones
- Track completion status
- Prioritize upcoming work

---

## Communication Templates

### Acknowledging Request

"I'll orchestrate this work by delegating to specialized agents:

**[Task Type] Tasks:**
- [List specific tasks]
- Agent: [Dev/Itinerary]

**[Task Type] Tasks:**
- [List specific tasks]
- Agent: [Dev/Itinerary]

Launching agents now..."

### Reporting Completion

"All work completed successfully!

**Dev Agent Results:**
- [Summary of dev work]
- Files modified: [list]

**Itinerary Agent Results:**
- [Summary of itinerary work]
- Files created: [list]

**Project Status Update:**
- Total destinations complete: X/9
- Next recommended: [destination]

[Any recommendations or next steps]"

---

## Example Scenarios

### Scenario 1: "Plan Amsterdam itinerary"

**Orchestrator Action:**
→ Launch Itinerary Agent with Amsterdam details
→ Once complete, suggest Dev Agent can generate HTML

### Scenario 2: "Fix the timeline and add Amsterdam"

**Orchestrator Action:**
→ Launch Dev Agent for timeline fix
→ Launch Itinerary Agent for Amsterdam planning (if dates provided)
→ Coordinate: Dev Agent updates index.html after itinerary is ready

### Scenario 3: "Create complete setup for Berlin, Prague, and Vienna"

**Orchestrator Action:**
→ Launch 3 Itinerary Agents in parallel (if dates provided)
→ After completion, launch Dev Agent to:
  - Generate 3 HTML files
  - Update index.html timeline
  - Update README status

### Scenario 4: "Update the home page with new colors"

**Orchestrator Action:**
→ Launch Dev Agent only (pure development task)

---

## Project Structure Reference

```
Eurotrip/
├── index.html                          # Home page with timeline
├── README.md                           # Project documentation
├── .agents/
│   ├── FOR_AGENTS.md                  # Framework instructions
│   ├── destination-template.json      # JSON template
│   └── destination-data-schema.json   # Schema validation
├── 1-Barcelona/
│   ├── barcelona_itinerary.json       # ✅ Complete
│   └── barcelona_itinerary.html       # ✅ Complete
├── 2-Paris/
│   ├── paris_itinerary.json           # ✅ Complete
│   └── paris_itinerary.html           # ✅ Complete
├── 3-Brujas/
│   ├── bruges_itinerary.json          # ✅ Complete
│   └── bruges_itinerary.html          # ✅ Complete
└── [Future cities...]                  # ⏳ Planning
```

---

## Current Project Status

**Completed Destinations:** 3/9
- Barcelona (Oct 14-17) ✅
- Paris (Oct 17-21) ✅
- Bruges (Oct 21-22) ✅

**Next Up:** Amsterdam (Oct 22+)

**Trip Duration:** Oct 14 - Nov 12, 2026 (30 days)
**Return Flight:** Madrid → Buenos Aires (Nov 12)

---

## Agent Selection Rules

| Task Type | Agent | Reason |
|-----------|-------|--------|
| HTML/CSS/Styles | Dev | Visual and code work |
| Itinerary creation | Itinerary | Research and planning |
| JSON generation | Itinerary | Data structure |
| Home page updates | Dev | HTML modification |
| Framework rules | Dev | Documentation |
| Activity research | Itinerary | Content creation |
| Bug fixes | Dev | Technical issues |
| Multi-city planning | Both (parallel) | Combine work |
| Food recommendations | Itinerary | Content research |
| Timeline component | Dev | UI development |

---

## Success Criteria

After delegating work, verify:

- [ ] All requested files created/modified
- [ ] JSON validates against schema (if applicable)
- [ ] HTML renders correctly (if applicable)
- [ ] Home page updated with new destinations
- [ ] README status reflects changes
- [ ] Consistent styling across pages
- [ ] No broken links
- [ ] Mobile-responsive
- [ ] Budget calculations included (itinerary)
- [ ] Emoji tags applied correctly (itinerary)

---

## Tips for Effective Orchestration

1. **Be specific** - Provide exact dates, city names, and requirements
2. **Parallel when possible** - Launch independent agents together
3. **Sequential when dependent** - Wait for itinerary before HTML generation
4. **Clear handoffs** - Tell each agent what the other will do
5. **Validate results** - Check that agents followed framework rules
6. **Update status** - Keep home page and README current
7. **Document decisions** - Track what was done and why

---

## Next Steps Recommendations

Based on current status, suggest to user:

1. **Plan Amsterdam next** (immediate next destination after Bruges)
2. **Batch plan similar cities** (Berlin + Prague together)
3. **Decide Italy cities** (Rome? Venice? Florence? Milan?)
4. **Set remaining dates** (Need dates for Amsterdam through Madrid)
5. **Book transport** (6 connections still TBD)

---

**Remember:** This orchestrator doesn't do the work itself - it delegates to specialized agents and coordinates their efforts. Always be clear about which agent is handling which task.