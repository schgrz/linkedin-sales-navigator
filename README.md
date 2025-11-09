# LinkedIn Sales Navigator Reporting

*Please Note: The reports, analysis, and generated modeling output differ due to [sdv](https://sdv.dev/) data anonymization providing different patterns for features and fields within the randomized output files*

*I will discuss actual findings and the process for this analysis*

*Data was synthesized based on similar patterns and provided to exemplify a working process*

## Project Overview

This project is meant to provide a simple time-series analysis using LinkedIn Sales Navigator reporting data for a few purposes:
1. To track Social Selling Index scores and provide an output summary for our team to visualize their performance over time
2. To understand what features lead to higher SSI Scores so we can coach our employees on better social media presence with the intention of increasing community engagement, boosting program sentiment, and leading to higher sales performance.

The problem this method solves is creating consistent reports and report outputs while saving monthly processing time. This notebook saved time in manual data entry, manual aggregation, and other related manual processing for repeated work while allowing the ability to train, re-train, and re-test models as new data is added to understand if the most important features remain the same over time.

The reason this is important is because the company pays for this tool. In order to make sure this tool is worth the investment, it needs to be utilized to the full potential. Running an analysis can let us gain insight into how it's currently being used and ways to improve its efficacy. Further research can be done to track direct results to revenue, however additional data and technological support is needed.

## Datasets

*Reminder: The datasets supplied in this project folder have been anonymized to protect personally identifiable information (PII) and maintain business confidentiality.*

The datasets are an output of totals. Some are aggregated during the 1-month period, some are account-life aggregated totals for each employee.

**Fields**
* Category *(Region)*
* Name
* Invited Email Address *(Email Address)*
* Current Seat Type *(Team Member Role)*
* Sales License Current Status *(At the time of reporting)*
* Date Invited
* Date Activated
* Seat ID
* Coach Level *(LinkedIn User "Level")*
* Days Active *(During the month)*
* Searches Performed *(During the month)*
* Total Leads Saved	*(During the month)*
* Accounts Saved *(During the month)*
* Total Accounts Saved *(Lifetime)*
* Total Lists Created *(Lifetime)*
* InMails Sent *(During the month)*
* InMails Acceptance Rate *(During the month)*
* Messages Sent *(During the month)*
* Smart Links Created *(During the month)*
* Smart Link Views *(During the month)*
* Total Connections *(Lifetime)*
* Connection Requests Accepted *(During the month)*
* SSI - Overall Score *(Score out of 100 - made up of the following 4 SSI Categories)*
* SSI - Establish your professional brand *(Score out of 25)*
* SSI - Find the right people *(Score out of 25)*
* SSI - Engage with insights *(Score out of 25)*
* SSI - Build relationships *(Score out of 25)*

## Methodology
1. **Data loading, cleaning, and preprocessing**
    - Imported and merged all files into a single dataset using pandas
    - Extracted date from file name to serve as report date field
    - Created Regional Vice President mapping by region
    - Removed old employees and fixed inconsistent employee names
    - Created pivot table summarizing SSI Scores by month
    - Created pivot table outlining pulling the most recent value for the Coach Level 

2. **Report Exporting**
    - Exported reports to .xlsx -> This is later copied and pasted into a Google Sheets dashboard for presentation to our employees and upper management

3. **Modeling / Analysis**
    - Split the data into X, y by selecting the relevant columns that made sense within the context of this problem. X and y were then split into an 80/20 Train/Test split for model evaluation *(sklearn train_test_split)*
    - Utilized a pipeline approach *(sklearn pipeline)* to train, tune, and evaluate different modeling methods including
        * linear regression
        * ridge regression
        * lasso regression
        * elasticnet regression
        * decision tree regressor
        * random forest regressor
        * XGBoost regressor
        * histgradientboosting regressor
        * k-nearest neighbors regressor
    - Evaluated best model using 5-fold cross validation using best R2 score
    - Fit the model using the best found model and hyperparameters
    - Ran permutation importance to determine which features contributed the most to the SSI Score
    - Findings were additionally understood with partial dependence plots to show HOW the top features contributed
    - Additional analysis was added as (within the real dataset) it was found that simply logging in was impactful in increasing SSI Score

## Findings
*(Running this report with the included data will provide different results from our actual findings)*

**Reporting**

The reporting uncovered granular person-by-person trends and allowed us to see if a user score decreased from month to month. This lets each employee track their own performance to manage themselves for self accountability and lets managers review their performance for additional accountability.

**Modeling / Analysis**

The social selling index is made up of 4 categories:

* **ESTABLISH your professional brand:** Complete your profile with the customer in mind. Become a thought-leader by publishing meaningful posts.
* **FIND the right people:** Identify better prospects in less time using efficient search and research tools.
* **ENGAGE with insights:** Discover and share conversation-worthy updates to create and grow relationships.
* **BUILD relationships:** Strengthen your network by connecting and establishing trust with decision makers.

This analysis uncovered a trend that for our employees, the most important features were:
1. Days Active
2. Total Leads Saved
3. Total Lists Saved
4. Total Accounts Saved
5. Profile Views

Days Active outscored Total Leads Saved by about 2x. While it's inferred that someone may have a higher score by just showing up, the implication of being active is that individuals who are active on the platform also engage in actions that lead to higher scores of social selling index from the four categories. The biggest correlation between users with higher scores is simply logging in and being active. From our group, generally, users who regularly log in and are active 15 days or more in a given month have a 39% (15.4 Point) higher average SSI Score than those who log in less than 15 days. 

Logging in is just the first step, but does lead to good habits like:
* engaging with communities
* connecting with people
* posting and providing insights or feedback
* sharing highlights about the program
* or even supporting clients or colleagues by spotlighting their successes or promoting their initiatives

This conclusion led to the first steps for our employees to understand how they might be able to increase their scores and for our managers to encourage their teams to log in more frequently. 

Since this was initial insight, the next steps would be to gather additional datapoints to report on and to see if SSI Scores change going forward while recording if and how managers are applying treatment (increased encouragement to log in more frequently). The result *should* be higher SSI Scores. Further analysis can be done by tracking or tying specific revenue to the platform to determine if the platform is worth it from a revenue generating perspective.

## Technology & Tools

- **Languages:** Python
- **Libraries:** pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn, datetime, os
- **Other Tools:** Jupyter Notebook, GitHub, VS Code

## How to Reproduce

1. Clone the repository:  
   ```bash
   git clone https://github.com/schgrz/linkedin-sales-navigator.git
2. **Initialize a virtual environment** (Python 3.12 or higher)

   ```bash
   python -m venv .venv
   source .venv/bin/activate # Mac/Linux
   .venv\Scripts\activate # Windows
   ```
3. **Install dependencies**

   ```bash
   python -m pip install -r requirements.txt
   ```
4. **Verify folder structure**

   ```
   LinkedIn Sales Navigator (Working Directory)
   ├── data/                     # contains raw and processed datasets
   ├── reporting/                # contains generated reports and visual outputs
   └── 2025_Sales_Navigator_reporting.ipynb
   ```
5. **Run the notebook**
    1. Open `2025_Sales_Navigator_reporting.ipynb` in Jupyter Notebook or VS Code.  
    2. Execute all cells to reproduce the analysis, modeling, and visualizations.

## Contact
- Email: alex.schwarzgrzesiak@gmail.com
- LinkedIn: [linkedin.com/in/schwarzalex](https://www.linkedin.com/in/schwarzalex/)
- Portfolio: [github.com/schgrz](https://github.com/schgrz)