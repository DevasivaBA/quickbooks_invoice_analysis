# quickbooks_invoice_analysis

# Quickbooks Invoice Data Cleaning and Analysis Project

This project demonstrates data cleaning, manipulation, and standardization techniques using Python and Pandas on Quickbooks invoice data. The goal is to prepare the data for further analysis and integration with inventory and purchase data to gain insights into sales trends, pricing, and inventory management.

## Project Overview

The project is divided into the following phases:

1.  **Data Cleaning and Standardization (Invoice Data):**
    *   Load raw invoice data from a CSV file with 'cp1252' encoding.
    *   Handle missing values by dropping rows where all values are null.
    *   Extract and clean item descriptions using regular expressions.
    *   Filter out irrelevant rows (e.g., summary rows containing 'Total').
    *   Standardize column names by removing extra spaces and replacing spaces with underscores.
    *   Split data into separate DataFrames for credit memos and invoices.
    *   Further clean and standardize the invoice DataFrame by:
        *   Moving the 'Name' column to the second position.
        *   Renaming the 'Num' column to 'Invoice_Number'.
        *   Dropping unnecessary columns ('Type', 'Amount', 'Balance', 'U/M').
        *   Filtering out rows where the 'Item' column contains only alphabetic characters (product items).
        *   Filtering out rows where the 'Item' column does not contain numeric values (e.g., freight, fees).

2.  **Data Enrichment (Inventory Data):** (Upcoming)
    *   Merge cleaned invoice data with inventory data.
    *   Calculate additional metrics (e.g., profit margins, inventory age).

3.  **Data Integration (Purchase Data):** (Upcoming)
    *   Merge with purchase data to analyze costs and profitability.
    *   Identify trends in purchasing and pricing over time.

## Usage

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/DevasivaBA/quickbooks_invoice_analysis](https://github.com/DevasivaBA/quickbooks_invoice_analysis)
    ```

2.  **Install dependencies:**
    ```bash
    pip install pandas
    ```

3.  **Place your raw invoice data:**
    Put the `Sales by Customer Details.CSV` file in the `data/raw/` folder.

4.  **Run the script:**
    ```bash
    python invoice_cleaner.py
    ```

5.  **Find cleaned data:**
    *   The cleaned invoice data will be saved in `data/processed/cleaned_invoices.csv`.
    *   The invoice data without non-numeric item tags will be saved in `data/processed/invoices_without_item_tags.csv`.

## Key Challenges and Solutions

*   **Non-UTF-8 Encoding:** The raw data was encoded in cp1252, requiring explicit encoding specification during loading.
*   **Inconsistent Formatting:** The data contained summary rows and inconsistent column names, which were addressed through filtering and renaming.
*   **Item Descriptions:** Item descriptions included additional information within parentheses, which was extracted and cleaned using regular expressions.
*   **Non-Product Items:** Rows with non-numeric item tags (e.g., freight, fees) were filtered out to focus on product sales.

## Future Work

*   Integrate inventory and purchase data to gain deeper insights.
*   Develop interactive dashboards using Power BI to visualize the cleaned and enriched data.
*   Implement automated data pipelines for regular updates and analysis.
