
# 🌍 Wanderwise: Smart Travel Planner UI (Vue + Naive UI)

## 🚀 Purpose

Wanderwise is a modern travel planning web application that uses AI to help users plan the **best possible trip**.  
It helps users choose flights, accommodations, restaurants, must-see places, and more — with a personalized touch and intuitive interface.  
It’s designed to make planning **fun, intelligent, and frictionless**.

---

## 🧑‍💻 Tech Stack

- **Frontend Framework**: Vue 3 (`<script setup>`)
- **Component Library**: [Naive UI](https://www.naiveui.com/) (Vue 3-compatible)
- **Design Approach**: Component-driven, responsive, mobile-first
- **Font**: Inter (Google Fonts or CDN)
- **Color Theming**: CSS variables or `n-config-provider` via Naive UI

---

## 🎨 Color Palette

Use these colors via CSS or theme overrides for Naive UI:

| Role         | Color     | Hex       | Description                        |
|--------------|-----------|-----------|------------------------------------|
| Primary      | Blue      | `#2C7BE5` | Buttons, links, active icons       |
| Secondary    | Gray      | `#6C757D` | Subtext, muted elements, tags      |
| Background   | Light Gray| `#F8F9FA` | Page and section background        |
| Card BG      | White     | `#FFFFFF` | For `n-card`, content containers   |
| Accent 1     | Teal      | `#00C9A7` | Success state, good deals          |
| Accent 2     | Amber     | `#FFC107` | Promotions, alerts                 |
| Danger       | Red       | `#DC3545` | Warnings, emergency locations      |
| Text         | Charcoal  | `#212529` | Default readable text              |

---

## ✍️ Font

- Use **Inter** as the global typeface
- Font weights: 400 (body), 600 (headings)
- Pair with generous line spacing and padding

---

## 🧩 Core Components (Vue + Naive UI)

All components must use **Naive UI** elements where possible:

- `Header.vue`: Navigation bar with logo and tabs (`n-menu` or `n-tabs`)
- `HeroSearch.vue`: Destination input, date picker, trip type, budget (`n-input`, `n-date-picker`, `n-select`)
- `ResultCards.vue`: Flight, hotel, restaurant, weather, sights, and hospital cards (`n-card`, `n-grid`)
- `PlannerPanel.vue`: Sidebar summary of selected trip details
- `Footer.vue`: Static links (`n-space`, `n-button`, `n-anchor`)

---

## 💎 Code Quality Expectations

- Use `<script setup>` syntax for all components
- Maintain scoped styles or Tailwind for consistency
- Prefer `n-grid`, `n-space`, and `n-flex` for layout
- Use reusable components and slots where needed
- Follow accessibility and semantic best practices

---

# 🧭 Refined User Flow: “Wanderwise Assistant”

A thoughtful, user-centered flow that simplifies trip planning while feeling like a guided experience.

---

## ✅ Step 1: Trip Intent & Dates

> "Where do you want to go and when?"

**Inputs**:
- Destination(s)
- Travel dates
- Trip type: Solo / Family / Business / Spiritual / Honeymoon
- Budget (optional)

**Why**: Sets the tone, feels imaginative, and gives enough context for personalization.

---

## ✅ Step 2: Flight Discovery & Selection

> "Let’s find the best way to get there."

**Features**:
- AI recommends 3–5 top flights by price, comfort, duration
- Filtering and manual browsing supported

**Why**: Flight usually locks the trip — perfect early commitment.

---

## ✅ Step 3: Accommodation

> "Now let’s find a place to rest and recharge."

**Features**:
- AI-recommended hotels with photos, price, walkability, etc.
- Filters: scenic, near city center, family-friendly

**Tip**: Show “Best Match,” “Budget Pick,” “Luxury Pick”

---

## ✅ Step 4: Weather Snapshot

> "Here's what the weather looks like during your stay."

**Features**:
- 5–7 day weather forecast
- Icons + packing suggestions (e.g., umbrella, sunscreen)

**Why**: Low effort, just helpful context.

---

## ✅ Step 5: Smart Itinerary Builder

> "Would you like a custom itinerary based on your interests?"

If YES, user selects:
- Food preferences (halal, vegan, street food)
- Interests (nature, shopping, history, kid-friendly)
- Travel pace (relaxed vs packed)

**Then**:
- AI creates day-by-day schedule: meals, places, transport, timing

**Why**: This is the “wow” moment — fully personalized travel magic.

---

## ✅ Step 6: Final Review & Save Trip

> "Here’s your trip summary:"

Includes:
- Flight + Hotel + Weather + Itinerary
- Option to download as PDF, email, or get mobile reminders
- Add-ons: emergency contacts, hospital list, etc.

---

## ✅ Flow Summary

| Step         | Goal                                |
|--------------|--------------------------------------|
| 1. Trip Setup| Get intent + dates + personality     |
| 2. Flights   | Secure travel details                |
| 3. Hotel     | Secure accommodation                 |
| 4. Weather   | Passive insight                      |
| 5. Itinerary | AI-generated joy, makes it feel real |
| 6. Summary   | Review + plan + share                |

---

## 💡 Bonus Features

- “Skip this step” option to avoid bottlenecks
- Save trip progress
- Bookmark restaurants or sights for custom planning

---

Use this guide to generate your project inside [https://bolt.new](https://bolt.new) or to scaffold your app manually in Vue.
