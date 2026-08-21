_This document is created by Levi Jiang in February 2026 for the reference of The Dallas Morning News' data story pitch_

## Task
A beat reporter needs a list of Dallas city council members and the campaign finance data. The reporter does not have a clear pitch or idea, and is essentially on a “fishing expedition.” City council members: Eric Johnson, Chad West, Jesse Moreno, Zarin Gracey, Maxie Johnson, Jaime Resendez, Laura Cadena, Adam Bazaldua, Lorie Blair, Paula Blackmon, Kathy Stewart, William Roth or Bill Roth, Cara Mendelsohn, Gay Donnell Willis, Paul Ridley. 
Please prepare a dataset and a memo that touches on: 1. What are the first steps you would take to assess the dataset’s strength and weaknesses? 2. What are the strengths and weaknesses of this dataset? 3. What are some possible angles/potential data stories you would pitch based on your initial assessment?

### Dallas City Hall Campaign Finance Data
The public record could be found on [City of Dallas official website](https://campfin.dallascityhall.com/search.aspx). Set the searching time as 2026, then you'll get the full records.


### Steps to Assess Strength and Weaknesses
- I will get an overall understanding of the dataset first. I will read the column definitions carefully, and pull out some rows to see if they align with the definition, and whether each row reflects an individual contribution, credit, or other transaction type and how amounts should be interpreted. I will also try to download available files to see what format is used here. I aim to understand what each record represents and how reliable the fields are for analysis.
- The second step is to assess completeness and coverage by checking date ranges, records by candidate, and the prevalence of missing values in key fields such as amount, donor name, business name, and address. This will identify temporal gaps, underreported candidates, or structural bias in the data.
- Then we can evaluate data quality in some columns like contribution amounts, dates, and contributor identifiers, looking for formatting issues, missing values or inconsistencies. Also, since the dataset includes geo info, I will check how complete and accurate it is to determine whether location-based analysis can be applied here.
- Clarify the dataset’s scope and limitations, such as whether it includes only itemized contributions, how non-cash transactions are recorded, and what reporting thresholds may affect the coverage.

### Strength
- **Data Transparency and Credibility**: In each record, there's a direct link to original PDFs so reporters can pull context and verify the data easily. Readers also can benefit from the accessibility of primary sources.
- **Geographic Info**: With the address and geo_location info, we are able to analyze the money a candidate spent on local or out-of-state business. 
- **Transaction-level Detail**: Each row appears to represent an individual contribution or transaction with amount, time, location, etc. We are able to track the money over time, aggregate by candidate, identify any time or location-based patterns and compare them. This is stronger than summary-level reports.


### Weakness
- **Formatting Problem**: In the Amount column, the amount should be numeric instead of text. This will cost us some time to clean them up and double-check the numbers and potential calculation errors.
- **Spelling Inconsistency**: For example, for candidate William Roth, his name is spelled in 3 different ways in this dataset: Bill Roth, William Roth and WILLIAM ROTH. This might cause double-counting or grouping in our analysis. We have to check all of the candidates and do some manual standardizations.
- **Lack of Details**: After carefully reviewing several campaign finance reports, I noticed that the dataset still lacks certain details. For instance, the reports clearly disclose the purpose of each expenditure, but the dataset only lists a vague term like “Expenditure.” If we only look at the dataset, we cannot tell whether a candidate spent $1,000 at Walmart for lobbying or simply buying office supplies.

### Possible Angles/Potential Stories
1. **Does advantage in fundraising lead to a council seat** - We can analyze the total donations, donation size distributions and frequency of large donors by candidate to see if the incumbent City Council members received more donations and other financial support than their competitors.
2. **The political finance network** - We can find out all the people or business that funded or received money from multiple council members. Our analysis here is limited to politics related financial transactions; routine office supply purchases and food expenses are not included in this discussion. This will enable us to uncover the network between Dallas's political and business worlds, revealing which stakeholders are pulling the strings behind the city's power structure.
3. **Where are campaign money from or going to (local vs outside Dallas)** - With the geo info, we can look into whether a council member's financial transactions happened mainly in their communities or around outside interests. We might find something interesting in the comparison of Dallas vs non-Dallas, Texas vs out-of-state, and other geographic concentrations.
