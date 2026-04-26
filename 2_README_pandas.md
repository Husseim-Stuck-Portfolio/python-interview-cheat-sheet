# pandas-cheat-sheet
A practical, well-organized "Pandas cheat sheet" covering data creation, I/O, indexing, filtering, aggregation, merging, reshaping, window functions, time series, string/datetime accessors, PyArrow backends, and modern pandas 2.x–3.x features.


# Pandas Cheat Sheet for Data Analysts, Scientists, and Developers

A practical, well-organized **Pandas cheat sheet** covering data creation, reading/writing, inspection, selection, filtering, sorting, missing data, data types, string/datetime accessors, apply/map, groupby, aggregation, merging, reshaping, pivoting, window functions, time series, multi-indexing, categorical data, PyArrow backends, copy-on-write, and modern pandas 2.x–3.x features.

This repository is designed for data analytics students, data scientists, bootcamp learners, backend developers, and anyone preparing for technical interviews who wants a fast, searchable, real-world pandas reference with corrected syntax examples and logically grouped query patterns.

## Contributing

Contributions are welcome if you want to improve examples, fix syntax, expand coverage, or add more real-world analytics use cases.

## Why this Pandas Cheat Sheet?

If you are learning Python for data analytics, machine learning, backend development, or technical interviews, this project gives you a single place to review the most useful pandas commands and patterns.

It focuses on:
- Modern pandas-first syntax (2.x through 3.x)
- Clear examples you can reuse quickly
- Logical grouping by topic
- Short explanations for fast scanning
- Common interview and day-to-day queries
- Cleanup of mixed or outdated syntax from broader references
- PyArrow-backed dtypes and copy-on-write awareness

## What's Included

This pandas cheat sheet includes:

- `pd.Series` and `pd.DataFrame` creation from dicts, lists, arrays, and files
- I/O: CSV, Excel, SQL, JSON, Parquet, Feather, ORC, HTML, clipboard, pickle
- Inspection: `head`, `tail`, `info`, `describe`, `shape`, `dtypes`, `memory_usage`
- Selection & indexing: `[]`, `loc`, `iloc`, `at`, `iat`, `isin`, `where`, `query`, `mask`
- Filtering, boolean indexing, and conditional assignment
- Sorting: `sort_values`, `sort_index`, `nsmallest`, `nlargest`
- Missing data: `isna`, `dropna`, `fillna`, `interpolate`, `replace`
- Data types: `astype`, `to_numeric`, `to_datetime`, `convert_dtypes`, `category`, `string`
- PyArrow integration: `dtype_backend="pyarrow"`, `string[pyarrow]`, `ArrowDtype`
- String accessor (`.str`): `contains`, `split`, `replace`, `extract`, `zfill`, `pad`
- Datetime accessor (`.dt`): `year`, `month`, `day`, `to_period`, `tz_localize`, `tz_convert`
- Apply & map: `apply`, `map`, `applymap`, `pipe`
- GroupBy: `groupby`, `agg`, `transform`, `filter`, `rolling`, `resample`
- Aggregation & statistics: `sum`, `mean`, `std`, `var`, `quantile`, `corr`, `cov`, `cumsum`
- Merging & joining: `merge`, `join`, `concat`, `append`
- Reshaping: `pivot`, `pivot_table`, `melt`, `stack`, `unstack`, `explode`, `crosstab`
- Window functions: `rolling`, `expanding`, `ewm`
- Duplicates: `duplicated`, `drop_duplicates`
- Binning: `cut`, `qcut`
- Sampling: `sample`
- MultiIndex / hierarchical indexing
- Categorical data
- Time series: `resample`, `asfreq`, `shift`, `diff`, `pct_change`
- Options & settings: `pd.set_option`, `pd.get_option`
- Visualization: `plot`, `hist`, `box`, `scatter`
- Performance: `eval`, `query` engine, copy-on-write

## Who This Repository Is For

This repository is useful for:

- Data analytics students learning pandas and Python
- Bootcamp students building portfolio projects
- Junior data analysts preparing for interviews
- Data scientists who need a quick pandas syntax reference
- Backend developers working with tabular data in Python
- Anyone converting generic Python notes into valid, up-to-date pandas syntax


---

## Main Topics

### 1. Import & Setup
Core imports, version checks, and global option configuration.

### 2. Data Creation
Creating `Series` and `DataFrame` objects from dicts, lists, arrays, ranges, and random data.

### 3. I/O — Reading Data
Loading data from CSV, Excel, SQL, JSON, Parquet, Feather, ORC, HTML, clipboard, and pickle.

### 4. I/O — Writing Data
Saving data to CSV, Excel, SQL, JSON, Parquet, Feather, HTML, clipboard, and pickle.

### 5. Inspection & Attributes
Quickly understanding your data with shape, dtypes, memory usage, and preview methods.

### 6. Selection & Indexing
Label-based (`loc`), position-based (`iloc`), fast scalar (`at`/`iat`), boolean masks, `isin`, `where`, and `query`.

### 7. Filtering & Conditional Logic
Row filtering, multi-condition masks, between, regex, and conditional column assignment.

### 8. Adding, Updating & Deleting
Creating new columns, modifying existing ones, renaming, and dropping rows/columns.

### 9. Sorting
Sorting by values, index, multiple columns, and retrieving top/bottom N rows.

### 10. Missing Data
Detecting, dropping, filling, interpolating, and replacing missing or null values.

### 11. Data Types & Conversion
Casting types, inferring types, converting to numeric/datetime, and using nullable/extension dtypes.

### 12. PyArrow & Modern Backends
Using PyArrow-backed strings, numeric types, and the `dtype_backend` parameter for memory efficiency.

### 13. String Accessor (`.str`)
Vectorized string operations: contains, split, replace, extract, strip, pad, zfill, and regex.

### 14. Datetime Accessor (`.dt`)
Extracting date parts, rounding, timezone handling, and period conversion.

### 15. Apply, Map & Pipe
Applying functions element-wise, row-wise, column-wise, and chaining operations with `pipe`.

### 16. GroupBy
Split-apply-combine workflows: aggregation, transformation, filtering, and grouped window ops.

### 17. Aggregation & Statistics
Built-in reductions, custom aggregations, cumulative operations, correlation, and covariance.

### 18. Merging & Joining
Combining DataFrames with `merge`, `join`, `concat`, and cross joins.

### 19. Reshaping & Pivoting
Pivot tables, melting, stacking/unstacking, exploding lists, and crosstabs.

### 20. Window Functions
Rolling, expanding, and exponentially weighted moving averages.

### 21. Duplicates
Detecting and removing duplicate rows.

### 22. Binning & Discretization
Cutting into equal-width or equal-frequency bins.

### 23. Sampling & Random Selection
Random sampling with or without replacement, weighted sampling, and train/test splits.

### 24. MultiIndex / Hierarchical Indexing
Multi-level row and column indexes, index slicing, and cross-section selection.

### 25. Categorical Data
Memory-efficient categorical dtype, ordering, renaming categories, and dummy encoding.

### 26. Time Series
Resampling, frequency conversion, shifting, differencing, and percent change.

### 27. Visualization
Quick plots: line, bar, histogram, box, scatter, and area charts.

### 28. Options, Settings & Performance
Global display options, copy-on-write mode, and expression evaluation.


## SEO Keywords Targeted

- pandas cheat sheet
- pandas functions reference
- pandas interview cheat sheet
- pandas data manipulation
- pandas read csv excel sql json
- pandas groupby agg transform
- pandas merge join concat
- pandas pivot melt reshape
- pandas window functions rolling
- pandas time series resample
- pandas string methods str accessor
- pandas datetime dt accessor
- pandas missing data fillna dropna
- pandas pyarrow backend
- pandas copy on write
- pandas type conversion astype
- pandas multiindex hierarchical
- pandas categorical data
- pandas one hot encoding get_dummies
- pandas plot visualization
- pandas style table formatting
- pandas performance optimization
- pandas 2.0 new features
- pandas 3.0 pyarrow strings
- python data analysis cheat sheet
- data science pandas reference

## How This Cheat Sheet Was Built

This project was created by extracting pandas patterns from source notes, official documentation, and real-world analytics workflows, then reorganizing and correcting them into a clean, pandas-focused structure.

The cleanup process included:
- grouping related functions by theme
- removing duplicates and outdated syntax
- replacing deprecated methods with modern equivalents
- preserving practical, copy-pasteable examples
- making the sheet easier to scan and search
- adding version awareness for pandas 2.x and 3.x features

## Best Ways to Use This Project

- Review before data analytics or Python coding interviews
- Use as a quick command lookup during projects
- Study one section at a time
- Compare older pandas syntax with modern alternatives
- Add your own examples as you learn

## Contributing

Contributions are welcome if you want to improve examples, fix syntax, expand coverage, or add more real-world analytics use cases.


## License

MIT for open reuse

## Author
Husseim Stuck

Created as a practical pandas learning and reference resource for data analytics study, portfolio work, and interview preparation.
