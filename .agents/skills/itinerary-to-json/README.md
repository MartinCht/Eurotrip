# Itinerary to JSON Skill

This skill provides structured JSON formatting for travel itineraries.

## Files

- **SKILL.md** - Complete skill documentation with schema, rules, and workflow
- **schema.json** - JSON Schema validation file for itinerary structure
- **example_bruges.json** - Reference example based on Bruges itinerary

## Usage

This skill is automatically loaded when:
- User requests JSON export of itinerary
- User wants structured travel data
- Converting between formats (Markdown/HTML to JSON)

## Schema Overview

The JSON structure includes:
- **Root**: Destination, dates, accommodation, transport
- **Days**: Daily breakdown with time blocks
- **Activities**: Ordered items with timing, tags, pricing, and booking info
- **Maps**: Route and location search links

## Key Features

✅ Flexible timing (duration + suggested time + restrictions)  
✅ Rearrangeable activities via order field  
✅ Emoji tag system aligned with itinerary-formatter  
✅ Price range tracking (€/€€/€€€)  
✅ Booking support with reference fields  
✅ Google Maps integration per activity
