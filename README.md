# Electric Vehicle (EV) Charging Station Visualization Program

## Task 8: Documentation

### I. Program Structure
The program processes and visualizes data related to electric vehicle charging stations and population distribution in Berlin. The goal is to generate a Streamlit application to identify areas requiring additional EV charging stations.

**Workflow Steps:**
1. **Load Data:**
   - Berlin geodata by postal codes (PLZ).
   - EV charging station data.
   - Population/resident data.
2. **Data Preprocessing:**
   - Process and merge data to create meaningful relationships.
   - Count charging stations by postal code (PLZ).
3. **Visualization:**
   - Generate an interactive Streamlit app for visual exploration of data.

---

### II. Key Components

#### 1. Imports
- **`pandas`**: For data manipulation.
- **`core.methods`**: A custom module containing data processing methods.
- **`core.HelperTools`**: Utility functions, such as a timer.
- **`config.pdict`**: Configuration dictionary storing filenames and parameters.

#### 2. Functions
- **`@ht.timer`**: A decorator to measure execution time for the `main()` function.
- **`main()`**: The main driver function for data loading, preprocessing, and app generation.

#### 3. Dataset Requirements
- **Geodata**: Spatial data for Berlin postal codes.
- **Charging Stations Data**: Existing EV charging station locations.
- **Residents Data**: Population data by postal code.

#### 4. Error Handling
Each step includes `try-except` blocks to handle and report errors during execution.

---

### III. Code Walkthrough

#### 1. Load Geodata
Reads the geodata file (`file_geodat_plz`) using `pd.read_csv()`. Defines Berlin's postal code regions for mapping.

#### 2. Load Charging Stations Data
Reads the dataset (`file_lstations`) with `pd.read_csv()` containing charging station locations.

#### 3. Preprocess Charging Stations Data
Uses `m1.preprop_lstat()` to clean, transform, and integrate charging station data with geodata.

#### 4. Count Charging Stations per PLZ
Uses `m1.count_plz_occurrences()` to count the number of charging stations for each postal code.

#### 5. Load Residents Data
Reads the residents' dataset (`file_residents`) with `pd.read_csv()`, containing population distribution.

#### 6. Preprocess Residents Data
Uses `m1.preprop_resid()` to clean and align population data with geodata.

#### 7. Generate Streamlit App
Combines processed data to create an interactive Streamlit app with `m1.make_streamlit_electric_Charging_resid()`.

---

### IV. Key Methods and Their Roles

- **`m1.preprop_lstat`**: Cleans and integrates charging stations data with Berlin's geodata.
- **`m1.count_plz_occurrences`**: Aggregates charging stations per postal code.
- **`m1.preprop_resid`**: Cleans and aligns residents data with Berlin's postal codes.
- **`m1.make_streamlit_electric_Charging_resid`**: Generates a Streamlit app for visualization.
- **`ht.timer`**: Logs the execution time of the `main()` function.

---

### V. Configuration (`config.pdict`)
The `pdict` dictionary stores file paths and parameters:
- `file_geodat_plz`: Filename for Berlin's postal code geodata.
- `file_lstations`: Filename for charging stations data.
- `file_residents`: Filename for population data.

---

### VI. Output

#### 1. Command-Line Messages
- Status updates for data loading, preprocessing, and app generation.
- Error messages in case of failures.

#### 2. Streamlit App
- Visualizes postal code regions, charging station density, and population distribution.
- Provides insights into areas requiring additional EV charging stations.

---

## Documentation for Utility Functions and Framework

This section explains the utility functions for data processing, serialization, computations, and randomization. These tools manage and analyze datasets involving DataFrames, dictionaries, and lists.

### I. Overview of Modules Imported

#### Standard Libraries:
- `math`, `random`, `pickle`: For mathematical operations, random value generation, and serialization.
- `time` and `functools`: Timing and decorators.
- `collections`:
  - `Counter`: Counts occurrences in collections.
  - `OrderedDict`: Maintains order in dictionaries.

#### Third-Party Libraries:
- **`pandas`**: For tabular data in DataFrames.

---

### II. Core Functions and Features

#### a. Timing Decorator
```python
def timer(func):
    """Print the runtime of the decorated function."""

II. Core Functions and Features
a. Timing Decorator
def timer(func):
    """Print the runtime of the decorated function"""
•	Purpose: Measures and prints the execution time of the decorated function.
•	Usage: Wrap any function with @timer to log its runtime.
b. Predicates
•	isElFilled(el, liste): Checks if an element exists in a list and is not None.
•	validateIndex (lambda): Checks if a DataFrame has no duplicate rows.
o	Returns True if no duplicates exist, otherwise False.
c. Serialization
@timer
def pickle_out(objName, dateiName):
    """Serialization"""
•	pickle_out(objName, dateiName): Saves a Python object to a file using pickle.
•	pickle_in(dateiName): Loads a Python object from a file using pickle.

d. Data Processing
1.	col_base_features(col, pattern):
o	Splits a column's string values by a pattern and extracts the first part.
2.	determine_dyn_colorder(colvals, colorder_fixedpart, pdict):
o	Dynamically adjusts column order by removing unnecessary elements and appending the fixed part to the remaining columns.
3.	cleanse_colnames(dfcn, zeichen):
o	Removes specified characters (zeichen) from DataFrame column names.
4.	countFreqs(arr):
o	Counts frequencies of elements in a list and returns an OrderedDict.

e. Data Cleaning
1.	List Cleaning:
o	remNanFromListFloat(x): Removes NaN values from a list.
o	remNullItemsFromList(x): Removes None values from a list.
2.	Dictionary Cleaning:
o	remNanFromDict(d): Removes keys with NaN values from a dictionary.
o	remNullItemsFromDict(d): Removes keys with None values from a dictionary.

f. Math and Combinatorics
1.	Set Operations:
o	intersect(x, y): Finds the intersection of two lists.
2.	Binomial Coefficient:
o	binom(n, k): Calculates the binomial coefficient C(n,k)=n!k!(n−k)!C(n, k)
g. Randomization
1.	getRandomColor(_):
o	Generates a random hex color code.

h. DataFrame Operations
1.	popRowFromDF(dframe, indexVal):
o	Removes a row from a DataFrame by index and returns the row as a list and the updated DataFrame.
2.	sortDF(dframe, col, asc):
o	Sorts a DataFrame by a specified column in ascending (asc=True) or descending (asc=False) order. Returns a new DataFrame with sorted rows.

i. Column Operations
1.	df_cols_assign_alias(x, y):
o	Renames DataFrame columns based on a mapping provided in pdict (parameter dictionary).
o	Mimics the SQL "AS" aliasing functionality.

III. Key Lambda Functions
1.	Splitting and Formatting:
o	lam_split: Extracts the second part of a string split by $.
o	tupToStr: Converts a tuple to a formatted string, e.g., (1, "A") -> "1. A".
2.	Sorting Dictionaries:
o	sortDictReverseOrderIntKey: Sorts a dictionary in reverse order by integer keys.
3.	Feature Extraction:
o	ohlist_To_FeaturesList: Extracts the unique prefix of each string in a list, split by $.


Documentation: Geospatial Data Preprocessing and Visualization Functions
This following explains the functions provided for geospatial data processing, preprocessing, and visualization of datasets. These functions focus on electric charging stations and residential data with postal codes (PLZ) in Germany. 

I. Imports
•	geopandas (gpd): For geospatial data handling.
•	core.HelperTools (ht): Utility tools (e.g., @ht.timer for runtime logging).
•	folium: For creating interactive maps.
•	streamlit (st): To build interactive web applications.
•	streamlit_folium (folium_static): To embed Folium maps into Streamlit apps.
•	branca.colormap (LinearColormap): For custom color mapping in visualizations.

II. Core Functions
1. sort_by_plz_add_geometry
Prepares and merges dataframes by postal codes (PLZ) and adds geospatial geometry.
Parameters:
•	dfr: Pandas DataFrame containing the primary dataset.
•	dfg: Geopandas DataFrame containing geospatial data.
•	pdict: Dictionary containing column mappings (e.g., pdict["geocode"] for the key to merge on).
Returns:
•	A GeoDataFrame with sorted data and valid geometries.

2. preprop_lstat
Preprocesses a dataset of charging stations and filters rows based on geographic and postal code constraints.
Parameters:
•	dfr: Pandas DataFrame from Ladesaeulenregister.csv.
•	dfg: Geospatial DataFrame.
•	pdict: Column mapping dictionary.
Returns:
•	GeoDataFrame of filtered and geospatially processed charging station data.
Steps:
1.	Filters relevant columns (PLZ, Bundesland, Breitengrad, Längengrad, KW).
2.	Converts latitude and longitude values to a proper decimal format.
3.	Filters rows for Berlin with postal codes between 10115 and 14200.
4.	Merges with geospatial data and ensures valid geometries.

3. count_plz_occurrences
Counts the occurrences of charging stations per postal code (PLZ).
Parameters:
•	df_lstat2: GeoDataFrame of charging station data.
Returns:
•	DataFrame with:
o	PLZ: Postal codes.
o	Number: Count of charging stations.
o	geometry: Geometry of the region.

4. preprop_resid
Preprocesses resident population data by postal codes and merges with geospatial data.
Parameters:
•	dfr: Pandas DataFrame from plz_einwohner.csv.
•	dfg: Geospatial DataFrame.
•	pdict: Column mapping dictionary.
Returns:
•	GeoDataFrame of residents data with valid geometries.
Steps:
1.	Filters relevant columns (PLZ, Einwohner, Breitengrad, Längengrad).
2.	Converts latitude and longitude to decimal format.
3.	Filters rows for postal codes between 10000 and 14200.
4.	Merges with geospatial data.

5. make_streamlit_electric_Charging_resid
Creates an interactive Streamlit app for visualizing heatmaps of:
•	Charging stations.
•	Resident population.
Parameters:
•	dfr1: GeoDataFrame with charging station data.
•	dfr2: GeoDataFrame with resident population data.
Returns:
•	A Streamlit app rendering heatmaps.
Features:
1.	Map Layers:
o	Heatmap for charging stations (based on Number).
o	Heatmap for residents (based on Einwohner).
2.	Color Maps:
o	Gradation from yellow to red to depict density.
3.	Interactivity:
o	Users can toggle between layers using radio buttons.
4.	Integration:
o	Embeds Folium maps into Streamlit via folium_static.
Steps:
1.	Initializes a Folium map centered on Berlin.
2.	Adds layers for residents and charging stations based on user selection.
3.	Applies color maps for density visualization.
4.	Displays the map in the Streamlit app.
![image](https://github.com/user-attachments/assets/e478ee90-3a2b-4132-b00d-529030d90707)

