---
name: itinerary-to-json
description: Use when creating, converting, or exporting travel itineraries to structured JSON format. Triggers on requests like "save itinerary as JSON", "export to JSON", "create JSON itinerary", or when updating existing JSON itinerary files. Provides complete schema with accommodation, transport, activities, timing, booking details, and Google Maps integration.
---

# Itinerary to JSON Converter

Converts travel itineraries to structured JSON format with comprehensive schema for destinations, accommodation, transport, daily activities, timing constraints, booking requirements, and map integration.

---

## JSON Schema Structure

### Root Level
```json
{
  "destination": "string - City/region name",
  "country": "string - Country name",
  "dates": {
    "start": "YYYY-MM-DD",
    "end": "YYYY-MM-DD"
  },
  "accommodation": { /* see below */ },
  "transport": { /* see below */ },
  "days": [ /* array of day objects */ ],
  "maps": { /* optional map links */ }
}
```

### Accommodation Object
```json
{
  "name": "string - Accommodation name",
  "address": "string - Full address",
  "link": "string - Booking/website URL",
  "checkIn": "YYYY-MM-DD",
  "checkOut": "YYYY-MM-DD",
  "bookingReference": "string or null"
}
```

### Transport Object
Contains `arrival` and/or `departure` objects (null if not applicable):

```json
{
  "arrival": {
    "date": "YYYY-MM-DD",
    "time": "HH:MM (24h format) or null",
    "from": "string - Origin location",
    "to": "string - Destination location",
    "provider": "string - Transport company/service",
    "link": "string - Booking URL",
    "bookingReference": "string or null"
  },
  "departure": {
    /* same structure as arrival */
  }
}
```

### Day Object
```json
{
  "date": "YYYY-MM-DD",
  "isArrivalDay": boolean,
  "isDepartureDay": boolean,
  "timeBlocks": [ /* array of time block objects */ ]
}
```

### Time Block Object
```json
{
  "name": "string - Morning/Afternoon/Evening/Night",
  "timeRange": "string - HH:MM-HH:MM or descriptive",
  "activities": [ /* array of activity objects */ ]
}
```

### Activity Object (Core Schema)
```json
{
  "order": integer,
  "name": "string - Activity name",
  "link": "string - Google Maps search URL or null",
  "duration": integer - minutes or null,
  "suggestedTime": "string - HH:MM or null",
  "timeRestriction": "string - Opening hours/constraints or null",
  "priority": "string - mandatory/high/medium/low/optional",
  "priceRange": "string - €/€€/€€€ or null",
  "tags": ["array of emoji strings from itinerary-formatter skill"],
  "notes": "string - Tips/description or null",
  "bookingRequired": boolean,
  "bookingDetails": "string - Booking instructions or null"
}
```

---

## Activity Tags (Emoji System)

Must align with **itinerary-formatter skill**:

### Cost & Booking
- `🆓` Free
- `🎟️` Paid
- `📅` Reservation Required

### Visit Style
- `👀` See & Continue (quick stop)
- `⏳` Be There (immersive visit)

### Extra Markers
- `⭐` Top Highlight
- `📸` Photo Spot
- `☂️` Indoor/Rainy Day
- `🍽️` Food/Dining

---

## Priority Levels

- **mandatory**: Cannot skip (arrival, check-in, departure)
- **high**: Top recommendations, star attractions
- **medium**: Nice-to-have experiences
- **low**: Optional, time-permitting
- **optional**: Explicitly marked as optional by user

---

## Price Range System

- `€` - Budget (under €10)
- `€€` - Moderate (€10-25)
- `€€€` - Expensive (€25+)
- `null` - Free or not applicable

---

## Time Handling Rules

1. **Duration**: Always store in minutes if known
2. **Suggested Time**: Use 24h format (HH:MM)
3. **Time Restriction**: Store opening hours, last entry times, seasonal variations as free text
4. **Flexible Rearrangement**: The `order` field allows easy activity reordering without changing time blocks

---

## Maps Integration

Store two types of map links at root level:

```json
"maps": {
  "fullDayRoute": "https://www.google.com/maps/dir/Location1/Location2/.../Location1",
  "allLocationsSearch": "https://www.google.com/maps/search/Location1+OR+Location2+OR+..."
}
```

### Per-Activity Links
Each activity should have a direct Google Maps search link:
```
https://www.google.com/maps/search/[Activity+Name+Location]
```

---

## Workflow

1. **Gather Information**:
   - Destination details
   - Accommodation info and links
   - Transport arrival/departure details
   - Daily activities with order and timing

2. **Structure Activities**:
   - Organize by date → time blocks → activities
   - Assign order numbers sequentially
   - Add appropriate emoji tags
   - Include duration and suggested times
   - Set priority levels

3. **Add Metadata**:
   - Google Maps links per activity
   - Time restrictions (opening hours)
   - Booking requirements
   - Price ranges
   - Notes and tips

4. **Generate Maps**:
   - Create full-day route link
   - Create consolidated search link

5. **Write JSON File**:
   - Save to `[destination_lowercase]_itinerary.json`
   - Ensure proper JSON formatting
   - Validate structure

---

## File Naming Convention

`[destination]_itinerary.json`

Examples:
- `bruges_itinerary.json`
- `barcelona_itinerary.json`
- `paris_itinerary.json`

---

## Example Usage

When user says:
- "Save this itinerary as JSON"
- "Create a JSON file for this trip"
- "Export itinerary to JSON format"
- "Convert this to structured data"

Load this skill and follow the schema above to generate the JSON file.
