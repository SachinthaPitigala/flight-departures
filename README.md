# ✈️ Seattle-Tacoma (SEA) Flight Departure Delays: A Carrier Reliability Data Story

An exploratory visual analysis of **110,977 commercial flight departures** from Seattle-Tacoma International Airport (SEA) across six major domestic carriers: **Alaska Airlines (AS)**, **Delta Air Lines (DL)**, **United Airlines (UA)**, **Southwest Airlines (WN)**, **American Airlines (AA)**, and **JetBlue Airways (B6)**.

---

## 📌 Executive Summary

If you are flying out of Seattle, **which airline you book dramatically changes your odds of leaving on time—and your risk of getting stranded by a multi-hour delay.**

* **Best Overall Reliability:** **United (UA)** and **Delta (DL)** lead SEA in on-time performance, with fewer than **23%** of flights delayed beyond 5 minutes and median departures running **3 to 4 minutes early**.
* **Highest Delay Frequency:** **JetBlue (B6)** and **Southwest (WN)** experience delays (>5 minutes) on nearly **half of all departures** (**46.96%** and **46.25%**, respectively).
* **The "Hometown Hub" Trade-Off:** **Alaska Airlines (AS)** operates **57.5%** of all analyzed departures (63,762 flights). While **36.44%** of its flights leave more than 5 minutes late, Alaska tightly caps catastrophic tail risk—only **0.46%** of its flights are delayed over 3 hours, the lowest severe-disruption rate of any carrier.
* **Hidden Extreme Outliers:** While typical delays cluster under 30 minutes, extreme tail events stretch up to **28 hours (1,679 minutes)**, pulling carrier averages far above their medians.

---

## 📊 Visual Walkthrough & Key Findings

### 1. The Headline Comparison: Share of Flights Delayed > 5 Minutes

<iframe
  src="charts/carrier_delay_bar.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

Looking at the percentage of flights departing more than 5 minutes past schedule reveals a sharp three-tier divide among Seattle carriers:

| Carrier | Code | Total Flights | Share of SEA Volume | Delayed > 5 Min | Median Delay | Mean Delay |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **United Airlines** | `UA` | 7,852 | 7.1% | **21.47%** | -4.0 min | 8.95 min |
| **Delta Air Lines** | `DL` | 26,671 | 24.0% | **22.52%** | -3.0 min | 7.53 min |
| **American Airlines** | `AA` | 5,141 | 4.6% | **30.13%** | -3.0 min | 15.31 min |
| **Alaska Airlines** | `AS` | 63,762 | 57.5% | **36.44%** | 0.0 min | 10.19 min |
| **Southwest Airlines** | `WN` | 6,991 | 6.3% | **46.25%** | +4.0 min | 15.50 min |
| **JetBlue Airways** | `B6` | 560 | 0.5% | **46.96%** | +2.0 min | 37.44 min |

* **Takeaway:** Passengers on JetBlue and Southwest are **more than twice as likely** to experience a >5-minute departure delay compared to passengers on United or Delta.

---

### 2. Full Departure Distributions: Early Pushbacks vs. Routine Lateness

<iframe
  src="charts/carrier_delay_histograms.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

When zooming into the core operational window (-26 to +120 minutes), the probability histograms show why averages alone can be misleading:

* **The Early-Departure Advantage (`UA`, `DL`, `AA`):** Over **73.9%** of United flights, **70.8%** of Delta flights, and **64.9%** of American flights push back **on time or early (≤ 0 minutes)**. Their distributions peak sharply between `-7` and `-3` minutes.
* **The Schedule-Creep Shift (`AS`, `WN`):** Alaska Airlines centers right on the 0-minute mark (**53.2%** on time or early), whereas Southwest's entire distribution is shifted rightward, with only **41.8%** of flights departing on or before schedule.

---

### 3. Zooming In on Actual Delays (≥ 0 Minutes)

<iframe
  src="charts/real_carrier_delay_histograms.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

Once a flight fails to leave early, how long do passengers actually wait? Filtering exclusively to non-negative departure delays (0 to 120 minutes) isolates true delay severity:

* **Delta (`DL`) Recovers Fastest:** Even among delayed flights, Delta maintains the lowest median delay (**9 minutes**) and lowest average delay (**19.77 minutes**), with only **37.3%** exceeding the FAA's 15-minute late threshold.
* **Alaska (`AS`) & Southwest (`WN`) Cluster in Short Delays:** Both carriers share a median delay of **13 minutes** among delayed departures, with roughly **44%–45%** crossing the 15-minute mark.
* **JetBlue (`B6`) Suffers Heavy Delays:** Among JetBlue flights departing at or after 0 minutes, the median delay jumps to **22 minutes** (mean **32.39 minutes**), and **18.4%** of those flights are delayed more than an hour.

---

### 4. Extreme Tail Risk & Operational Outliers

<iframe
  src="charts/carrier_delay_stripchart.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

Box-and-strip plots across the uncapped dataset expose the long right tail of aviation disruptions—weather holds, mechanical swaps, and cascading crew timeouts:

| Carrier | IQR (25th–75th Pct) | 90th Percentile | Flights > 60 Min | Flights > 180 Min | Max Recorded Delay |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Delta (`DL`)** | -7 to +4 min | 28.0 min | 5.16% | 1.05% | 1,113 min (18.6 hrs) |
| **Alaska (`AS`)** | -5 to +14 min | 38.0 min | **4.88%** | **0.46%** | 582 min (9.7 hrs) |
| **United (`UA`)** | -7 to +2 min | 35.0 min | 6.36% | 1.31% | 1,113 min (18.6 hrs) |
| **American (`AA`)** | -6 to +10 min | 43.0 min | 6.65% | 1.54% | **1,679 min (28.0 hrs)** |
| **Southwest (`WN`)** | -2 to +20 min | 48.0 min | 7.12% | 0.80% | **350 min (5.8 hrs)** |
| **JetBlue (`B6`)** | -5 to +36 min | **93.1 min** | **16.07%** | **3.04%** | 1,427 min (23.8 hrs) |

* **Hub Advantage in Recovery:** Because Seattle is Alaska Airlines' primary hub—and a major hub for Delta—both airlines have spare aircraft and reserve crews on-site to prevent minor delays from spiraling into 10+ hour cancellations.
* **Out-of-Station Vulnerability:** Carriers with smaller Seattle footprints (`B6`, `AA`) exhibit extreme maximum delays (23.8 to 28.0 hours), reflecting overnight aircraft-on-ground (AOG) recovery bottlenecks when an inbound plane breaks down away from a main hub.

---

## 💡 Actionable Takeaways for Travelers

1. **For Tight Connections:** Book **Delta (`DL`)** or **United (`UA`)**. Their 75th-percentile departure times are **+4 minutes** and **+2 minutes**, meaning 3 out of 4 flights leave essentially on time.
2. **For Lower Worst-Case Disruption Risk:** **Alaska Airlines (`AS`)** offers the tightest cap on severe delays (>60 min at **4.88%**, >3 hrs at **0.46%**) thanks to unmatched fleet and crew depth at SEA.
3. **Build Buffer Time on Point-to-Point Carriers:** When flying **Southwest (`WN`)** or **JetBlue (`B6`)** out of SEA, avoid tight same-day connections—nearly 1 in 2 flights departs more than 5 minutes behind schedule.
