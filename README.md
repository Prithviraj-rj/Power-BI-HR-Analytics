# Power-BI-HR-Analytics
A freelance project delivering a Power BI dashboard to analyze employee attendance, WFH, and sick leave trends. Features a dynamic Power Query pipeline to transform complex Excel data.
# Freelance Project: HR Analytics Dashboard for a Tech Agency

## Project Title
**HR Insights Dashboard for a Software Development Agency**

## Problem Statement / Business Context
As a freelance data analyst, I was commissioned by a software development agency to solve a critical inefficiency in their HR operations. The agency's HR Manager was reliant on manual analysis of monthly attendance data stored in disparate Excel sheets. This process was time-consuming, prone to errors, and failed to provide the strategic insights needed to manage their roster of developers effectively. The raw data was in a pivoted format (dates as columns), making traditional analysis extremely difficult.

*Raw Data Snippet: The challenge was to transform this pivoted, multi-sheet format into a usable dataset.*
![Raw Data Format](https://i.imgur.com/kS94Epl.png)

## Objective / Goal
The primary objective of this freelance engagement was to design and build a fully automated, interactive Power BI dashboard to replace the client's manual reporting process. The goals were to:
*   Develop a dynamic and scalable solution to ingest and consolidate attendance data from multiple Excel sheets.
*   Provide the client with at-a-glance KPIs for key metrics: **Presence %**, **Work-From-Home (WFH) %**, and **Sick Leave (SL) %**.
*   Analyze attendance trends over time and identify patterns by day of the week.
*   Empower the HR Manager with a self-service tool to drill down into employee-level data without needing technical assistance.
*   Deliver actionable insights for strategic planning around office capacity, team events, and potential employee health concerns.

## Tools & Technologies Used
*   **Data Source:** Microsoft Excel
*   **Data Extraction, Transformation & Modeling:** Power Query
*   **Data Analysis & Calculations:** DAX (Data Analysis Expressions)
*   **Data Visualization:** Power BI Desktop

## Data Sources
The primary data source was a real-world (but anonymized) attendance file provided by the client, spanning three months.

*   **Attendance Data:** Provided in an Excel workbook with each month on a separate sheet (`April 2022`, `May 2022`, etc.).
*   **ID Map:** A separate sheet mapping anonymized employee IDs to names.
*   **Attendance Key:** A legend defining the codes used in the attendance sheets (e.g., P, WFH, SL, HSL). This was used to create the calculation logic.

![Attendance Key Logic](https://i.imgur.com/39sQ2tP.png)

## Methodology / Process

#### 1. Data Cleaning & Transformation (Power Query)
This phase was critical due to the complex data structure. I engineered a solution designed to be dynamic and scalable for the client's future needs.
*   **Dynamic Data Ingestion:** Instead of manually combining sheets, I built a custom Power Query function that takes a worksheet as input and performs all necessary transformations automatically.
*   **Unpivoting Data:** The core transformation step was **unpivoting** the date columns. This converted the client's wide, pivoted table into a clean, tabular format with one row per employee per day, creating dedicated `Date` and `Attendance Status` columns.
*   **Custom Function Creation:** I encapsulated the entire transformation logic into a reusable function that could be invoked on all attendance sheets, ensuring consistency and a zero-maintenance-effort solution for the client.
*   **Error Handling & Data Cleansing:** I built in dynamic error handling for data type conversions to ensure the pipeline was robust and would not fail with future data.
*   **Optimized Model:** I disabled the 'load' option for staging queries to keep the final data model lean and performant for the end-user.

#### 2. Data Modeling & DAX Measures
*   **Centralized Logic:** A dedicated 'Measure Table' was created in DAX to house all calculations—a best practice that makes the model easy for the client or another analyst to maintain.
*   **Calculated Columns:** Created new columns using DAX for `Day of Week` and `Start of Month` to enable time-based and pattern analysis.
*   **Core Measures:** Developed key DAX measures to power the dashboard visuals:
    *   `Total Working Days`: Calculated by counting all days, excluding holidays and weekly-offs.
    *   `Presence %`: `(Days Present + WFH Days) / Total Working Days`
    *   `WFH %`: `WFH Days / (Days Present + WFH Days)`
    *   `Sick Leave %`: `Sick Leave Days / Total Working Days`
    *   The logic correctly handled half-day leaves (`HSL`, `HWFH`) by assigning them a value of 0.5.

#### 3. Dashboard Design & Visualization
I designed the dashboard for clarity and intuitive use, ensuring the client could get answers to their most pressing questions immediately.
*   **KPI Cards:** Prominently displayed the three core metrics (Presence %, WFH %, SL %) at the top.
*   **Trend Analysis:** Area charts were used to visualize trends for each KPI over the three-month period.
*   **Day-of-Week Analysis:** Bar charts effectively revealed which days had the highest presence and WFH rates.
*   **Drill-Down Capability:** Included a table of all employees with their individual KPIs and a detailed matrix visual at the bottom that shows the raw attendance record for any selected employee, allowing the HR manager to investigate specific cases independently.
*   **Interactivity:** Month slicers were added to allow stakeholders to easily filter the entire dashboard view.

## Key Insights or Results
The final dashboard delivered immediate, data-driven insights that provided significant value to the client:
*   **Work-From-Home Behavior:** The highest rates of WFH occur on **Thursdays and Fridays**, while the highest in-office presence is on **Tuesdays**. This provided the client with critical information for planning in-office events and developing an official hybrid work policy.
*   **Overall Trends:** A slight decline in overall presence and a corresponding increase in WFH and sick leaves were observed from April to June, prompting a review of employee workload and wellness initiatives.
*   **Actionable Data:** The HR Manager can now identify employees with low presence or high sick leave percentages with a single click, enabling proactive and supportive communication.

## Dashboard or Model Output

![HR Insights Dashboard](https://i.imgur.com/3wYq1uD.png)

## How to Run / Use
1.  Clone or download this repository.
2.  Ensure you have Microsoft Power BI Desktop installed.
3.  Place the `HR_Attendance_Data.xlsx` file in the `data/` subfolder.
4.  Open the `HR Insights Dashboard.pbix` file.
5.  If prompted, update the data source path to point to the location of the Excel file on your machine.
6.  Click "Refresh" on the Home ribbon to load the data and interact with the dashboard.

## Future Scope / Improvements
As part of my project delivery, I provided the client with a roadmap for future enhancements:
*   **Automated Data Refresh:** Connect the report to a centralized location like SharePoint or a cloud drive for fully automated refreshes.
*   **Proactive Alerting:** Configure Power BI alerts to automatically notify the HR Manager if a key metric crosses a certain threshold (e.g., if overall sick leave exceeds a target percentage).
*   **Row-Level Security (RLS):** Implement RLS for future phases to allow managers to see data only for their direct reports.
