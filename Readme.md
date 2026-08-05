<img width="1672" height="941" alt="Astrology API" src="https://github.com/user-attachments/assets/474f2913-4b67-4358-b936-33601f348a4f" />

# Jyothisya API — Vedic Astrology (Jyotish) Kundali & Horoscope API

## 🌟 What is the Jyothisya API?

The **Jyothisya API** is a production-grade Vedic Astrology (Jyotish) API for developers building horoscope apps, kundali generators, matchmaking platforms, and astrology SaaS products. It calculates accurate birth charts (kundali), planetary positions, dasha periods, divisional charts (varga), and yogas using the **VSOP87 planetary theory** and **ELP2000 lunar theory**, with Delta-T correction applied for **±1 arcsecond positional accuracy**.

If you are searching for a **Vedic astrology API**, **Jyotish API**, **kundali API**, **birth chart API**, **horoscope API for apps**, or **Panchang API**, Jyothisya covers all of these in a single integration.

Built for real production use — mobile horoscope apps, matchmaking and compatibility platforms, astrology SaaS, daily horoscope services, remedial astrology tools, and Muhurtha/event-timing apps. Calculations follow classical **Parashara** and **Jaimini** logic (Brihat Parashara Hora Shastra) rather than simplified modern shortcuts, and the API is **not AGPL-licensed** — safe for commercial and white-label products with no source-code disclosure requirement.

---

## 🚀 Key Features

| Feature | Details |
|---|---|
| **Astronomically Grounded** | VSOP87 planetary theory + FK5 frame correction + ELP2000 lunar theory + Delta-T correction — ±1 arcsecond precision |
| **11 Planets Supported** | Sun, Moon, Mars, Mercury, Jupiter, Venus, Saturn, Rahu, Ketu, Uranus, Neptune |
| **4 Languages Built In** | English, Sinhala, Tamil, Hindi — every field returns raw + translated values |
| **5-Level Dasha System** | Maha → Antar → Vidasha → Sookshma → Prana, selectable by depth |
| **16 Divisional (Varga) Charts** | D1 through D60, including Navamsa and Dasamsa |
| **Classical BPHS & Jaimini Logic** | Not simplified or modernized shortcuts |
| **Narrative Explanations Included** | Plain-language summaries alongside raw data — no extra formatting logic needed |
| **6 Configurable Ayanamsas** | Lahiri, Tropical, Raman, KP, Yukteshwar, Fagan-Bradley |
| **5 Configurable House Systems** | Sripati, Whole Sign, Equal House, Porphyry, Placidus |
| **Single-Call Full Report** | Every module returned in one response |

---
## 🔮 Modules & Endpoints

Every module below is available as its own endpoint, and all of them together are also returned in a single `full-report` call.

| Endpoint | What It Calculates |
|---|---|
| `basic-kundali` | Free-tier birth chart with D1 and D9 |
| `kundali` | Complete birth chart — planets, lagna, bhavas, dasha periods, yogas |
| `panchanga` | Tithi, nakshatra, yoga, karana, and vaara for any date |
| `varga` | All 16 classical divisional charts, default D9 Navamsa |
| `shadbala` | Six-fold planetary strength calculation |
| `jaimini` | Arudha padas and special lagnas |
| `graha` | Planetary dignity, combustion, and retrogression |
| `sripati` | Sripati bhava cusps |
| `ashtakavarga` | Bhinna and Sarvashtakavarga scores |
| `moon-sign` | Detailed rashi and nakshatra breakdown |
| `transit` | Gochara transit positions and Gochara Pala |
| `erashtaka` | Saturn transit (Erashtaka) status, with plain-text remedies |
| `kaal-sarp` | Kaal Sarp Yoga analysis |
| `manglik` | Manglik Dosha analysis, including cancellation (bhanga) rules |
| `sadesati` | Sadesati (Saturn 7.5-year transit) analysis |
| `Dasha` | Vimshottari Dasha periods - Maha - Antar - pratyantar (120-year cycle) |
| `DashaSubTree` | Vimshottari Dasha periods - Sookshama - Prana (120-year cycle) |
| `yogini-dasha` | Yogini Dasha periods (36-year cycle) |
| `gemstone` | Gemstone recommendations based on planetary strength |
| `gulika-mandi` | Gulika and Mandi positions |
| `full-report` | Every module above, in a single response |
| `health` | Health check |

> **In short: any core Vedic horoscope calculation your app needs can be done through this single API.**
> 
<img width="1672" height="941" alt="My_2" src="https://github.com/user-attachments/assets/969b57c5-1a37-458c-861c-6cdb6d785b57" />
---

## 📝 Narrative, Human-Readable Explanations

Jyothisya doesn't just return raw structured data — several modules also include short, plain-language summaries that can be displayed directly in an app UI without any extra formatting logic:

* **Yoga summary** — plain-language count of detected yogas with an active status list
* **Kaal Sarp Yoga description** — states whether the yoga is present, partial, or absent
* **Manglik (Kuja) Dosha description** — explains whether the dosha applies and why
* **Sadesati description** — current Saturn transit status relative to the natal Moon
* **Yogini Dasha description** — explains the 36-year cycle and starting Yogini
* **Gemstone recommendation summary** — short explanation based on Lagna lord strength
* **Erashtaka status and remedies** — plain-text guidance on Saturn transit phases
* **Bhava (house) keywords** — short keyword tags for house significations

---

## 🎯 Accuracy Breakdown

| Component | Method | Accuracy |
|---|---|---|
| Planetary Longitudes | VSOP87 (truncated) + FK5 correction | &lt; 0.001° (~3.6 arcsec) |
| Moon Longitude | 30-term ELP2000 + E-factor + A1/A2 | ~4 arcsec |
| Lagna (Ascendant) | Sripati bhava system + precise sidereal time | High precision |
| Nakshatra / Pada | 27-nakshatra division of ecliptic | Exact |
| Ayanamsa | Lahiri (Chitrapaksha) + 5 alternatives | Exact |
| Delta-T (ΔT) | Terrestrial Time vs Universal Time | Applied for Moon & nodes |

---

## 🌐 Ayanamsa & House Options

### Ayanamsa Options
* `lahiri` — **Lahiri (Chitrapaksha)** — standard Vedic ayanamsa (default)
* `tropical` — **Sayana / Tropical** — no ayanamsa applied
* `raman` — **Raman** ayanamsa
* `kp` — **Krishnamurti (KP)** ayanamsa
* `yukteshwar` — **Yukteshwar** ayanamsa
* `fagan_bradley` — **Fagan-Bradley** ayanamsa

### House System Options
* `sripati` — **Sripati (Parashara)** — classical Vedic bhava system (default)
* `whole_sign` — **Whole Sign (Rashi Bhava)** — 1st house starts at 0° of Lagna
* `equal_house` — **Equal House** — 1st house cusp at exact Ascendant degree
* `porphyry` — **Porphyry** — trisects zodiacal quadrant arcs
* `placidus` — **Placidus** — Western quadrant system

---

## 🔓 Licensing — No AGPL Restrictions

**Jyothisya is not AGPL-licensed** and carries no copyleft obligations:
* **No Source-Code Disclosure:** Never required to open-source your own application
* **Commercial-Friendly:** Sell your SaaS, mobile apps, and white-label products freely
* **No Attribution Headaches:** Integrate without legal friction or compliance overhead

---

## ❓ Frequently Asked Questions

**How many planets does this API support?**
Eleven — seven classical grahas, two lunar nodes (Rahu/Ketu), and two outer planets (Uranus/Neptune).

**Is this Jyotish API based on classical Parashara rules?**
Yes. Calculations follow Brihat Parashara Hora Shastra and Jaimini Sutras rather than simplified modern shortcuts.

**Can I use this API in a commercial product?**
Yes. The API is not AGPL-licensed, so there are no copyleft or open-source disclosure requirements.

**Can I access Dasha Depth 4 (Sookshma) and Depth 5 (Prana)?**
Yes. Main endpoints are capped at Depth 3. Use the `/dasha/sub-tree` endpoint passing `parent_maha`, `parent_antar`, and `parent_pratyantar` to fetch Depth 4 and Depth 5 sub-periods (~90 nodes in &lt;10ms).

**Can I test different Ayanamsas and House Systems on the Free plan?**
The Free Plan provides access to standard Lahiri ayanamsa and Sripati house system. Custom options are unlocked on Pro and Ultra plans.

<img width="1365" height="768" alt="My_1" src="https://github.com/user-attachments/assets/36e7a8b8-11e8-4afd-b7ca-33a69c397dbe" />
