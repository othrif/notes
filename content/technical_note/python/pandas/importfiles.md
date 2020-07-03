---
title: "Importing files using pandas"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---


### From csv


```python
import pandas as pd 
file = 'titanic.csv'
# Read the file into a DataFrame: df
df = pd.read_csv(file)
# View the head of the DataFrame
print(df.head())

```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-1-25973cb3da0e> in <module>
          2 file = 'titanic.csv'
          3 # Read the file into a DataFrame: df
    ----> 4 df = pd.read_csv(file)
          5 # View the head of the DataFrame
          6 print(df.head())


    ~/Library/Python/3.7/lib/python/site-packages/pandas/io/parsers.py in parser_f(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, squeeze, prefix, mangle_dupe_cols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, dialect, error_bad_lines, warn_bad_lines, delim_whitespace, low_memory, memory_map, float_precision)
        674         )
        675 
    --> 676         return _read(filepath_or_buffer, kwds)
        677 
        678     parser_f.__name__ = name


    ~/Library/Python/3.7/lib/python/site-packages/pandas/io/parsers.py in _read(filepath_or_buffer, kwds)
        446 
        447     # Create the parser.
    --> 448     parser = TextFileReader(fp_or_buf, **kwds)
        449 
        450     if chunksize or iterator:


    ~/Library/Python/3.7/lib/python/site-packages/pandas/io/parsers.py in __init__(self, f, engine, **kwds)
        878             self.options["has_index_names"] = kwds["has_index_names"]
        879 
    --> 880         self._make_engine(self.engine)
        881 
        882     def close(self):


    ~/Library/Python/3.7/lib/python/site-packages/pandas/io/parsers.py in _make_engine(self, engine)
       1112     def _make_engine(self, engine="c"):
       1113         if engine == "c":
    -> 1114             self._engine = CParserWrapper(self.f, **self.options)
       1115         else:
       1116             if engine == "python":


    ~/Library/Python/3.7/lib/python/site-packages/pandas/io/parsers.py in __init__(self, src, **kwds)
       1889         kwds["usecols"] = self.usecols
       1890 
    -> 1891         self._reader = parsers.TextReader(src, **kwds)
       1892         self.unnamed_cols = self._reader.unnamed_cols
       1893 


    pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader.__cinit__()


    pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._setup_parser_source()


    FileNotFoundError: [Errno 2] File titanic.csv does not exist: 'titanic.csv'



```python

```
