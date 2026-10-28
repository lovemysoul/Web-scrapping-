# University of Kerala – Affiliated Colleges Web Scraping Project

A Python notebook that scrapes the public affiliated-colleges directory of the University of Kerala, collects contact details for every college, enriches the data, validates it, explores it with charts, and exports a final cleaned CSV.

**Notebook:** `Web_Scraping_Project_clean.ipynb`
**Source:** https://www.keralauniversity.ac.in/affiliated-colleges

---

## What the project does

| Step | What happens |
|------|--------------|
| 1. Fetch | Downloads the directory page and parses the HTML with BeautifulSoup |
| 2. IDs | Extracts each college's name and internal college ID (204 colleges) |
| 3. Scrape | Sends a POST request per college to its details page and extracts address, phone number(s), email and website |
| 4. Enrich | Adds district, establishment year and college type from the directory page and merges them using the college ID |
| 5. Validate | Checks email format and phone-number length |
| 6. EDA | Missing-value analysis and charts for contact completeness and college type, plus a district summary |
| 7. Findings | Written interpretation and recommendations |
| 8. Export | Trims whitespace, converts blanks to missing values, removes duplicates, and saves the final CSV |

---

## Dataset

The final dataset has **204 rows and 10 columns**:

`College Name`, `College ID`, `Address`, `Contact Number`, `Email Address`, `Website URL`, `Status`, `District`, `Establishment Year`, `College Type`

### Key results

- Scraping succeeded for **191** colleges. **13** colleges had no contact section on their details page.
- Missing values: Address 67, Website URL 31, Email 26, Contact Number 13, and 8 each for District, Establishment Year and College Type.
- College types: Self Financing 126, Aided 46, Government 19, Government Self Financing 3, Autonomous 2, not recorded 8.
- Districts: Thiruvananthapuram 88, Kollam 61, Alappuzha 34, Pathanamthitta 13, not recorded 8.
- No duplicate college IDs, names or rows were found.
- All populated emails passed the basic format check, and all populated phone numbers passed the length check.

These figures describe the records that were extracted. They do not independently prove the distribution of every college affiliated with the university.

---

## Requirements

- Python 3.8+
- Libraries: `requests`, `beautifulsoup4`, `pandas`, `matplotlib`, `openpyxl` (needed for the Excel export)

```bash
pip install requests beautifulsoup4 pandas matplotlib openpyxl
```

## How to run

1. Open `Web_Scraping_Project_clean.ipynb` in Jupyter, VS Code or Google Colab.
2. Run all cells from top to bottom. An internet connection is required.
3. The scraping step takes a few minutes because it waits 0.5 seconds between requests.

## Output files

| File | Created in | Contents |
|------|-----------|----------|
| `kerala_university_colleges.csv` | Step 3 | Raw scraped contact details |
| `kerala_university_colleges.xlsx` | Step 3 | Same data as Excel |
| `kerala_university_colleges_enriched.csv` | Step 4 | Contact details plus district, year and type |
| `kerala_university_colleges_final.csv` | Step 8 | Final cleaned dataset |

---

## Notes and limitations

- The scraper depends on the current HTML structure of the university website. If the site changes, the extraction code may need updating.
- Phone and email checks only test format. They do not confirm the details are active or current.
- The missing fields (mainly addresses) should be verified against the official college pages before using the data as an operational directory.
- Requests are paced with a short delay and a descriptive User-Agent. Please keep that behaviour if you re-run the scraper, and follow the website's terms of use.

## Possible improvements

- Re-check the 13 colleges whose contact section was not found.
- Fill missing district, year and type values manually or from another source.
- Re-run the scraper periodically to capture changes on the website.
