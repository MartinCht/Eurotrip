---
name: trip-itinerary-generator
description: Generates structured, destination-agnostic travel guides and itineraries (HTML & Markdown) based on source documents/guides, user accommodation, and dining constraints. Formats itineraries with round-trip Google Maps links, dual-language food terminology, practical logistics, and curated place lists.
---

# Trip Itinerary Generator

Use this skill whenever asked to analyze city guides/documents and generate customized travel itineraries and city companion guides.

## Core Preferences & Structural Rules

Every generated guide/itinerary must follow this exact sequence and formatting logic:

### 1. Document Structure & Order
1. **Itinerary (First Section):** Day-by-day breakdown with Morning, Lunch, Afternoon, Evening, and Night Optional activities.
2. **Food Recommendations & Dining Culture (Second Section):** Consolidated culinary guide.
3. **Logistics & Essential Info (Third Section):** Arrival/airport transit, public transit tickets & apps, bike rentals, and emergency numbers. *(Do NOT include behavioral etiquette, street conduct rules, or generic safety lectures—only retain emergency contacts and essential ticket/transit mechanics).*
4. **Maps Lists (Fourth Section):** Dedicated links for curated recommendations and local markets.

---

### 2. Map Links & Routing Rules

* **Daily Itinerary Maps:** Must be **multi-stop round-trip routes** in Google Maps (`https://www.google.com/maps/dir/...`) that start at the user's accommodation/hostel, progress sequentially through the day's stops, and return to the accommodation.
* **POI / Markets / Place Lists:** Must **NOT** be generated as routes. They must open as a single consolidated search/list link on Google Maps (e.g. using `https://www.google.com/maps/search/Stop1+OR+Stop2+OR+...`) or direct list link so all places are viewed simultaneously without drawing a route line.
* **Curated Maps:** Retain external/embedded custom map URLs provided in the source materials.

---

### 3. Food & Drink Formatting Rules

* **Dual Naming (Food Section):** In the consolidated food section, list items showing **Local Name / English Name** without attributing regional/origin tags.
  * *Example:* `Pa amb tomàquet / Bread with Tomato & Olive Oil: ...`
* **Consistent Local Naming:** Throughout the rest of the guide (itinerary descriptions, meal tips, lunch recommendations), **always refer to dishes, drinks, and meal rituals by their local/native name** (e.g., *menú del día*, *pa amb tomàquet*, *la hora del vermut*, *fricandó*).
* **Meal Context:** Accommodate hostel/hotel meal inclusions (e.g., if breakfast and dinner are included at the accommodation, tailor restaurant/food highlights specifically to lunch, afternoon aperitifs, and late snacks).
* **Anti-Trap Advice:** Highlight local dining authenticities (lunch fixed-price menus, authentic drink choices vs. tourist traps).

---

### 4. Logistics & Mobility Rules

* **Ticket Purchasing:** Explicitly state where to purchase physical transport cards (vending machines/stations) and whether digital purchase/validation is possible via official local mobile apps.
* **Public Bikes:** Verify if the municipal bike-share system is restricted to local residents (requiring local ID/tax numbers) and immediately provide tourist-accessible alternatives (e.g. Donkey Republic, Cooltra, local rental shops).
* **Safety Info:** Keep concise, focusing strictly on emergency telephone numbers and local police contacts.

---

### 5. Output Deliverables
* Always provide clean, responsive standalone HTML (`.html`) styling with clear visual hierarchy, accessible buttons for Google Maps links, and semantic cards per day.
