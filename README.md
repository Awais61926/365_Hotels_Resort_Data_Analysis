# 365 Hotels & Resorts — Revenue & Occupancy Analysis

## 📊 Project Overview

This project presents an end-to-end **Revenue and Occupancy Analysis** for 365 Hotels & Resorts.

The objective was to analyze hotel booking, occupancy, revenue, booking channel, and guest satisfaction data to identify performance patterns, revenue opportunities, and areas requiring management attention.

The project follows a complete data analytics workflow:

**Data Inspection → Data Cleaning → KPI Calculation → Business Analysis → Visualization → New Data Integration → Business Recommendations**

---

## 🎯 Business Objectives

The analysis focuses on answering key business questions around:

- Hotel occupancy performance
- Revenue generation
- Room-class performance
- City-level performance
- Weekday vs weekend demand
- Property-level RevPAR
- Booking channel performance
- Cancellation behavior
- Guest satisfaction
- Relationship between guest ratings and occupancy
- Integration of new monthly data

---

## 🗂️ Data

The project works with multiple datasets covering:

- Hotel/property information
- Room classes
- Calendar/date information
- Aggregated hotel bookings
- Individual booking transactions
- Additional August booking data

The datasets contain information such as:

- Property ID
- Hotel name
- City
- Hotel category
- Room category
- Booking date
- Successful bookings
- Capacity
- Revenue generated
- Revenue realized
- Booking status
- Booking platform
- Guest ratings

> **Note:** The original datasets are not included in this public repository where redistribution may not be permitted. The notebook can be reviewed alongside the original project data.

---

## 🧹 Data Cleaning

Data quality issues were investigated individually rather than automatically removing unusual values.

### Cleaning decisions included:

- Missing `capacity` values were investigated and filled using consistent property/room information.
- Missing `ratings_given` values were investigated by booking status rather than replacing them with a mean.
- Invalid `no_guests` values were identified and removed.
- Extreme `revenue_generated` values were investigated individually.
- Clear 1,000× revenue-entry errors were corrected where the intended value could be reasonably inferred.
- Extreme revenue values that could not be reliably reconstructed were removed.
- Records where `successful_bookings > capacity` were removed because they represented logically impossible occupancy records.

### Cleaning impact

- **9** invalid guest-count records removed
- **6** over-capacity records removed
- **3** obvious revenue-entry errors corrected
- **2** unresolvable extreme revenue records removed

The notebook documents the reasoning behind each cleaning decision.

---

## 📐 Key Metrics

The analysis calculates several hospitality performance metrics.

### Occupancy %

```text
Occupancy = Successful Bookings / Capacity × 100
```

### ADR — Average Daily Rate

```text
ADR = Total Realized Revenue / Completed Stays
```

Overall ADR calculated in the analysis:

**1,492.52**

### RevPAR — Revenue per Available Room

```text
RevPAR = ADR × Occupancy Rate
```

### Realization %

```text
Realization = Revenue Realized / Revenue Generated × 100
```

The analysis found average realization of approximately:

- **Cancelled:** 40.00%
- **Checked Out:** 100.00%
- **No Show:** 100.00%

### Length of Stay

```text
Length of Stay = Checkout Date − Check-in Date
```

---

## 📈 Analysis Performed

### Occupancy Analysis

The project analyzes:

- Average occupancy by city
- Occupancy by room class
- City × room-class interaction
- Weekday vs weekend occupancy
- Weekly occupancy trend
- Property-level occupancy

### Revenue Analysis

The project analyzes:

- Revenue by hotel category
- RevPAR by property
- Top and bottom RevPAR properties
- Revenue vs occupancy
- Occupancy vs RevPAR
- High-occupancy / low-RevPAR properties

A median-based test was used to identify properties with above-median occupancy and below-median RevPAR. No property met both conditions.

### Booking Channel Analysis

Booking platforms were compared using:

- Realized revenue
- Booking volume
- Cancellation rate
- Revenue per booking

Cancellation rates were broadly similar across platforms, ranging from approximately **24.30% to 24.99%**.

### Guest Satisfaction

Guest satisfaction was analyzed using only bookings that actually contained a guest rating.

The analysis included:

- Average rating by city
- Average rating by property
- Property-level rating vs occupancy correlation

The property-level correlation between average guest rating and occupancy was:

**r = 0.995**

This indicates a very strong positive association, but correlation alone does not establish causation.

---

## 📊 Visualizations

The project includes six required visualizations:

### 1. Occupancy % by City, Split by Room Class

A grouped bar chart comparing average occupancy across cities and room classes.

### 2. Weekly Occupancy Trend

A line chart showing the movement in average weekly occupancy across the available analysis period.

The data produced **14 ISO calendar weeks (Weeks 17–30)** rather than exactly 12 weeks.

### 3. Weekday vs Weekend Occupancy by City

A grouped bar chart comparing weekday and weekend occupancy for each city.

### 4. RevPAR by Property

A sorted horizontal bar chart showing RevPAR performance across the hotel properties.

### 5. Revenue by Booking Platform

A bar chart comparing realized revenue across the seven booking platforms/categories.

### 6. Realized Revenue Distribution by Hotel Category

A box plot showing the distribution, spread, and remaining extreme observations of realized revenue for hotel categories.

Each chart includes a title, labelled axes, and a business takeaway.

---

## 🔍 Key Findings

### 1. Significant Weekday–Weekend Occupancy Gap

Weekend occupancy was consistently higher than weekday occupancy across all four cities.

Weekend occupancy ranged from **71.46% to 78.05%**, compared with **50.06% to 54.65%** on weekdays.

This represents an occupancy gap of approximately **21–23 percentage points**, indicating substantially weaker weekday occupancy.

### 2. Occupancy Declined Over the Analysis Period

Average weekly occupancy declined from **79.41% in Week 17 to 51.59% in Week 30**, representing a decrease of approximately **27.82 percentage points**.

Although occupancy fluctuated from week to week, the overall pattern showed weaker occupancy toward the end of the analysis period.

### 3. Guest Ratings and Occupancy Show a Strong Association

Property-level average guest rating and occupancy showed a **very strong positive correlation of 0.995**.

Properties with higher average guest ratings tended to have higher occupancy.

However, this is an association rather than evidence that higher ratings directly cause higher occupancy.

---

## 💡 Business Recommendation

### Prioritize Weekday Demand

The analysis identified a **21–23 percentage-point gap between weekday and weekend occupancy across all four cities**.

Management should investigate weekday-focused commercial strategies such as:

- Corporate/business packages
- Weekday promotional offers
- Targeted booking-channel campaigns
- Partnerships targeting weekday demand

The effectiveness of these actions should be measured by whether they reduce the weekday occupancy gap over subsequent periods.

---

## 🔄 August Data Integration

The project also tests whether the analysis pipeline can absorb new monthly data without breaking the existing structure.

The August dataset was:

1. Compared against the existing aggregated booking structure.
2. Checked for matching and non-matching columns.
3. Reshaped into the structure required for the aggregated booking analysis.
4. Validated against `dim_hotels`.
5. Appended to the cleaned aggregated dataset.
6. Verified using a row-count check.

### August structure validation

The August dataset shared the following core fields with the aggregated booking data:

- `property_id`
- `check_in_date`
- `room_category`
- `successful_bookings`
- `capacity`

The August file also contained additional property, room, date, and derived fields.

The duplicated property attributes were checked against `dim_hotels` before the data was appended.

### Row-count verification

Before the append:

**9,194 rows**

August data:

**7 rows**

Expected combined total:

**9,201 rows**

The final row count was verified after appending.

---

## ⚠️ Data Limitations

The available data supports analysis of:

- Occupancy
- Revenue
- ADR
- RevPAR
- Realization
- Booking channels
- Cancellation rates
- Guest ratings
- Length of stay
- Property performance

However, some business questions cannot be answered reliably using the available data.

### Booking Channel Profitability

Revenue and booking volume alone do not show which channel is most profitable.

Additional data would be required, including:

- Booking-platform commission
- Customer acquisition cost
- Marketing spend
- Net revenue after channel fees

### Causes of Weekday Occupancy Weakness

The available data shows a substantial weekday/weekend occupancy difference, but it does not explain the underlying causes.

Additional information could include:

- Business vs leisure booking purpose
- Customer market or segment
- Competitor occupancy
- Competitor pricing
- Promotional campaigns
- Corporate contracts

### Guest Satisfaction Drivers

The dataset provides ratings but does not explain why guests gave those ratings.

Additional data could include:

- Review text
- Complaint records
- Service-quality indicators
- Property-level operational metrics

### Rating and Occupancy Relationship

The correlation between guest rating and occupancy is very strong (**r = 0.995**), but correlation does not establish causation.

Additional longitudinal or experimental data would be required to determine whether changes in guest satisfaction directly influence occupancy.

---

## 🛠️ Tools & Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Jupyter Notebook**

---

## 📁 Project Structure

```text
365_Hotels_Resort_Data_analysis/
│
├── README.md
├── 365_Hotels_Resort_Data_analysis.ipynb
├── requirements.txt
└── data/
    └── README.md
```

> Raw datasets are not included in the public repository where redistribution rights are unavailable.

---

## 📌 Skills Demonstrated

This project demonstrates practical experience in:

- Data cleaning
- Data validation
- Exploratory data analysis
- Hospitality analytics
- KPI calculation
- Revenue analysis
- Occupancy analysis
- Booking-channel analysis
- Statistical interpretation
- Correlation analysis
- Data visualization
- Data integration
- Business insight generation
- Management-level reporting
- Translating analytical results into actionable recommendations

---

## 👤 Author

### Muhammad Awais

**Data Analytics | Python | AI & Machine Learning**

GitHub: [Awais61926](https://github.com/Awais61926)

---

## ⭐ Project Purpose

This project was developed as a practical demonstration of how raw hotel booking data can be transformed into **structured analysis, meaningful business insights, and actionable recommendations** using Python.

The focus is not only on calculating metrics, but also on understanding **why the numbers matter for business decision-making**.
