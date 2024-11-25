# Module 6 challenge

>[!Note]
>
>This README and the files in this repository were reviewed and enhanced using the following AI platforms:
>
>> OpenAI. (2023). ChatGPT (October 2023 version) [Large language model]. OpenAI. https://chat.openai.com
>> 
>> Grammarly Inc. (n.d.). Grammarly. https://www.grammarly.com

# NASA CME and GST Data Processing
This project extracts, processes, and merges data for Coronal Mass Ejections (CMEs) and Geomagnetic Storms (GSTs) from NASA's DONKI API. The resulting dataset is cleaned, analyzed, and exported for further use.
## Project Structure
1. **Request CME Data**  
   Fetch CME data using the NASA API, clean it, and prepare it for linking with GST data.

2. **Request GST Data**  
   Fetch GST data using the NASA API, clean it and prepare it for linking with CME data.

3. **Merge and Export Data**  
   Merge the two datasets based on their relationships, calculate insights, and export the final dataset.
## Prerequisites

1. **Python 3.7+**
2. **Libraries:**
   - `requests`
   - `pandas`
   - `dotenv`
   - `json`
3. **NASA API Key**

## Instructions

### Part 1: Request CME Data

1. **API Request:** Fetch CME data from the NASA DONKI API.
2. **Filter Columns:** Keep only `activityID`, `startTime`, and `linkedEvents`.
3. **Handle Missing Data:** Remove rows with missing `linkedEvents`.
4. **Expand Events:** Use a nested loop to expand `linkedEvents` into individual rows.
5. **Extract GST Activity IDs:** Create a function to extract `activityID` from the `linkedEvents` dictionary.
6. **Data Cleanup:**
   - Remove rows without `GST_ActivityID`.
   - Convert `startTime` to datetime format and rename it `startTime_CME`.
   - Rename `activityID` to `cmeID`.

### Part 2: Request GST Data

1. **API Request:** Fetch GST data from the NASA DONKI API.
2. **Filter Columns:** Keep only `activityID`, `startTime`, and `linkedEvents`.
3. **Handle Missing Data:** Remove rows with missing `linkedEvents`.
4. **Expand Events:** Use the `explode()` method to expand `linkedEvents` into individual rows.
5. **Extract CME Activity IDs:** Apply the extraction function to `linkedEvents`.
6. **Data Cleanup:**
   - Remove rows without `CME_ActivityID`.
   - Convert `startTime` to datetime format and rename it `startTime_GST`.
   - Rename `activityID` to `gstID`.

### Part 3: Merge and Export Data

1. **Merge Data:** Merge the CME and GST datasets on their respective `activityID` relationships.
2. **Calculate Time Differences:** Add a `timeDiff` column to calculate the time difference between `startTime_CME` and `startTime_GST`.
3. **Analyze Data:** Use `describe()` to compute mean and median time differences.
4. **Export:** Save the cleaned and merged dataset to a CSV file.

## Output

**Merged Dataset:** A CSV file containing linked CME and GST events with corresponding attributes.
- **Insights:** Mean and median time differences between CME and GST events.

## References

- [NASA DONKI API Documentation](https://api.nasa.gov/)
- [Pandas Documentation](https://pandas.pydata.org/)
