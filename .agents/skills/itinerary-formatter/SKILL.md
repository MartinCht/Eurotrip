---
name: itinerary-formatter
description: Triggers when creating, editing, or formatting travel itineraries across Markdown, HTML, or any format. Enforces Name-first item structure followed by standardized emoji-only tags for cost, reservations, visit pacing, and highlights.
---

# Itinerary Formatter & Tagging Rules

Use this skill whenever generating, editing, or formatting travel itineraries, day-by-day plans, or city guides in Markdown, HTML, or any text format.

## 🏷️ Mandatory Formatting Rule: Name First, Tags Second
Every attraction, restaurant, or activity item must place the **Name first**, followed by an en-dash/separator and the **emoji-only tag string**.

* **Markdown Format:** `- **Attraction Name** — [Tags]`
* **HTML Format:** `<li><strong>Attraction Name</strong> — [Tags] ...</li>`

---

## 🎨 Emoji-Only Tagging Legend

Every stop must be tagged using the exact emoji combinations below:

### 1. Cost & Booking Status
- `🆓` **Free:** No admission fee (public squares, parks, exterior views, free museums).
- `🎟️` **Paid:** Requires a ticket or entrance fee.
- `📅` **Reservation Required:** Must be booked in advance (combine with cost, e.g., `🎟️📅` or `🆓📅`).

### 2. Visit Style & Pacing
- `👀` **See & Continue:** Quick stop, exterior view, photo op, stroll, or passing through (10–30 mins).
- `⏳` **Be There:** Immersive visit, full museum tour, sit-down experience, or extended stay (1–3+ hours).

### 3. Extra Useful Markers
- `⭐` **Top Highlight:** Must-see priority spot or star recommendation.
- `📸` **Photo Spot:** Prime viewpoint, aesthetic alley, or panoramic angle.
- `☂️` **Indoor / Rainy Day:** Fully indoor activity (essential backup for bad weather).

---

## 📋 Itinerary Structure & Creation Rules
1. **Chronological Structure:** Organize each day into Morning 🌅, Lunch 🍽️, Afternoon ☀️, Evening 🌆, and Night Optional 🌙.
2. **Logical Flow:** Sequence stops geographically to minimize backtracking and ensure smooth walking/transit routes.
3. **Balanced Pacing:** Alternate between `👀` (light walking/views) and `⏳` (seated/deep visits) to prevent travel fatigue.
4. **Primary & Secondary Locations:**
   - **Primary Locations:** Main destinations (museums, monuments, major squares) are listed as main bullet points with full tags (`Name — [Tags]`).
   - **Secondary Locations:** Complementary sub-stops attached to a primary location (such as recommended dining spots, cafés, or adjacent viewpoints) are nested as sub-bullets, also following the **Name First + Emoji-Only Tags** format.
5. **Examples:**
   - `- **Museo del Louvre** — 🎟️📅⏳ ⭐`
     - `- **Café Marly (Inside Louvre)** — 🎟️⏳ 🍽️` (Secondary location for dining)
   - `- **Pont Alexandre III** — 🆓👀 📸`
   - `- **Barrio de Montmartre** — 🆓👀`
     - `- **Le Pure Café** — 🎟️⏳ 🍽️` (Secondary location for coffee/meal near Montmartre)
