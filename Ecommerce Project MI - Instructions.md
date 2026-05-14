\# Mock interview page.  
In this page, you’ll find all the information needed for your mock-up Interview.

\#\# Dataset

\- For this interview, you will be working with the following dataset. Feel free to get acquainted with it.

\*\*Dataset:\*\* https://drive.google.com/drive/folders/1TIJfqQQxCaWGl\_wQJBU9khRvU8s1e-VV

\- Tables Metadata:  
      
    \*\*Sales table\*\*  
      
    The sales table keeps information about every sale including the product, the customer, and the amount.  
      
    \- \*\*Transaction Date\*\* – Date of purchase  
    \- \*\*Customer ID\*\* – Customer identifier  
    \- \*\*Description\*\* – Product description  
    \- \*\*Stock Code\*\* – Product code  
    \- \*\*Invoice No\*\* – An invoice contains multiple products and represents a single checkout  
    \- \*\*Quantity\*\* – Quantity of a product purchased  
    \- \*\*Sales\*\* – Total amount of a product in a single checkout  
    \- \*\*Unit Price\*\* – Unit price of a product  
      
    \---  
      
    \*\*State mapping\*\*  
      
    The state\_mapping table maps multiple variations of state code and descriptions to a standardized state code.  
      
    \- \*\*Order State\*\* – State code, description and all its variations  
    \- \*\*State\*\* – A standardized state code  
    \- \*\*Region\*\* – Region name  
      
    \---  
      
    \*\*Product table\*\*  
      
    The product table keeps description, landed and shipping cost, weight, and product category.  
      
    \- \*\*Stock Code\*\* – Product code  
    \- \*\*Weight\*\* – Weight of a single unit  
    \- \*\*Landed Cost\*\* – Manufacturer cost \+ freight  
    \- \*\*Shipping\_Cost\_1000\_r\*\* – Average cost of shipping 1000 miles to customers  
    \- \*\*Description\*\* – Most recent product description  
    \- \*\*Category\*\* – Product category  
      
    \---  
      
    \*\*Customer table\*\*  
      
    The customer table has customer identifier and their location information.  
      
    \- \*\*Customer ID\*\* – Customer unique identifier  
    \- \*\*Order City\*\* – City  
    \- \*\*Order Postal\*\* – Postal code  
    \- \*\*Order State\*\* – State  
    \- \*\*Latitude\*\* – Latitude of customer location  
    \- \*\*Longitude\*\* – Longitude of customer location

\-  Interview Objective:

    \- Analyze the shipping costs for the products. Compare a hypothesis shipping pricing to the baseline value.  
    \- Try to answer the question: How can we improve business profit based on the shipping of multiple items?  
    \- Note: All the calculations are based on the average cost of shipping 1000 miles to customers.  
      
\-  Steps to prepare:

    1\. Import the data to your preferred DBMS.  
    2\. Import to tableau and focus your analysis on shipping costs:  
        \- \*\*Baseline Shipping Assumption:\*\* Each additional unit in a shipment is estimated to incur approximately 70% of the cost required to ship that product individually. Calculate shipping costs based on the baseline assumption.  
        \- \*\*Hypothesis Analysis:\*\* This analysis involves a deeper dive into the data, allowing for a more detailed and granular examination of potential scenarios.  
            \- For this analysis, use the following hypothesis rules that were provided:  
                \- If \*\*Hypothesis Quantity\*\* is \*\*1 or less\*\*, the value is \*\*1\*\*.  
                \- If \*\*Hypothesis Quantity\*\* is \*\*2 or less\*\*, the value is \*\*0.8\*\*.  
                \- If \*\*Hypothesis Quantity\*\* is \*\*4 or less\*\*, the value is \*\*0.6\*\*.  
                \- If \*\*Hypothesis Quantity\*\* is \*\*7 or less\*\*, the value is \*\*0.5\*\*.  
                \- If \*\*Hypothesis Quantity\*\* is \*\*9 or less\*\*, the value is \*\*0.4\*\*.  
                \- For any other value greater than \*\*9\*\*, the value is \*\*0.3\*\*.  
            \- Calculate the shipping costs based on the hypothesis.  
    3\. Prepare the charts you think are useful to answer the objective question.