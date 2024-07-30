# quickbooks_invoice_analysis

# Quickbooks Invoice Data Cleaning and Analysis Project

This project focuses on cleaning and preparing Quickbooks invoice data for subsequent analysis and integration with other datasets. The primary goal is to extract meaningful insights regarding sales trends, product performance, and customer behavior.

## Project Structure

*   **invoice_cleaner.py:** Python script containing data cleaning and transformation functions.
*   **data/raw:** Directory for storing the original, uncleaned invoice data.
*   **data/processed:** Directory for storing the cleaned and transformed data.

## Data Cleaning and Transformation Steps

1.  **Load Data:**
    *   Reads the raw invoice data from a CSV file (`invoice_data.csv`).
    *   Handles potential encoding issues by specifying 'cp1252' encoding, which is common for Quickbooks exports.

2.  **Clean Data (Function: `clean_data`):**
    *   Removes summary rows (containing 'Total') and header rows (containing 'Name') as they are not individual invoice records.
    *   Drops rows with all missing values (empty rows).
    *   Standardizes column names by removing extra spaces and replacing spaces with underscores to ensure consistency and easier manipulation in subsequent analysis.
    *   Renames the `Unnamed: 0` column to `Temp` as a placeholder and the `U/M` column to `U_M`, as the original names may not be consistent.
    *   Removes the temporary column `Temp`.
    *   Splits the DataFrame into `credit_memo` and `invoice` based on the `Type` column, as credit memos are treated differently from regular invoices.

3.  **Process Invoices (Function: `process_invoices`):**
    *   Reorders columns to move `Name` to the second position for better readability and consistency with other datasets.
    *   Renames `Num` to `Invoice_Number` for clarity.
    *   Drops unnecessary columns:
        -   `Type`:  Already used to split the data.
        -   `Amount`, `Balance`:  Likely calculated fields that can be derived later.
        -   `U_M`:  Not needed for the immediate analysis goals.
    *   Extracts descriptions within parentheses in the `Item` column and stores them in a new column `Description` to separate product IDs from additional details.
    *   Removes the parentheses and their contents from `Item` to leave only the product IDs.
    *   Filters out rows where the cleaned `Item` consists only of alphabetic characters (non-product items like fees or services).
    *   Splits the data into two DataFrames: one with numeric item tags (`invoices_with_tags`) and one without (`invoices_without_tags`).

4.  **Save Data (Function: `save_data`):**
    *   Saves the cleaned and filtered DataFrames into separate CSV files in the `data/processed/` directory:
        -   `credit_memo.csv`: Contains cleaned credit memos.
        -   `invoices_with_tags.csv`: Contains cleaned invoices with numeric item tags.
        -   `invoices_without_tags.csv`: Contains cleaned invoices without numeric item tags (these are typically not product sales).

## Future Work

*   Integrate inventory and purchase data using the cleaned invoice data.
*   Perform deeper analysis on sales trends, product performance, and customer behavior.
*   Build interactive dashboards using Power BI for data visualization.
*   Create a data pipeline to automate the cleaning and analysis process for new invoice data.

## Dependencies

*   pandas: For data manipulation and analysis.

## Usage

1.  Install pandas: `pip install pandas`
2.  Place your raw Quickbooks invoice data in the `data/raw` directory.
3.  Run the script: `python invoice_cleaner.py`
