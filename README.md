# NFC Freezer Meal System

A dyslexia-friendly, dark-mode meal card web app. Scan an NFC tag → see your meal's reheat steps, freshness status, and what to add fresh. Hosted free on GitHub Pages.

---

## Live URLs (after GitHub Pages is enabled)

| Page | URL | NFC Tag |
|------|-----|---------|
| Freezer Dashboard | `https://mininedco.github.io/nfc-meals/` | Fridge door tag |
| Random Meal | `https://mininedco.github.io/nfc-meals/random.html` | "Surprise me" tag |
| Individual meal | `https://mininedco.github.io/nfc-meals/meal.html?id=bulgogi` | Tag on each bag |

### All 14 meal IDs

| ID | Meal |
|----|------|
| `bulgogi` | Korean Bulgogi |
| `gra-tiem` | Moo Gai Gra Tiem |
| `grapow` | Pad Kra Pao |
| `thai-curry` | Thai Red Curry Chicken |
| `tom-kha` | Tom Kha Gai |
| `tom-yum` | Tom Yum Concentrate |
| `japanese-curry` | Japanese Curry |
| `alfredo` | Alfredo Sauce |
| `mentaiko` | Mentaiko Cream Sauce |
| `soondubu` | Soondubu Base |
| `thai-cabbage` | Thai Cabbage Stir Fry |
| `tomato-beef` | Tomato Beef |
| `bo-luc-lac` | Bò Lúc Lắc |
| `pot-pie` | Chicken Pot Pie Filling |


---

## Programming NFC Tags

**Hardware:** NTAG213 or NTAG215 stickers (~$0.50 each on Amazon)
**App:** [NFC Tools](https://www.wakdev.com/en/apps/nfc-tools.html) (free, iOS + Android)

### Steps
1. Open NFC Tools → **Write** → **Add a record** → **URL/URI**
2. Enter the URL for that meal (e.g. `https://mininedco.github.io/nfc-meals/meal.html?id=bulgogi`)
3. Tap **Write** → hold phone to tag → done in ~1 second
4. Stick tag to freezer bag or container lid

### Tag assignments
- **Each meal bag** → `meal.html?id={meal-id}`
- **Fridge door** → `index.html` (dashboard sorted by expiration)
- **"Surprise me" tag** → `random.html` (smart random, prioritises expiring meals)

---

## Updating Meals

Edit `meals.json` — this is the only file you need to touch.

### Key fields

```json
{
  "id": "bulgogi",           // URL slug — do not change after tagging
  "name": "Korean Bulgogi",  // Display name
  "frozen_date": "2025-04-30", // YYYY-MM-DD — update when you refreeze
  "expiry_weeks": 8,         // Weeks until expiry from frozen_date
  "prep_time_min": 3,        // Minutes to prep (used for sort)
  "cook_time_min": 5         // Minutes to cook (used for sort)
}
```

### Freshness thresholds (auto-calculated)
| Days left | Status | Colour |
|-----------|--------|--------|
| > 21 days | Fresh | Teal |
| 8–21 days | Eat Soon | Amber |
| ≤ 7 days | Expiring | Red |

### Adding a new meal
Copy any existing entry in `meals.json`, change the `id` (no spaces, use hyphens), fill in the fields, save, commit, push. GitHub Pages updates in ~30 seconds.

---


