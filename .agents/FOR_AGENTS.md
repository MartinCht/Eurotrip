# Eurotrip Agent Guide

> **For agents** creating destination itineraries

---

## ⚠️ CRITICAL: Start Here

Before doing anything else:

1. **Ask the user for exact dates**:
   - "What is the arrival date at [destination]?" (format: YYYY-MM-DD)
   - "What is the departure date from [destination]?" (format: YYYY-MM-DD)

2. **You CANNOT proceed without confirmed dates.**

3. **Once confirmed**, follow this guide to create the itinerary.

---

## 📋 Your Task

Create a complete destination itinerary JSON file following the Eurotrip framework.

### What You'll Produce

A JSON file: `[CityName]/[cityname]_itinerary.json`

Example: `Paris/paris_itinerary.json`

### Structure Reference

Copy `.agents/destination-template.json` as your starting point.

Validate against `.agents/destination-data-schema.json` for structure.

Look at `Barcelona/barcelona_itinerary.json` as a complete example.

---

## 🚀 Step-by-Step Process

### Step 1: Confirm Dates ⚠️ MANDATORY

Ask the user:
- Arrival date (YYYY-MM-DD)
- Departure date (YYYY-MM-DD)

**Example:**
> "I'll create a Paris itinerary. Confirming dates: arrival October 17, 2026 and departure October 21, 2026. Is that correct?"

### Step 2: Gather Core Information

Confirm or ask about:
- [ ] Destination name and country
- [ ] Previous city (for arrival transport context)
- [ ] Next city (for departure transport planning)
- [ ] Accommodation (name, address, meals included)
- [ ] Special interests or requirements

### Step 3: Create Folder and File

```bash
mkdir [CityName]/
cp .agents/destination-template.json [CityName]/[cityname]_itinerary.json
```

### Step 4: Fill in Metadata

```json
{
  "destination": "Paris",
  "country": "France",
  "dates": {
    "start": "2026-10-17",
    "end": "2026-10-21"
  },
  "accommodation": { ... },
  "transport": {
    "arrival": { ... },
    "departure": { ... }
  }
}
```

**Key points:**
- `dates` is REQUIRED
- `transport.arrival` = coming FROM previous city
- `transport.departure` = going TO next city
- Store transport info in BOTH cities' JSON files

### Step 5: Research and Plan Days

For each day of the stay:

1. **Use the actual calendar date**: `"date": "2026-10-17"`
2. **Mark arrival/departure days**: `"isArrivalDay": true`
3. **Organize into time blocks**:
   - `morning` (typically 08:00-13:00)
   - `lunch` (typically 13:00-15:00)
   - `afternoon` (typically 15:00-18:30)
   - `evening` (typically 18:30-21:00)
   - `night` (optional, 21:00+)

### Step 6: Add Activities

**One entry per activity/place** - don't batch them!

❌ Bad: `{ "name": "Morning in Montmartre" }`

✅ Good:
```json
[
  { "name": "Sacré-Cœur Basilica", "duration": 45, ... },
  { "name": "Place du Tertre", "duration": 30, ... },
  { "name": "Café des Deux Moulins", "duration": 60, ... }
]
```

**Required fields for each activity:**
```json
{
  "order": 1,
  "name": "Sacré-Cœur Basilica",
  "link": "https://www.google.com/maps/search/Sacré-Cœur+Basilica+Paris",
  "duration": 45,
  "suggestedTime": "09:00",
  "timeRestriction": "Open 06:00-22:30 daily",
  "priority": "high",
  "tags": ["🆓", "⏳", "⭐", "☂️"],
  "type": "religious site",
  "notes": "Climb the dome for panoramic views (extra fee)",
  "bookingRequired": false,
  "optional": false
}
```

**Optional but valuable fields:**
- `priceRange`: "€", "€€", or "€€€"
- `cost`: Specific price "15 EUR"
- `opening_hours`: Detailed schedule
- `bookingDetails`: URL and advance time needed
- `secondaryPlaces`: Nearby spots within same activity

### Step 7: Create Google Maps Links

For each day, create a round-trip route:

```
https://www.google.com/maps/dir/
  [Accommodation]/
  [Place1]/
  [Place2]/
  [Place3]/
  [Accommodation]
```

Store in: `days[n].map_url`

### Step 8: Add Food Recommendations

**Critical: Dual-language names**

```json
{
  "name_local": "Coq au vin",
  "name_english": "Chicken braised in wine",
  "description": "Classic Burgundy dish...",
  "typical_cost": "18-25 EUR",
  "meal_type": "main"
}
```

Include:
- `must_try_dishes[]` - Local specialties
- `drinks_and_rituals[]` - Regional drinks and customs
- `restaurants[]` - Specific recommendations
- `tourist_traps_to_avoid[]` - What to skip

### Step 9: Add Logistics

```json
{
  "logistics": {
    "public_transport": {
      "ticket_types": [ ... ],
      "where_to_buy": { ... },
      "operating_hours": { ... }
    },
    "bike_rentals": { ... },
    "emergency_contacts": { ... },
    "practical_tips": [ ... ]
  }
}
```

### Step 10: Document Research

```json
{
  "research_notes": {
    "sources": [
      {
        "name": "Rick Steves Paris Guide",
        "url": "https://...",
        "type": "guide"
      }
    ],
    "alternatives_considered": [
      {
        "name": "Versailles Day Trip",
        "reason_not_selected": "Not enough time in 4 days"
      }
    ],
    "notes": "Focused on central Paris, skipped distant attractions"
  }
}
```

Also add per-day research notes:
```json
{
  "days": [
    {
      "date": "2026-10-17",
      "research_notes": {
        "alternatives": [...],
        "sources": [...],
        "notes": "..."
      }
    }
  ]
}
```

---

## 🏷️ Emoji Tags (REQUIRED)

Apply these standardized tags to every activity:

### Cost & Booking
- 🆓 **Free** - No admission fee
- 🎟️ **Paid** - Requires ticket
- 📅 **Reservation Required** - Must book ahead

### Visit Style
- 👀 **See & Continue** - Quick stop (10-30 min)
- ⏳ **Be There** - Full experience (1-3+ hours)

### Special
- ⭐ **Top Highlight** - Must-see spot
- 📸 **Photo Spot** - Great for photos
- ☂️ **Indoor** - Rain-friendly
- 🍽️ **Dining** - Food/restaurant

**Usage:**
```json
"tags": ["🎟️", "⏳", "⭐", "☂️"]
```

---

## ✅ Quality Standards

### Every Activity Must Have:
- [x] `name` - Clear, specific name
- [x] `link` - Google Maps or official website
- [x] `priority` - mandatory | high | medium | low | optional
- [x] `tags` - Emoji array
- [x] `duration` - Estimated time (minutes or string)

### Recommended:
- [ ] `suggestedTime` - Start time (HH:MM)
- [ ] `timeRestriction` - Opening hours
- [ ] `bookingRequired` - true/false
- [ ] `notes` - Tips or important info

### Food Names:
- [x] `name_local` - In local language
- [x] `name_english` - In English or Spanish
- [x] `description` - Brief description
- [x] `typical_cost` - Price range

---

## 📐 Critical Rules

### ✅ DO:

1. **Ask for dates first** - Cannot proceed without them
2. **Use actual calendar dates** - `"2026-10-17"` not "Day 1"
3. **One activity per entry** - Granular, not grouped
4. **Include emoji tags** - On every activity
5. **Dual-language food names** - Local + English/Spanish
6. **Store transport in both cities** - Arrival AND departure city JSON
7. **Create round-trip maps** - From accommodation and back
8. **Document sources** - In research_notes
9. **Use 24-hour time** - "14:30" not "2:30 PM"
10. **Test all links** - Verify Google Maps URLs work

### ❌ DON'T:

1. **Don't skip dates** - They're mandatory
2. **Don't batch activities** - "Morning walk" → separate places
3. **Don't forget time blocks** - Every day needs morning/lunch/afternoon/evening
4. **Don't omit booking info** - If required, include URL and timing
5. **Don't use 12-hour time** - Always 24-hour format
6. **Don't forget emoji legend** - Include at bottom of JSON
7. **Don't skip food section** - It's required
8. **Don't ignore logistics** - Transport and emergencies matter

---

## 🎯 Common Patterns

### Museum/Attraction
```json
{
  "name": "Louvre Museum",
  "link": "https://www.google.com/maps/search/Louvre+Museum+Paris",
  "duration": 180,
  "suggestedTime": "09:00",
  "timeRestriction": "09:00-18:00 (closed Tue)",
  "priority": "high",
  "tags": ["🎟️", "⏳", "⭐", "☂️", "📅"],
  "bookingRequired": true,
  "bookingDetails": {
    "url": "https://www.louvre.fr/en/visit/hours-admission",
    "advanceTimeNeeded": "1-2 days"
  },
  "cost": "17 EUR"
}
```

### Quick Photo Stop
```json
{
  "name": "Eiffel Tower (exterior)",
  "link": "https://www.google.com/maps/search/Eiffel+Tower",
  "duration": 20,
  "priority": "high",
  "tags": ["🆓", "👀", "📸"],
  "cost": "free",
  "notes": "View from Trocadéro for best photos"
}
```

### Restaurant/Café
```json
{
  "name": "Café de Flore",
  "link": "https://www.google.com/maps/search/Café+de+Flore+Paris",
  "duration": 90,
  "priority": "medium",
  "tags": ["🍽️", "⭐"],
  "priceRange": "€€",
  "notes": "Historic café, order croissant and café crème"
}
```

### Park/Outdoor
```json
{
  "name": "Luxembourg Gardens",
  "link": "https://www.google.com/maps/search/Luxembourg+Gardens+Paris",
  "duration": 60,
  "priority": "low",
  "tags": ["🆓", "👀"],
  "cost": "free",
  "optional": true
}
```

---

## 📋 Final Checklist

Before delivering your work:

### Structure
- [ ] JSON is valid (no syntax errors)
- [ ] Follows schema in `destination-data-schema.json`
- [ ] All required fields populated

### Content
- [ ] Dates section with correct start/end dates
- [ ] Each day has actual calendar date (YYYY-MM-DD)
- [ ] All activities have name, link, priority, tags
- [ ] Food names in dual language
- [ ] Logistics section complete
- [ ] Research notes with sources

### Quality
- [ ] All Google Maps links tested and working
- [ ] Emoji tags applied consistently
- [ ] Times in 24-hour format (HH:MM)
- [ ] Opening hours included where relevant
- [ ] Booking requirements noted
- [ ] At least one map per day

### Transport
- [ ] Arrival transport documented (from previous city)
- [ ] Departure transport documented (to next city)
- [ ] Remember to note this in BOTH cities' JSON files

---

## 🔧 Troubleshooting

### "I don't know the dates"
→ **STOP.** Ask the user for dates before proceeding.

### "Too many activities to list individually"
→ Group logically but still separate major stops. Use `secondaryPlaces` for minor spots.

### "User's guide doesn't match our format"
→ Use `trip-itinerary-generator` skill to transform, then validate against schema.

### "Opening hours not available"
→ Use `null` or omit field, note in research_notes.

### "Can't find food recommendations"
→ Research local cuisine guides, food blogs, or ask user for preferences.

---

## 📚 Reference Files

- **`.agents/destination-template.json`** - Copy this as starting point
- **`.agents/destination-data-schema.json`** - Structure validation
- **`Barcelona/barcelona_itinerary.json`** - Complete example
- **`Bruges/bruges_itinerary.json`** - Another example

---

## 🎯 Activity Selection & Reasoning

When planning activities, always document WHY you selected or rejected options. This helps users understand the logic and make informed changes.

### Document in `research_notes.alternatives`

For EACH DAY, include an `alternatives` array with rejected options:

```json
"research_notes": {
  "alternatives": [
    {
      "name": "Musée de Cluny",
      "reason_not_selected": "€9 student, 90 min visit. Too much for arrival day. Can add if you skip some Latin Quarter walking or save for Day 4.",
      "when_to_add": "Day 4 if you want more museums"
    },
    {
      "name": "Notre-Dame Exterior Walk-by",
      "reason_not_selected": "Quick 15 min stop from Shakespeare & Co. Saved for Day 4 when doing full Île de la Cité tour.",
      "when_to_add": "Afternoon if near area, or save for Day 4"
    }
  ],
  "sources": [...],
  "notes": "Day 1 restructured to include Montmartre sunset..."
}
```

### Document in Overall `research_notes.alternatives_considered`

For MAJOR decisions affecting the whole trip, add to the top-level `research_notes`:

```json
"research_notes": {
  "alternatives_considered": [
    {
      "name": "4-Day Museum Pass (€62)",
      "reason_not_selected": "2-Day Museum Pass (€55) is more efficient. Concentrated museum days on Sat-Sun (Days 2-3). Saves €30 vs trying to use 4-day pass with gaps.",
      "notes": "2-day pass strategy covers: Hôtel de la Marine, Invalides, Arc (Day 2), Versailles, Orsay (Day 3). Louvre separate ticket Day 4."
    },
    {
      "name": "Hôtel Madrigal (original accommodation)",
      "reason_not_selected": "Switched to St Christopher's Inn - closer to Bercy bus station (15 min vs 25 min), near Canal/Montmartre, social hostel atmosphere, cheaper.",
      "notes": "St Christopher's saves 10 min on Day 5 departure and puts you near Montmartre."
    },
    {
      "name": "Le Marais on Day 4 (original plan)",
      "reason_not_selected": "Moved Le Marais to Day 1 evening to free up Day 4 for Palais Garnier + Louvre + Islands.",
      "notes": "Day 4 now: Palais Garnier → Louvre → Île de la Cité → Panthéon."
    }
  ]
}
```

### Why This Matters

**For the User:**
- Understands the reasoning behind the plan
- Can easily swap alternatives if preferences differ
- Sees what was considered but rejected

**For Future Agents:**
- Context for why certain choices were made
- Guidance on what can be swapped without breaking flow
- Documented research prevents duplicate work

### Real Example: Paris Day 5 Decision

**Original Plan:** 04:00-06:00 Montmartre walk before 06:30 bus departure

**Problem:** Too rushed, defeats the purpose of enjoying Montmartre

**Solution:** Move Montmartre to Day 1 evening (sunset at Sacré-Cœur)

**Documentation:**
```json
{
  "name": "Day 5 Early Morning Montmartre (04:00-06:00)",
  "reason_not_selected": "Too rushed before 06:30 FlixBus. Moved Montmartre to Day 1 late afternoon/evening for sunset at Sacré-Cœur - much better experience and no 4am wake-up!",
  "notes": "Day 5 now pure departure logistics (05:45 leave hostel → 06:00 at bus station)."
}
```

### Selection Criteria to Consider

When choosing activities, document reasoning based on:

1. **Time constraints** - "90 min museum doesn't fit after 2-hour Louvre visit"
2. **Energy levels** - "Too much for arrival day"
3. **Geographic flow** - "Backtracking from Eiffel to Marais, saved for Day 1"
4. **Opening hours** - "Closed Mondays, conflicts with departure day"
5. **Cost optimization** - "Museum Pass expired, buying separate ticket"
6. **Thematic coherence** - "Day 2 = Royal Paris, saving Latin Quarter for Day 1"
7. **User preferences** - "User requested Palais Garnier, moved activities from Day 4 to Day 1"
8. **Practical logistics** - "Near hostel, easy to add any evening"

### Template for Alternatives

Use this structure for each alternative:

```json
{
  "name": "Clear, specific name",
  "reason_not_selected": "Why NOT in main plan: timing/cost/energy/flow/preference",
  "when_to_add": "Specific guidance: 'Morning of Day 3 instead of X' or 'If you skip Y'"
}
```

**Keep it actionable** - User should know exactly WHEN and HOW to add the alternative.

---

## 💡 Pro Tips

1. **Start with the template** - Don't write JSON from scratch
2. **Research first, structure later** - Gather all info, then organize
3. **Think about flow** - Minimize backtracking, group nearby places
4. **Consider timing** - Match activities to opening hours
5. **Account for meals** - Lunch and dinner are time blocks
6. **Include alternatives** - Rainy day options, plan B's
7. **Be specific** - "Notre-Dame Cathedral" not "cathedral"
8. **Test your route** - Click the Google Maps link
9. **Document as you go** - Add sources immediately
10. **Validate at the end** - Check against schema
11. **Document ALL decisions** - Why you selected AND rejected activities
12. **Make alternatives actionable** - Tell user exactly when/how to swap

---

**Ready?** Confirm the dates with the user and start creating!
