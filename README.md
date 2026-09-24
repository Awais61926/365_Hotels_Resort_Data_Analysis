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

Several data-quality issues were investigated and addressed rather than blindly removing unusual records.

### Cleaning decisions included:

- Missing hotel capacity values were investigated and filled using consistent property/room information.
- Missing guest ratings were investigated by booking status rather than replacing them with a mean.
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

The analysis calculates several hospitality performance metrics:

### Occupancy %

```text
Occupancy = Successful Bookings / Capacity × 100
