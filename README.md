# BambooChute: Data Cleaning for Pandas

**BambooChute** is a comprehensive data cleaning toolkit built on top of Pandas, offering a vast array of functions to streamline your data preparation process. From handling missing data to detecting outliers, managing categorical data, and ensuring data integrity, BambooChute empowers data analysts, scientists, and engineers to work more efficiently with their data.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Functionality Overview](#functionality-overview)
  - [Loading Data](#loading-data)
  - [Handling Missing Data](#handling-missing-data)
  - [Outlier Detection and Removal](#outlier-detection-and-removal)
  - [Categorical Data Processing](#categorical-data-processing)
  - [Date Handling and Transformation](#date-handling-and-transformation)
  - [Data Type Validation](#data-type-validation)
  - [Duplicate Management](#duplicate-management)
  - [Data Formatting](#data-formatting)
  - [Data Profiling](#data-profiling)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Versatile Data Loading:** Seamlessly load data from multiple formats (CSV, Excel, JSON, and Pandas DataFrames).
- **Comprehensive Missing Data Handling:** Use a variety of imputation strategies (mean, median, KNN, regression, etc.) and drop methods.
- **Flexible Outlier Detection & Removal:** Detect outliers using various methods (Z-score, IQR, Isolation Forest, etc.) with detailed configuration options.
- **Efficient Categorical Data Processing:** Convert, encode, map, and manage rare categories with ease.
- **Robust Date Handling:** Convert dates, extract date parts, handle invalid dates, and calculate date differences.
- **Data Validation Tools:** Validate data types, check for missing data, and ensure value consistency.
- **Duplicate Management:** Identify, mark, merge, and handle near-duplicates with options for fuzzy matching.
- **Consistent Data Formatting:** Clean string data by trimming whitespace, standardizing cases, and removing special characters.
- **Data Profiling:** Generate summary reports on missing data, outliers, distribution, and correlations for a comprehensive overview.

## Installation

Install BambooChute via pip:

```bash
pip install BambooChute
```

Ensure dependencies from `requirements.txt` are installed:

```bash
pip install -r requirements.txt
```

## Getting Started

Here’s an example to get you started with loading data, handling missing values, detecting outliers, and exporting the cleaned data:

```python
import pandas as pd
from BambooChute import Bamboo

# Load data
data = pd.read_csv('data.csv')

# Initialize Bamboo
bamboo = Bamboo(data)

# Preview data
print(bamboo.preview_data())

# Handle missing data
bamboo.impute_missing(strategy='mean')

# Detect and remove outliers
bamboo.detect_outliers_zscore(threshold=3)

# Export cleaned data
bamboo.export_data('cleaned_data.csv')
```

## Functionality Overview

### Loading Data

BambooChute makes it easy to load data from various sources. The `Bamboo` class can accept:
- **CSV**: Read from a CSV file path.
- **Excel**: Read from an Excel file.
- **JSON**: Load data from a JSON file.
- **Pandas DataFrame**: Load data directly from an in-memory DataFrame.

```python
# Load data from various formats
bamboo = Bamboo('data.csv')  
bamboo = Bamboo(df)  
```

This flexibility allows BambooChute to be integrated with most data pipelines, irrespective of the data source.

### Handling Missing Data

The package offers multiple imputation methods to fill missing values, including:
- **Mean, Median, and Mode Imputation**: Fill missing values in numeric columns using statistical averages.
- **K-Nearest Neighbors (KNN)**: Impute values based on the values of nearby points, ensuring continuity in numerical patterns.
- **Custom Functions**: Define your own function for filling missing values.

Example Usage:

```python
# Impute missing values using the mean of each column
bamboo.impute_missing(strategy='mean')

# Impute using K-Nearest Neighbors
bamboo.impute_knn(n_neighbors=5)

# Drop rows or columns with missing values
bamboo.drop_missing(axis=0, how='any')
```

Each function supports optional parameters to control which columns are affected, allowing for precise control over data imputation.

### Outlier Detection and Removal

Outliers can distort your data analysis, so BambooChute offers several detection methods:
- **Z-score Detection**: Identifies outliers by measuring how many standard deviations a value is from the mean.
- **IQR (Interquartile Range)**: Detects values outside a specific range based on the first and third quartiles.
- **Isolation Forest and DBSCAN**: Use machine learning to detect outliers in complex datasets.

Example Usage:

```python
# Detect outliers using Z-Score
outliers = bamboo.detect_outliers_zscore(threshold=3)

# Remove outliers using IQR
bamboo.remove_outliers(method='iqr', multiplier=1.5)

# Remove outliers using Isolation Forest
bamboo.remove_outliers_isolation_forest(contamination=0.1)
```

### Categorical Data Processing

BambooChute makes it easy to manage categorical data with functions for:
- **Conversion to Categorical**: Change columns to categorical types.
- **Encoding**: Convert categories to one-hot or label encodings.
- **Rare Category Detection**: Identify and replace rare categories to improve model performance.

Example Usage:

```python
# Convert columns to categorical type
bamboo.convert_to_categorical(['column'])

# Encode categorical data with one-hot encoding
bamboo.encode_categorical(method='onehot')

# Detect and replace rare categories
rare_categories = bamboo.detect_rare_categories(column='category_column', threshold=0.05)
bamboo.replace_rare_categories(column='category_column', replacement='Other')
```

### Date Handling and Transformation

BambooChute simplifies working with dates, offering tools for:
- **Conversion to Datetime**: Convert columns to a datetime format.
- **Extraction of Date Parts**: Extract parts of a date (year, month, day).
- **Date Range Creation**: Generate sequences of dates.
- **Date Differences**: Calculate differences between dates.

Example Usage:

```python
# Convert columns to datetime format
bamboo.convert_to_datetime(['date_column'])

# Extract specific date parts (e.g., year, month)
bamboo.extract_date_parts('date_column', parts=['year', 'month'])

# Calculate time difference between two date columns
bamboo.calculate_date_differences(start_column='start_date', end_column='end_date')
```

### Data Type Validation

Data integrity is critical, and BambooChute’s data type validation tools allow you to:
- **Check Consistency**: Identify columns with mixed types.
- **Convert Data Types**: Enforce specific types across columns.
- **Identify Invalid Types**: Detect rows with types that don’t match the expected type for a column.

Example Usage:

```python
# Check for data type consistency
consistency = bamboo.check_dtype_consistency()

# Enforce specific data types
bamboo.enforce_column_types({'age': 'int64', 'price': 'float64'})
```

### Duplicate Management

Efficiently manage duplicates with functions for:
- **Identifying Duplicates**: Find duplicate rows.
- **Dropping Duplicates**: Remove duplicate rows, keeping specific occurrences.
- **Near-Duplicate Detection**: Identify nearly identical values using fuzzy matching.

Example Usage:

```python
# Identify duplicates based on specific columns
duplicates = bamboo.identify_duplicates(subset=['name'])

# Drop duplicates, keeping the first occurrence
bamboo.drop_duplicates(keep='first')

# Handle near-duplicates using fuzzy matching
bamboo.handle_near_duplicates(column='name', threshold=0.8)
```

### Data Formatting

BambooChute’s formatting tools allow you to standardize data appearance:
- **Whitespace Management**: Trim excess whitespace from strings.
- **Case Standardization**: Convert text to lowercase, uppercase, or title case.
- **Special Character Removal**: Clean up text fields by removing unwanted symbols.

Example Usage:

```python
# Trim whitespace in string columns
bamboo.trim_whitespace()

# Standardize case to title
bamboo.standardize_case(case='title')

# Remove special characters in specific columns
bamboo.remove_special_characters(columns=['text_column'], chars_to_remove='@#$')
```

### Data Profiling

Gain insights into your data by generating summary reports, allowing for a deeper understanding of data structure and issues.

```python
# Generate a summary report with key insights on data
summary = bamboo.generate_summary_report()
```

## Testing

The BambooChute package uses **pytest** for testing. To execute all tests in the `tests` directory, run:

```bash
pytest tests/
```

For more detailed output, add the `-v` flag for verbose mode or `--maxfail=3` to stop after three failures. This ensures every function is well-tested for reliability and performance.

## Contributing

To contribute:

1. Go the homepage, fork the repository.
2. Create a new branch.
3. Make changes and submit a pull request with your email.
  - You will receive an email asking about your changes, please reply.
4. Thanks for contributing!

## License

BambooChute is licensed under the MIT License.