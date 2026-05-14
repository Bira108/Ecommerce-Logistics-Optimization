**SQL:**

### **1\. Context: The State of the CSV Files**

When you speak about the files, you want to highlight the **challenges** you overcame. This makes your work look more impressive.

* **The Issue:** The raw data was "dirty" and fragmented. Values in the `Order State` column didn't match across files (e.g., "WA" vs "Washington"), and the shipping costs were floating in a separate sheet without a direct link to the orders.  
* **The Choice of Metrics:** You chose **Key Alignment, Standardization,** and **Logic Transformation** because:  
  1. **Alignment** is required to join the data accurately.  
  2. **Standardization** ensures filters (like your State filter) actually work.  
  3. **Transformation** (The math) is where you turn raw data into "Business Intelligence."

### **2\. The SQL Presentation Guide**

*As you show your code on the screen, follow these three steps:*

**I. Relational Integrity & Key Alignment**

"Before the analysis, I had to ensure our tables could 'talk' to each other. I used **`TRIM`** and **`CAST`** on the Customer IDs and Stock Codes. This was vital because raw CSV data often imports with hidden spaces that cause joins to fail. By doing this, I ensured a 100% match rate between our Sales and our Products."

**II. Data Normalization (The 'State' Fix)**

"One of the biggest hurdles was geographic consistency. For example, Indiana was listed as **'IN.'** with a period. I wrote an **`UPDATE`** script using **`REPLACE`** to strip those characters and convert everything to **`UPPER`** case. I then used a **Mapping Table** (`dim_locations`) to bridge the gap between abbreviations and full state names, ensuring our Tableau map would be 100% accurate."

**III. The Business Intelligence View**

"Finally, I created a **SQL View** called `v_shipping_analysis`. Instead of just pulling raw data, I engineered the metrics directly into the view—calculating **Total Product Cost** and **Estimated Shipping** on the fly. This 'Pre-Aggregated' layer is what allows the Tableau dashboard to remain fast and responsive even as we add complex filters."

III. **Executive Summary (The "Why")**

"Before moving to Tableau, I used SQL to perform a high-level **Efficiency Audit**. I grouped our data by Region to calculate the **Shipping-Cost-Ratio**—which is essentially what percentage of our revenue is being eaten by shipping costs."

**The Insight:**

"This query confirmed our suspicion. We discovered a critical risk in the **Southern Region**. While we are generating revenue, our Shipping Cost Ratio is 65.36%.

 This 'Validation Query' gave me the confidence to move into Tableau, knowing exactly which geographical 'lever' we needed to pull to recover our profit."

---

### **3\. The "Transition" Line**

*Use this exact line to move from SQL to your Dashboard:*

**"Now that we have a clean, standardized, and high-performing dataset, I moved this into Tableau to visualize exactly where that profit is leaking and how we can fix it."**

---

**Tableau:**

## **The Strategic Guide**

### **I. The Introduction (Dashboard Title & Navigation)**

*Projecting Profit Recovery through Logistics Optimization*

* **The Hook:** "Today, we aren't just looking at where we are making money, but where we are losing it due to outdated logistics. Our current shipping model treats every item the same, which effectively 'penalizes' our bulk customers and long-distance regions."  
* **The Controls:** "I’ve included **Category** and **State** filters at the top. This allows us to see that while the company is overall profitable, specific pockets of the business are underperforming due to shipping costs."

### **II. The Problem: "Where" and "What"**

* **Geographic Profit Leakage (The Map):**   
  **The Insight:** "As we see on the map, profitability isn't uniform. While **Texas** is healthy at **$10K** in profit, **Washington** is currently in the red, showing a **$2,000 loss**. This 'leakage' is a direct result of shipping heavy items over long distances without a volume-based discount."  
* Notice that when we look at our overall logistics, the problem isn't national—it’s concentrated. Our analysis identified these **11 specific states** where our current shipping model is failing to keep us in the green. This allows us to target our 'Hypothesis Model' where it's needed most.   
    
* **Top Margin-Eroding Products (Top 5 Chart):**  
  **The Insight:** "If we look at our worst-performing products, we have one specific item responsible for a **$5,000 loss**. This confirms that it isn't a sales problem—we are selling the product—it's a logistics problem. We are spending more to ship these items than we are making in margin."

### **III. The Solution: "The Strategy Comparison"**

* **The Narrative:** "To fix this, we modeled two alternative shipping scenarios to see how we can recover that lost margin.  
* **The Comparison \- Net Profit Impact (The 3 Bars):**  
    
  1. **Current Net Profit ($250K):** "This is our 'as-is' state. It’s profitable, but inefficient."  
  2. **Baseline Assumption ($366K):** "By a flat 70% cost to additional units in an order, we immediately see a **$116K profit lift**."  
  3. **Hypothesis Model ($411K):** "This is my recommendation. It uses a **Tiered Multiplier** based on quantity. We charge 100% for the first item ($1.0$), but scale down to just 30% ($0.3$) for orders over 9 units. This captures the maximum logistical efficiency and brings our total profit to **$411K**."

On your Tableau Dashboard, use the Category Filter to select only WA, TX and SC, and only Electronics, Food, and Cat Food.

The total loss is 5K, 3K negative from WA, plus 2k of non-profit.  
If we implement our new mode, we immediately recover 3k from WA and give 2k profit back to TX.

### **IV. The Conclusion & Call to Action**

* **The Conclusion:** "By shifting from a flat shipping rate to this Volume-Based Tiered Model, we aren't just saving money; we are transforming our most unprofitable regions into growth opportunities. We can turn Washington's loss into a gain without changing our prices—just by optimizing how we ship."  
*   
* **The Call to Action:** "I recommend we pilot the **Hypothesis Model** starting with our heaviest product categories. This will deliver a **64% increase** in total net profit and stabilize our margins across the Western US."

—--------

\- For the hypothesis analysis, use the following hypothesis rules that were provided:  
    \- If \*\*Hypothesis Quantity\*\* is \*\*1 or less\*\*, the value is \*\*1\*\*.  
    \- If \*\*Hypothesis Quantity\*\* is \*\*2 or less\*\*, the value is \*\*0.8\*\*.  
    \- If \*\*Hypothesis Quantity\*\* is \*\*4 or less\*\*, the value is \*\*0.6\*\*.  
    \- If \*\*Hypothesis Quantity\*\* is \*\*7 or less\*\*, the value is \*\*0.5\*\*.  
    \- If \*\*Hypothesis Quantity\*\* is \*\*9 or less\*\*, the value is \*\*0.4\*\*.  
    \- For any other value greater than \*\*9\*\*, the value is \*\*0.3\*\*.  ( 70% )

To do this, I created a calculated field called Hypothesis Multiplier. I used an IF-ELSEIF statement to translate the business rules into logic. 

"The reason I built it this way is to model **Logistical Efficiency**. In real-world shipping, the first item in a box is the most expensive because it covers the 'base' cost of the packaging and labels. Each additional item added to that same box has a much lower incremental cost.

This multiplier allowed me to calculate a more realistic 'Hypothesis Profit' by rewarding high-volume orders with lower shipping rates, which is exactly how we recovered the $161K in profit shown in the final bar chart."

—-----------

"What was your data cleaning strategy?"

"I followed a Standardization and Enrichment strategy. First, I handled structural cleaning by trimming whitespace and casting IDs to correct data types to ensure join integrity. Second, I performed categorical cleaning to normalize city and state strings. Finally, I moved into Feature Engineering, where I derived the shipping and profit metrics necessary to answer the core business question."

—------------------------

Upload files  
Create tables  
Clean tables

Create3  metrics:

* Revenue per Order (Sales)  
* Product Cost (Landed Cost)  
* Estimated Shipping Cost (The "Real Math")

2 results:

* V\_shipping\_analysis query  
* Executive summary query

Data cleaning & modeling:

1\. Key Alignment & Integrity

* Type Casting: We converted Customer\_ID from Text to Integer. This was crucial because computers cannot join a "word" to a "number," even if they look the same.  
* Whitespace Removal (TRIM): We used TRIM() on Stock\_Code and Customer\_ID to delete hidden spaces that would have caused our joins to return zero results.  
* Referential Integrity Check: We performed a Gap Analysis (the "Audit" query) to find Sales records that didn't have a matching Customer or Location.

2\. Categorical Standardization

* Case Normalization (UPPER): We forced all Order\_City names to UPPERCASE. This prevented "Jackson" and "JACKSON" from being counted as two different cities in our final report.  
* String Cleaning (Punctuation): We used REPLACE to remove periods from state abbreviations (changing IN. to IN).  
* Mapping Expansion: We updated our dim\_locations lookup table to include missing states like Alabama (AL) and Wyoming (WY) so that no revenue was dropped during the join process.

3\. Business Logic Transformation

Feature Engineering: We didn't just use the columns we were given. We created new metrics:

* Total Product Cost: (Landed\_Cost \* Quantity)  
* Est. Shipping Cost: (Weight \* Shipping\_Cost\_1000\_mile \* Quantity)  
* Est. Net Profit: (Revenue \- Total\_Product\_Cost \- Est. Shipping\_Cost)

Semantic Layer Creation: We wrapped all this logic into a SQL View (v\_shipping\_analysis). This means a user (or Tableau) doesn't have to see the messy "raw" data—they only see the clean, calculated results.

