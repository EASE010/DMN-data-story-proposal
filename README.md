_This document is created by Levi Jiang in February 2026 for the reference of The Dallas Morning News' data story pitch_

## Task 1
### Questions for the Reporter
- The records available for inquiry on the website are cases scheduled for hearing between 2023 and 2025. Are you seeking cases that occurred during this period or cases that were scheduled for hearing?
- What story you're going to tell? What are you hoping to find from these cases? Are you looking for patterns or trends (race, sex, charges, regions)?
- Is there a specific concern (racial disparities, backlog, certain offenses, court delays)?
- From an ethical perspective, we should discuss the use of personally identifiable information, like names and addresses, how race data would be processed, and whether any records may involve sensitive or sealed cases.

### Three Technical Checks
- Inspect the page to see how the table is loaded, checking whether the data exists directly in an HTML div, is retrieved through background API, or is rendered dynamically via JavaScript.
- Check the site’s robots.txt file or other terms of use to determine whether automated scraping is permitted and whether specific sections are restricted.
- Check the page load speed and if there's blocking after repeated requests. It can help determine whether we can use auto scrapping to pull all the data at once or need some throttling.

### Ethical or Legal Considerations
- Is this dataset intended for public use? Does the site restrict automated access?
- Name, race, sex and home address are all sensitive personal data. Will this expose people to harm or harassment?
- Are we considering the invisible enforcement patterns, policing bias and socioeconomic disparities behind all these data?
- For some special cases, like domestic violence and minors involved cases, how should we make sure we're not invading privacy and protect the vulnerable people?

### Alternative Method
- Look for other download options (downloadable CSV/Excel/PDF) or APIs
- Check some other source website like Texas Open Data Portal
- Contact some government agencies like the court administration office for help
- File a public records request
- (If AI is permitted in our newsroom for data collecting) Use screen recording or screenshot to capture entire webpages, then use AI to transform them into datasets
- Ask some researchers and legal nonprofits for available materials

### Scrapping Tools and Methods
- If the table loads via background requests, usually we can find an endpoint returning HTML or JSON. I can use Python `requests` to replicate these calls across the desired years and months, and clean them up with `pandas`.
- Pseudo code:
```
for year in [2023, 2024, 2025]:
    for month in all_months:
        request data for Dallas County Grand Jury Cases Scheduled Report
        parse table rows
        clean column names
        append to our dataset

standardize dates and text fields
check duplicates and errors
export to CSV
```

## Task 2
### Steps to Assess Strength and Weaknesses
- I will get an overall understanding of the dataset first. I will read the column definitions carefully, and pull out some rows to see if they align with the definition, and whether each row reflects an individual contribution, credit, or other transaction type and how amounts should be interpreted. I will also try to download available files to see what format is used here. I aim to understand what each record represents and how reliable the fields are for analysis.
- The second step is to assess completeness and coverage by checking date ranges, records by candidate, and the prevalence of missing values in key fields such as amount, donor name, business name, and address. This will identify temporal gaps, underreported candidates, or structural bias in the data.
- Then we can evaluate data quality in some columns like contribution amounts, dates, and contributor identifiers, looking for formatting issues, missing values or inconsistencies. Also, since the dataset includes geo info, I will check how complete and accurate it is to determine whether location-based analysis can be applied here.
- Clarify the dataset’s scope and limitations, such as whether it includes only itemized contributions, how non-cash transactions are recorded, and what reporting thresholds may affect the coverage.

### Strength
- **Data Transparency and Credibility**: IIn each record, there's a direct link to original PDFs so reporters can pull context and verify the data easily. Readers also can benefit from the accessibility of primary sources.
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

## Task 3
Overall thinking: When working with a colleague from a non-tech background, I'd like to make sure:
1. Raw data is in a separate folder and never overwritten so they can do fact-checking
2. Analysis is traceable step-by-step so it's clear to identify any mistakes
3. If they are not familiar with running a code or a program, then they should be able to verify numbers without running code

I will use a GitHub repo to store all the files they need. Here's the structure:
```
Story/
│
├── README.md
│
├── 01_raw_data/
│   ├── source_original.csv
│   ├── data_dictionary.md
│   └── sources_notes.md
│
├── 02_analysis/
│   ├── 01_data_cleaning.ipynb
│   └── 02_calculations_results.ipynb
│
├── 03_outputs/
│   ├── cleaned_data/
│   │   ├── cleaned_dataset.csv
│   │   └── cleaned_data_notes.md
│   │
│   ├── story_numbers/
│   │   └── story_numbers_notes.md
│   │
│   └── charts_preview/
│       ├── chart_1.png
│       ├── chart_2.png
│       └── chart_notes.md
│
├── 04_multimedia_assets/
│   ├── photos/
│   ├── graphics/
│   └── videos/
│
└── methodology.md

```
### Breakdown of the files:
```
README.md
```
I will include a clear README explaining the story context, folder structure, data sources, and where to find the exact numbers used in the article for fact-checking

```
├── 01_raw_data/
│   ├── source_original.csv
│   ├── data_dictionary.md
│   └── sources_notes.md
```
This folder contains the original data files, a short data dictionary explaining every variable, and a source note documenting where each dataset came from, access dates, etc.

```
├── 02_analysis/
│   ├── 01_data_cleaning.ipynb
│   └── 02_calculations_results.ipynb
```
So for people with no coding experience, running a whole Python project can be very tricky. Instead, I will choose to do my data analysis works in Jupyter notebook. This is where I can combine narrative + code together in a step-by-step logic, and show my editor the visible output without running anything. I prefer to split data cleaning and computation into two separate files to avoid the issue of a single file becoming too large to pinpoint a specific step. Within each file, I will write explanations before and after major steps, describing in plain language what is going on and what each output represents. This allows editors to follow the logic without reading the code.

```
├── 03_outputs/
│   ├── cleaned_data/
│   │   ├── cleaned_dataset.csv
│   │   └── cleaned_data_notes.md
│   │
│   ├── story_numbers/
│   │   └── story_numbers_notes.md
│   │
│   └── charts_preview/
│       ├── chart_1.png
│       ├── chart_2.png
│       └── chart_notes.md
```
Here, `cleaned_data/` is the folder of all the datasets after processing and explaining notes. `story_numbers_notes.md` is where I track down all the numbers that are used in the story and where they came from, so editors can double check if they appears in the right place and if they're accurate. `charts_preview/` has the static PNGs or screenshots of our data viz so editors can quickly review them. With the `chart_notes.md`, graphics team can rebuild these charts.

```
├── 04_multimedia_assets/
│   ├── photos/
│   ├── graphics/
│   └── videos/
```
This is where we store all multimedia assets except the data viz. Editors can review visual elements here and verify information such as credits and captions.

```
methodology.md
```
If this is a large and complex project, I will also add a methodology file for our assumptions, cleaning decisions, calculations, etc.
