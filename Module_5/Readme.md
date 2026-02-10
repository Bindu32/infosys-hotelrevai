# Hotel Revenue Strategy Dashboard

A Power BI dashboard for hotel revenue optimization, pricing strategy, and upsell analysis.

## Overview

This interactive dashboard helps hotel managers:
- Identify upsell opportunities
- Optimize pricing by season and room type
- Track performance across properties
- Compare forecast vs actual revenue

## Features

- **Upsell Analysis**: Track special requests, meal plan adoption, and estimated upsell revenue
- **Pricing Optimization**: Seasonal recommendations and dynamic pricing strategies
- **Performance Metrics**: YoY growth, segment profitability, and hotel comparisons
- **Interactive Filters**: By hotel, date range, market segment, room category, and season

## Key Metrics

- Total Revenue with Upsell: **$462.58K**
- Optimal Price Point: **$283.48**
- Segment Profitability Index: **97.23**
- Estimated Upsell Revenue: **$191.52K**
- YoY Revenue Growth: **56%**

## Data Model

**Main Tables:**
- `Raw_Fact` - Booking transactions with revenue, ADR, meal plans, special requests
- `date-dimension` - Calendar with seasons
- `hotel-dimension` - Hotel properties
- `room-dimension` - Room categories
- `Customer-dimension` - Guest information

## Technologies

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Power Query

## Getting Started

1. Download `Hotel_Group_Project.pbix`
2. Open in Power BI Desktop
3. Click **Refresh** to load data
4. Navigate to "Revenue Strategy Analysis" page

## Usage

**Filters Available:**
- Market Segment (Online TA, Direct, Corporate, Groups, etc.)
- Hotel (City Hotel, Resort Hotel)
- Arrival Date (custom date ranges)
- Season (Peak, Shoulder, Low)
- Room Category (Deluxe, Standard, Economy, Suite)

Click on any visual to filter other elements. Hover for detailed tooltips.

## Sample DAX Measures

**Estimated Upsell Revenue:**
```dax
Estimated Upsell Revenue = 
VAR MealUpsell = [Meal Upsell Revenue]
VAR SpecialRequestsUpsell = SUMX(Raw_Fact, Raw_Fact[total_of_special_requests] * 15)
RETURN MealUpsell + SpecialRequestsUpsell
```

**Optimal Price Point:**
```dax
Optimal Price Point = 
VAR CurrentOccupancy = [Occupancy %]
VAR CurrentADR = [ADR(Avg Daily Rate)]
VAR PriceAdjustment = 
    SWITCH(TRUE(),
        CurrentOccupancy >= 85, 1.15,
        CurrentOccupancy >= 70, 1.05,
        CurrentOccupancy >= 50, 1.00,
        CurrentOccupancy >= 40, 0.95,
        0.85)
RETURN CurrentADR * PriceAdjustment
```

## Dashboard Sections

1. **Upsell & Engagement**: Special request rates, meal plan trends, revenue breakdown
2. **Pricing Strategy**: Seasonal recommendations, ADR analysis, discount tracking
3. **Performance Analytics**: Hotel comparison, segment profitability, YoY growth
