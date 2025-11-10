# Revenue Performance Analysis

### 1. Introduction
This Power BI dashboard provides a comprehensive analysis of a business’s aggregated values over time, across regions, and by product type. Its interactive features allow stakeholders to explore trends in revenue, costs, and profit margins. 


# Dashboard
### Why This Dashboard is Useful?
This dashboard consolidates essential business metrics into one easy-to-use tool, offering multiple ways to view and compare financial data for smarter decision-making.

- Metric Selector (Total Costs, Total Profit, Total Revenue): Enables users to switch between key financial views with a single click, allowing comparison of patterns across        metrics. This compare patterns for one metric against the others.
- Year Filter: A dropdown in the top right to choose the year. Allows users to select a specific year, updating all visuals instantly to compare performance over time.
- Analyze Monthly Trends (Column Chart): Displays the selected metric (costs, profit, or revenue) month by month, helping to identify seasonality or shifts in performance.
- Compare Regional Performance (Horizontal Bar Chart): Highlights the total metric by continent, making it easier to detect underperforming or high-performing regions.
- Evaluate Product Categories (Pie Chart): Shows the share of each product category, assisting in identifying areas of strength or concern in the product portfolio.
- Drill Down into Subcategories (Treemap): Reveals which subcategories contribute most within each product category, supporting more granular analysis and strategy refinement.

##**How to use this dashboard for decision making:**
This Power BI dashboard enables decision-makers to make well-informed business choices by offering an interactive and comprehensive view of key financial metrics.

 - Track Performance Trends: Use the Monthly Time Series (Column Chart) to monitor costs, profits, and revenue on a monthly basis. Identify seasonality, growth opportunities, or     unexpected dips. Changing the year filter lets you compare these patterns across different periods.
 - Assess Regional Performance: Use the Regional Comparison (Horizontal Bar Chart) to highlight which continents are over- or under-performing. Focus on specific regions to          allocate resources or adjust strategies and boost profitability where it’s needed most.
 - Analyze Product Mix: Use the Product Category Breakdown (Pie Chart) and Subcategory Detail (Treemap) to pinpoint top-performing and lagging categories. Determine which product    lines deserve more investment or a marketing push.
 - Support Strategic Planning: Continuously monitor all visuals together to detect issues or opportunities early. Use these insights to refine pricing strategies, reallocate         budgets to high-impact regions, expand successful product lines, or optimize inventory and logistic.

### Example of Screenshot
Below is a screenshot of the Performance Summary of UK market in September
<img width="854" height="475" alt="image" src="https://github.com/user-attachments/assets/06b4b5ef-9d3a-429b-ba9c-ed14749ea899" />


### 2. Dataset and Key Measures Used
This dashboard integrates multiple datasets to offer a comprehensive and dynamic view of business performance, with the ability to track key financial metrics by region, product category, and subcategory.

#### Datasets Integrated into Power BI

| Dataset               | Description                                                                  |
| --------------------- | ---------------------------------------------------------------------------- |
| **Sales**                 | Contains transactional data, including revenue, units sold, and profit       |
| **Promotions**            | Includes promotion details, such as discount types and their impact on sales |
| **Geography**             | Provides regional and country-level location data                            |
| **Stores**                | Includes store-level information, such as name, location, and type           |
| **Products**              | Contains details about product names, IDs, and categories                    |
| **Product Categories**    | Defines the broader categories of products                                   |
| **Product Subcategories** | Provides more detailed segmentation of products                              |
| **Calendar**              | Enables time-based analysis through a complete date table                    |

#### Key Measures Calculated
* **Revenue:** Total sales revenue, calculated from the transactional data.
  
* **Revenue with Discount:** Revenue accounting for discounts applied during promotions.

* **Costs:** The total costs associated with products and transactions.

* **Returns:** Sales returns, showing the impact of returned products on overall performance.


#### Technical Features and Filters

* **Metric Buttons:** Users can dynamically select and view data for Costs, Profit, or Revenue, with the entire page updating accordingly.

* **Year Filter:** Allows users to filter the data by year, with all visualizations adjusting to the selected time period.

## 3. Key Insights and Business Implications

This dashboard provides interactive insights into revenue performance by region and product category for 2007. By using filters and dynamic visualizations, it allows stakeholders to explore revenue trends, analyze regional performance, and evaluate the impact of product categories and subcategories.

#### **A. Revenue Trends in 2007**

**Findings:**

* Revenue starts relatively low in January (\\$175M), gradually increases to peak in May (\\$280M).

* After May, revenue decreases, reaching a low point in September (\\$236M).

* October sees a recovery, rising to \\$276M, with a slight decline in November (\\$255M) and a smaller dip in December (\\$246M).

**Business Implications:**

The peak in May signals a potential opportunity for mid-year promotions or targeted campaigns. Identifying the factors behind this peak can help replicate the success for other months.

The dip from May to September suggests the need for strategies to maintain customer interest during slower months, such as limited-time offers, seasonal product launches, or targeted marketing.

The increase in October may indicate a resurgence in customer demand as the holiday season approaches. Early promotional campaigns and inventory planning will be key to capitalizing on this recovery.

The slight decrease in November and December suggests that post-holiday promotions or sustained engagement efforts can help smooth out revenue dips and maintain customer attention.

**How the Dashboard Helps:**

The Monthly Time Series chart highlights seasonal trends, enabling decision-makers to plan campaigns, promotional activities, and inventory management aligned with revenue fluctuations.

#### **B. Regional Performance Breakdown**

**Findings:**

* North America: $1.8 bn (64% of total revenue)

* Europe: $0.60 bn (21%)

* Asia: $0.40 bn (14%)

* Oceania: $0.02 bn (1%)

**Business Implications:**

North America remains the dominant market, accounting for more than 60% of revenue. While the region is key, the concentration in one market could pose a risk of over-dependence.

Europe and Asia offer significant growth potential and diversification opportunities. Strategies should be considered to strengthen the presence in these regions and reduce dependency on North America.

**How the Dashboard Helps:**

The Regional Comparison chart provides a clear visual comparison of revenue by region, helping inform decisions about expanding into underperforming or high-growth markets.

#### **C. Product Category and Subcategory Breakdown**

**Findings:**

Top Categories:

* Computers: $1 bn (36%)

* Cameras & Camcorders: $1 bn (35%)

* TV and Video: $0.39 bn (14.0%)

* Cell Phones: $0.33 bn (12.0%)

Low-performing Categories: Music, Movies & Games, Audio (less than 3% combined).

**Business Implications:**

Computers and Cameras & Camcorders together account for nearly 70% of revenue. These categories should be the focus of bundled promotions or cross-sell strategies to increase additional revenue opportunities.

Low-performing categories like Music, Movies & Games might benefit from a strategic review, considering adjustments to pricing or changes in the product portfolio.

**How the Dashboard Helps:**

The Product Category Breakdown (Pie Chart) highlights top-performing categories and enables decision-makers to easily identify products that require attention for a more effective marketing or sales strategy.

#### **D. Subcategory Focus**

**Findings:**

The highest-performing products within the top categories are related to Camcorders.

**Business Implications:**

Top-performing subcategories, like Camcorders, projectors and cameras should be the focus of targeted campaigns and promotions to maximize ROI and increase sales.

**How the Dashboard Helps:**

The Subcategory Detail (Treemap) allows easy identification of the best-performing subcategories, helping to decide where to focus efforts for maximizing profits.

#### **Executive Summary (2007 Revenue)**

* Total Revenue: $1.56 bn

* Highest-Earning Month: May ($280 M)

* Top Region: North America (64% of total revenue)

* Leading Product Categories: Computers + Cameras (71% of total revenue)

* Star Subcategory: Camcorders and Projectors

## 4. Business Recommendations

* **Mid-Year Promotions:** Leverage the peak in May by rolling out targeted campaigns, possibly focusing on key product categories like Computers and Cameras, which make up the bulk of revenue.

* **Seasonal Promotions:** Develop strategies to sustain sales through the dip from May to September, such as introducing time-sensitive offers, bundling products, or launching new products to keep customer interest high during slower months.

* **Holiday Season Strategy:** Plan ahead for October, when sales see a recovery, by aligning inventory, launching early holiday promotions, and optimizing digital marketing efforts to take full advantage of the increased demand leading into the holiday season.

* **Post-Holiday Engagement:** Address the slight revenue dip in November and December by introducing post-holiday promotions or loyalty programs to maintain customer attention and encourage repeat business.

* **Regional Focus:** Prioritize growth in underperforming regions like Asia and Europe while maintaining the strong position in North America. Consider tailored marketing campaigns or partnerships to expand market share in these regions.

## 5. Next Steps

* **In-depth Seasonal Analysis:** Evaluate the factors contributing to the peak in May to replicate success and identify promotional opportunities for other months.

* **Revenue Growth in Low-Performing Months:** Review strategies to boost performance during the dip from May to September, including new product introductions or aggressive discounting in slower months.

* **Cross-Sell and Bundle Promotions:** Focus on bundling Computers and Cameras to drive additional sales, as they represent the majority of revenue. Experiment with new cross-sell offers to maximize revenue per transaction.

* **International Expansion Strategy:** Explore expansion opportunities in Asia and Europe, leveraging the data to tailor product offerings and marketing strategies for these regions.

* **Monitor Regional Trends:** Use the regional breakdown to track the performance of markets over time and adjust strategies for better global diversification.

## 6. Conclusion:

The 2007 Revenue Dashboard provides valuable insights into seasonal trends, regional performance, and product category dynamics. By leveraging interactive filters, trend analysis, and market segmentation, stakeholders can optimize strategies, enhance marketing efforts, and drive revenue growth across North America, Europe, and Asia. This dashboard offers actionable insights for targeted promotions, regional expansion, and maximizing product category performance.

**For deeper exploration, download the Power BI report and explore the data yourself.**


