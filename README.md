# Eurotrip Coordinator Guide

> **Your guide** for launching agents and managing the trip

---

## 🎯 Quick Start: How to Launch an Agent

### Copy-Paste Template

```
I need you to create a complete itinerary for [CITY NAME].

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

**Start by confirming the dates with me, then proceed with research and itinerary creation.**
```

### Example: Paris

```
I need you to create a complete itinerary for Paris.

**Destination Details:**
- City: Paris
- Country: France
- Arrival Date: 2026-10-17
- Departure Date: 2026-10-21
- Previous City: Barcelona
- Next City: Bruges
- Accommodation: TBD - please research budget hostels in central Paris

**Framework:**
Read and follow `.agents/FOR_AGENTS.md` for complete instructions.

**Start by confirming the dates with me, then proceed with research and itinerary creation.**
```

---

## 🗓️ Your Trip Timeline

**🌍 Full Journey:** Buenos Aires → Barcelona → Paris → London → Bruges → Amsterdam → Berlin → Prague → Vienna → Italy → Madrid → Rosario  
**📅 Duration:** October 14 - November 12, 2026 (30 days)  
**🏠 Return Flight:** Madrid to Rosario (via World2Fly 2W2075) on November 12, 2026 - ✅ CONFIRMED (note: return lands in Rosario, not Buenos Aires)

> ⚠️ **DISCLAIMER:** Dates for Italy and Madrid below are **estimated** based on planned number of nights only. Amsterdam, Berlin, Prague, and Vienna are all fully booked (accommodation + transport). Vienna's departure flight to Italy (Treviso/Venice) IS confirmed, but everything from Treviso onward through Rome is a total blank ("black hole") - no cities, accommodation, or internal transport defined. The Rome→Madrid flight is also not booked yet. Dates will shift if bookings require adjustments.

### Confirmed Destinations

| # | City | Country | Dates | Nights | Status |
|---|------|---------|-------|--------|--------|
| 1 | **Barcelona** | Spain 🇪🇸 | Oct 14-17, 2026 | 3 | ✅ Complete |
| 2 | **Paris** | France 🇫🇷 | Oct 17-21, 2026 | 4 | ✅ Complete |
| 3 | **London** | United Kingdom 🇬🇧 | Oct 21-24, 2026 | 3 | ✅ Complete |
| 4 | **Bruges** | Belgium 🇧🇪 | Oct 25, 2026 (stopover) | 0 (no overnight) | ✅ Complete |
| 5 | **Amsterdam** | Netherlands 🇳🇱 | Oct 25-28, 2026 | 3 | ✅ Complete |
| 6 | **Berlin** | Germany 🇩🇪 | Oct 28-30, 2026 | 2 | ✅ Complete |
| 7 | **Prague** | Czech Republic 🇨🇿 | Oct 30 - Nov 1, 2026 | 2 | ✅ Complete |
| 8 | **Vienna** | Austria 🇦🇹 | Nov 1-3, 2026 | 2 | ✅ Complete |

### Planned Destinations (Estimated Dates - Accommodation/Transport TBD)

| # | City | Country | Estimated Dates | Nights | Status |
|---|------|---------|------------------|--------|--------|
| 9 | **Italy** (Treviso/Venice → ??? → Rome) | Italy 🇮🇹 | Nov 3-10, 2026 (approx.) | ~7 (cities/dates TBD) | ✅ Arrival flight confirmed (Treviso); 🕳️ everything else undefined |
| 10 | **Madrid** | Spain 🇪🇸 | Nov 10-12, 2026 | 2 | ⚠️ Hostel selected (Onefam Sungate, not booked); arrival flight candidate (Ryanair FR 9601, ~€110) pending |

### Trip Flow

```
Buenos Aires (Departure)
    ↓ Flight
Barcelona (Oct 14-17)
    ↓ Flight
Paris (Oct 17-21)
    ↓ Eurostar
London (Oct 21-24)
    ↓ FlixBus (overnight)
Bruges (Oct 25, stopover)
    ↓ FlixBus
Amsterdam (Oct 25-28) ✅ confirmed
    ↓ DB ICE 141 (confirmed)
Berlin (Oct 28-30) ✅ confirmed
    ↓ DB RJ 171 (confirmed)
Prague (Oct 30-Nov 1) ✅ confirmed
    ↓ ÖBB EC 115 + RJ 251 (confirmed)
Vienna (Nov 1-3) ✅ confirmed
    ↓ Ryanair FR 51 (confirmed, 13:45→15:00)
Treviso/Venice (Nov 3) ✅ arrival confirmed
    ↓ 🕳️ TBD - black hole, nothing planned
Italy (Nov 3-10, approx.) 🕳️ cities/dates/booking TBD, ends in Rome
    ↓ TBD (Rome → Madrid flight candidate: Ryanair FR 9601, ~€110, shopping for better fare)
Madrid (Nov 10-12) ⚠️ hostel selected (Onefam Sungate, not booked), arrival flight pending
    ↓ World2Fly 2W2075 (confirmed, 10:25→19:00)
Rosario (Return Home) ✅ confirmed - NOTE: lands in Rosario, not Buenos Aires
```

---

## ✅ Before Launching an Agent

Make sure you have:
- [ ] Exact arrival date (YYYY-MM-DD)
- [ ] Exact departure date (YYYY-MM-DD)
- [ ] Previous city name (for transport context)
- [ ] Next city name (for transport planning)
- [ ] Accommodation info or "TBD"
- [ ] Any special requirements (dietary, interests, budget)

---

## 📋 After Agent Completes

### Verification Checklist

- [ ] File created: `CityName/cityname_itinerary.json`
- [ ] JSON is valid (no syntax errors)
- [ ] Dates section has correct start/end dates
- [ ] Each day has the actual calendar date
- [ ] Activities organized in time blocks (morning, lunch, afternoon, evening)
- [ ] Food recommendations included (with local + English/Spanish names)
- [ ] Logistics section complete (transport, emergencies)
- [ ] Google Maps links work
- [ ] Research notes included with sources

### Common Adjustments

If you need changes, ask the agent:
- "Add more food recommendations"
- "Include rainy day alternatives"
- "Reduce walking on Day 2"
- "Find cheaper accommodation"
- "Add more museum options"

---

## 🎨 Optional Add-Ons for Your Launch Message

### Special Interests
```
**Special Interests:**
- Museums and art galleries
- Local food markets
- Historical WWII sites
- Nature/parks
- Architecture
- Nightlife (or skip nightlife)
```

### Dietary Requirements
```
**Dietary Notes:**
- Vegetarian/vegan
- Allergies: [list]
- Prefer local specialties over tourist restaurants
```

### Budget Preferences
```
**Budget:**
- ~50 EUR/day for activities
- Prefer free walking tours
- Willing to splurge on: [specific attraction/meal]
```

### Mobility/Accessibility
```
**Accessibility:**
- Prefer less intensive walking
- Need wheelchair-accessible routes
- Interested in bike rentals
```

---

## 🚀 Working with Multiple Agents

You can launch multiple agents in parallel once you have dates:

**Example: 3 Agents at Once**

1. **Agent 1** → Amsterdam (Oct 23-26, 2026)
2. **Agent 2** → Berlin (Oct 27-30, 2026)
3. **Agent 3** → Prague (Oct 31-Nov 3, 2026)

Each agent works in their own destination folder - no conflicts!

---

## 📁 File Structure

```
Eurotrip/
├── .agents/
│   ├── FOR_YOU.md                    ← You're reading this
│   ├── FOR_AGENTS.md                 ← Agents read this
│   ├── destination-template.json     ← Blank template
│   └── destination-data-schema.json  ← Structure reference
│
├── Barcelona/
│   └── barcelona_itinerary.json      ✅ Complete
│
├── Paris/
│   └── paris_itinerary.json          🚧 In progress
│
├── Bruges/
│   └── bruges_itinerary.json         ✅ Complete
│
└── [Future cities...]
```

---

## 🎯 Framework Overview

### What Agents Produce

Each destination gets a JSON file with:

```
{
  destination + country + dates
  ├── accommodation (name, address, meals included)
  ├── transport (arrival from prev city, departure to next)
  ├── days[]
  │   └── each day
  │       ├── date (YYYY-MM-DD)
  │       ├── time blocks (morning, lunch, afternoon, evening, night)
  │       │   └── activities[]
  │       │       ├── name, Google Maps link, duration
  │       │       ├── emoji tags 🆓🎟️📅👀⏳⭐📸☂️🍽️
  │       │       ├── priority, booking info, costs
  │       │       └── notes
  │       ├── map_url (round-trip route for the day)
  │       └── research_notes (alternatives, sources)
  ├── food_recommendations (dual-language dishes, drinks, restaurants)
  ├── logistics (transport, emergency contacts, tips)
  ├── maps (curated collections)
  └── research_notes (sources, alternatives)
}
```

### Emoji Tags (from itinerary-formatter skill)

**Cost & Booking**
- 🆓 Free
- 🎟️ Paid
- 📅 Reservation Required

**Visit Style**
- 👀 See & Continue (10-30 min)
- ⏳ Be There (1-3+ hours)

**Special**
- ⭐ Top Highlight
- 📸 Photo Spot
- ☂️ Indoor/Rain-friendly
- 🍽️ Dining

---

## 🔧 Troubleshooting

### Agent didn't ask for dates
→ Remind: "Please confirm the dates first as required by the framework."

### Agent created wrong structure
→ Point to example: "Follow the structure in `Barcelona/barcelona_itinerary.json`"

### Missing food recommendations
→ Reference: "Please add the food_recommendations section as shown in FOR_AGENTS.md"

### JSON errors
→ Ask: "Please validate the JSON syntax"

### Broken Google Maps links
→ Request: "Please test all map links and fix any broken ones"

---

## 📊 Transport Tracking

### Confirmed Transport

1. **Buenos Aires → Barcelona**: LEVEL LL2602, Oct 14, 05:25 arrival at BCN
2. **Barcelona → Paris**: Vueling VY8002, Oct 17, 08:45 BCN → 10:35 ORY
3. **Paris → London**: Eurostar, Oct 21, 07:32 Gare du Nord → 09:00 St Pancras
4. **London → Bruges**: FlixBus N814, Oct 24 19:30 → Oct 25 03:00
5. **Bruges → Amsterdam**: FlixBus 802, Oct 25, 16:10 → 20:20
6. **Amsterdam → Berlin**: DB ICE 141, Oct 28, 05:45 Amsterdam Centraal → 12:50 Berlin Hbf
7. **Berlin → Prague**: DB RJ 171, Oct 30, 07:28 Berlin Hbf → 11:25 Praha hl.n.
8. **Prague → Vienna**: ÖBB EC 115 + RJ 251, Nov 1, 10:08 Praha hl.n. → 14:49 Wien Hbf (via Pardubice)
9. **Vienna → Treviso/Venice**: Ryanair FR 51, Nov 3, 13:45 VIE → 15:00 TSF
10. **Madrid → Rosario**: World2Fly 2W2075, Nov 12, 10:25 MAD → 19:00 ROS (return home - note: lands in Rosario, not Buenos Aires)

### To Be Booked ⚠️

11. Italy internal transport (Treviso/Venice → ... → Rome) - cities/route undefined
12. Rome → Madrid - candidate flight Ryanair FR 9601 (~€110, shopping for a better fare/date before booking)

---

## 💡 Pro Tips

### For Best Results:

1. **Always provide exact dates** - Agents cannot work without them
2. **Mention previous/next city** - Helps with transport planning
3. **Share your interests** - Gets better activity recommendations
4. **Reference existing work** - "Similar to Barcelona but shorter"
5. **Be specific about meals** - Does accommodation include meals?
6. **Set budget expectations** - Free/cheap or willing to splurge?

### For Efficiency:

1. **Batch similar cities** - Research Berlin + Prague together
2. **Plan transport ahead** - Book early for better prices
3. **Consider geography** - Group nearby cities
4. **Check opening hours** - Some places closed Mondays
5. **Factor in travel days** - Arrival/departure days have less time

---

## 📝 Quick Reference

| Need to... | Do this... |
|------------|-----------|
| Launch an agent | Copy template at top, fill in details, send |
| Check trip progress | See timeline table above |
| Verify completed work | Use verification checklist |
| Make changes | Ask agent for specific adjustments |
| Work on multiple cities | Launch multiple agents in parallel |
| Track transport | See transport tracking section |

---

## 🎯 Next Steps

### For Italy / Madrid (Current):
Amsterdam, Berlin, Prague, and Vienna are all fully booked (accommodation + transport). Vienna→Treviso/Venice flight is confirmed, as is the Madrid→Rosario return flight. Madrid now has a full day-by-day plan (`9- Madrid/madrid_itinerary.json`) and a selected hostel (Onefam Sungate), but it's not booked yet, and the Rome→Madrid flight is still just a candidate (Ryanair FR 9601, ~€110 - shopping for a better fare). Still need: cities/accommodation/internal transport for Italy (the "black hole" between Treviso and Rome).

### For Future Destinations:
1. Decide exact cities/route for Italy (arrival is Treviso/Venice, must end in Rome for the eventual Rome→Madrid flight)
2. Book accommodation & internal transport for Italy
3. Book the Rome→Madrid flight once a better fare/date is found (or confirm FR 9601 if no better option appears)
4. Book Onefam Sungate in Madrid via the Cloudbeds link
5. Update the timeline table above as bookings are confirmed
6. Use the template to launch agents
7. Review and track progress

---

**Questions?** Check `.agents/FOR_AGENTS.md` to see what agents are being instructed to do.

**Need the technical structure?** See `.agents/destination-data-schema.json` for the complete JSON schema.
