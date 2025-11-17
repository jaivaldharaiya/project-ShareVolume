# SEC Shares Outstanding Viewer

## Summary

This is a single-page web application that fetches and displays public company data from the U.S. Securities and Exchange Commission (SEC) EDGAR API. Specifically, it retrieves a company's historical data for `EntityCommonStockSharesOutstanding`. The application then identifies and presents the highest and lowest share counts reported in annual filings (Form 10-K) for fiscal years after 2020.

The application loads with a default company (Altria, CIK 0000764180) and allows users to dynamically fetch data for any other company by providing its Central Index Key (CIK).

## Setup

This is a standalone static web application. No build process or server is required.

1.  Clone or download the repository.
2.  Open the `index.html` file in any modern web browser.

## Usage

*   **Default View:** On loading `index.html`, the application will automatically fetch and display the share data for Altria.
*   **Search for another Company:** To view data for a different company, enter its 10-digit CIK number into the input field at the bottom of the page and click the "Load Data" button or press Enter.
*   **Direct Link:** You can also link directly to a company's data by appending a CIK query parameter to the URL. For example: `index.html?CIK=0001018724` will load data for Amazon.com, Inc.

## Code Explanation

The project is contained within a single `index.html` file for simplicity.

*   **HTML:** The file provides the semantic structure for the application, including two main data cards for displaying the maximum and minimum share values, and a footer section for user input. Specific element IDs (e.g., `share-max-value`) are used as hooks for JavaScript manipulation.

*   **CSS:** All styling is handled by an embedded stylesheet within the `<style>` tag. It uses a modern approach with CSS variables for theming, ensuring a clean and responsive user interface.

*   **JavaScript:** The core logic is contained within an embedded `<script>` tag.
    *   **Data Fetching:** It uses the `fetch()` API to request data from the public SEC endpoint. A CORS proxy (`api.allorigins.win`) is used to overcome browser cross-origin restrictions when fetching data for user-specified CIKs.
    *   **Data Processing:** Upon receiving the JSON response, the script filters the data to include only annual reports (Form 10-K) from fiscal years 2021 and later. It then calculates the maximum and minimum share values from this filtered dataset.
    *   **DOM Manipulation:** The script dynamically updates the page title, header, and data cards with the processed information without requiring a page reload. It also handles loading states and potential API errors gracefully.
    *   **URL Handling:** The JavaScript reads the `CIK` query parameter from the URL on initial load and updates it via the History API when a new CIK is searched, allowing for shareable, direct links.

## License

This project is licensed under the MIT License.