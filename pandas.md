#Pandas Cheat Sheet

##Series

###Creating Series Objects
Expression | Description
---  | ---
`Series([1, 2, 3])` | A Series object
`Series([1, 2, 3], dtype='int64')` | A Series object with the specified data type
`Series([1, 2, 3], index=list('abc'))` | A Series object with the specified index
`Series([1, 2, 3], dtype='int64')` | A Series object with the specified data type
`Series({'foo': 1, 'bar': 2, 'baz': 3})` | A Series object with the keys of the dict as indices
`Series({'a': 1, 'b': 2}, index=list('abc'))` | A Series object with the specified elements and index (the unspecified elements will be `NaN`s)

###Indexing
Expression | Description
---  | ---
`s['a']` | An element of a series with the specified index
`s[['a', 'b']]` | A sub-series with the specified indices
`s['a':'c']` | Slicing by indices (opposed to normal Python slicing, the endpoint is inclusive as well)
`s[s < 3]` | Filter by the specified criteria

###Series Attributes and Member Functions
Attribute/Function | Description
---  | ---
`s.dtype` | Data type
`s.name` | Name
`s.index` | Index
`s.index.name` | Index name
`s.values` | Values as an array
`s.drop('c')` `s.drop(['c', 'd'])` | Drop elements with the specified index(es)

###Operations and Arithmetic
Expression | Description
---  | ---
`pd.isnull(s)` `pd.notnull(s)` | A Series object with the (not) nullness of the elements
`s + t` `s * t` `...` | Perform operations on the series with the indices aligned (intoduces `NaN`s if there is a difference in indices)

###NumPy's Array Operations on Series
Expression | Description
---  | ---
`s[s > 2]` | The series is indexed with a boolean series and the sub-series with the elements at the True indices are returned (preserves the index)
`s * 2` `np.exp(s)` | Array-like operations with a scalar (preserves the index)

###Sorting and Ranking
Expression | Description
---  | ---
`s.sort_index()` `...` | Returns a new sorted object with the elements sorted by the index
`s.sort_index(ascendind=False)` `...` | Descending sort
`s.order()` | Sort by elements
`s.rank()` | Return a series with the same index as `s` but instead of the original elements of the series it contains the rank of each element if the series would be sorted (in case of ties it assigns the mean rank of the tied group)
`s.rank(method='first')` | Assigns the rank of the first element to each element in the group in case of a tie (available tie resolution methods are `min`, `max`, `mean` and `first`)
`s.rank(ascending=Falese)` | Sorts in descending order
##DataFrame

###Creating DataFrame Objects
Expression | Description
---  | ---
`DataFrame({'foo': [1, 2, 3], 'bar': [4, 5, 6]})` | A DataFrame object with the columns `foo` and `bar` and 3 rows
`DataFrame(data, columns=['foo', 'bar'])` | A DataFrame object with the specified (order of) columns
`DataFrame(data, index=list('abcde'))` | A DataFrame object with the specified row indices
`DataFrame([{'foo': 1, 'bar': 2}, {'foo': 5, 'bar': 10}])` | A DataFrame object with the list elements as rows and the dict elements as columns
`DataFrame(np.arange(15).reshape((5, 3)), columns=['foo', 'bar', 'baz'])` | A DataFrame object from the 2D array with the specified columns

###Indexing
Expression | Description
---  | ---
`d['foo']` `d.foo` | The column `foo` of the frame
`d['bar'] = 16.5` | Assign a value to all elements in the specified column of the frame
`d[d > 10]` | A data frame with the same shape as `d` but with `NaN`s instead of the elements where the specified filtering criteria does not hold
`d[d.foo > 10]` | The rows of the frame where the criteria is true
`d.foo = np.arange(5)` | Assign the elements of the specified list to the elements of the column (assuming that the length of the list is the same as the #rows of the column)
`d.ix['a']` | The row(s) at `index='a'` of the frame
`d.ix[['a', 'c'], 'foo']` | A sub-frame of the frame with the specified rows (`a` and `c`) and the specified column (`foo`)
`d.ix['a':'c', 'foo']` | A sub-frame of the frame with the specified rows (`a` to `c` inclusive) and the specified column (`foo`)
`d.icol(2)` | The elements of the third column as a Series with the original row index preserved
`d.irow(2)` | The elements of the third row as a Series with the column names as indices
`d.xs('c')` | The elements of the row `c` as a Series with the column names as indices

###DataFrame Attributes and Member Functions
Attribute/Function | Description
---  | ---
`d.dtypes` | The data types of each column
`d.name` | Name
`d.index` | Indices
`d.index.name` | Index name
`d.columns` | List of columns
`d.columns.name` | Name of the columns list
`d.values` | Values as a 2D array
`d.drop('c')` `d.drop(['c', 'd'])` | Drop elements with the specified index(es)
`d.drop('foo', axis=1)` `s.drop(['foo', 'bar'], axis=1)` | Drop columns with the specified index(es)

###Operations and Arithmetic
Expression | Description
---  | ---
`d + e` `...` | Perform operations on the frames with the row and column indices aligned (intoduces `NaN`s if there is a difference in indices)
`d.add(e)` `d.sub(e)` `d.div(e)` `d.mul(e)`| Flexible arithmetic methods on frames
`d.add(e, fill_value=0)` | Flexible arithmetic methods on frames with a default fill value (instead of introducing `NaN`s)
`d + s` `d.sub(s)` `...`| Arithmetic between a frame and a series (by default it matches the index of the series on the columns of the frame broadcasted down the rows)
`d.add(s, axis=0)` `...`| Arithmetic between a frame and a series (match the index of the series )

###Function Application and Mapping
Expression | Description
---  | ---
`np.abs(d)` `...` | Element-wise `abs` on the frame (works with all NumPy functions)
`f.apply(f)` | Applies the given function `f` row-wise
`f.applymap(f)` | Applies the given function `f` element-wise and returns a frame of the same shape as `d` with the results
`d['c'].map(f)` | Applies `f` on the elements of column `c` element-wise

###Sorting and Ranking
Expression | Description
---  | ---
`d.sort_index()` `...` | Returns a new sorted object with the elements sorted by the index
`d.sort_index(axis=1)` `...` | Sort columns by the index
`d.sort_index(ascendind=False)` `...` | Descending sort
`d.sort_index(by='foo')` | Sort by elements in column `foo`
`d.sort_index(by=['foo', 'bar'])` | Sort by elements in columns `foo` then `bar`

##Index

###Index Types
Type | Description
---  | ---
`Index` | The most general Index type
`Int64Index` | Special Index type for integer values
`MultiIndex` | Hierarchical Index type representing multiple levels of indices on a single axis
`DatetimeIndex` | Nanosecond timestamp Index
`PeriodIndex` | Special index for period (timespan) data

###Creating Index Objects
Expression | Description
---  | ---
`pd.Index(np.arange(10))` | An Index object

###Index Attributes and Member Functions
Attribute/Function | Description
---  | ---
`i.append(j)` | Concatenate with other Index
`i.difference(j)` | Set diff of two Indices as an Index
`i.intersection(j)` | Intersection
`i.union(j)` | Union
`i.isin[1, 2, 3]` | A boolean array indicating whether the Index elements are contained by the passed-in collection
`i.delete(5)` | Remove element from the Index
`i.drop([5, 6])` | Remove elements from the Index
`i.insert(5, 3)` | Insert 5 at position 3
`i.is_monotonic` | Monotonicity
`i.is_unique` | Uniqueness
`i.unique()` | Compute unique sequence

###Reindexing Series and DataFrames
Expression | Description
---  | ---
`s.reindex(['a', 'b', 'c'], fill_value=0)` | Reindex the series
`d.reindex(['a', 'b', 'c'], method='ffill')` | Reindex the frame

###Reindex Function Args
Arg | Description
---  | ---
`index` | The new index sequence (can be an pd.Index type or any sequence-like structure)
`method` | The method to populate the missing elements (can be `ffill`, `pad`, `backfill` or `bfill`)
`fill_value` | Substitute value to use when introducing missing data
`limit` | Maximum size gap to fill
`level` | Match simple index on level of MultiIndex, otherwise select subset of
`copy` | If `True` then always copy underlying data

###Hierarchical Index
Expression | Description
---  | ---
`Series([1, 2, 3, 4], index=[['a', 'a', 'b', 'b'], [1, 2, 1, 2]])` | A Series object with a 2-level index
`DataFrame(np.random.randint(0, 10, 15).reshape(5, 3), index=[['foo', 'foo', 'foo', 'bar', 'bar'], ['a', 'b', 'c', 'a', 'b']])` | A DataFrame object with a 2-level row index
`d['a']` | All elements with the main index `a` and any subindex
`s.unstack()` | Unstack a series with a multi-index into a frame (the main index labels will be the row labels and the secondary index labels will be the columns)
`d.stack()` | Stack a frame into a multi-indexed series

##Summarizing and Computing Stats

###Reduction Methods
Method | Description
---  | ---
`d.count()` | Returns a series with the frame's column (by default) indices and the count of the elements in the columns
`d.describe()` | A set of summary stats
`d.min()` `d.max()` | Minimum/maximum
`np.argmin(e[1])` `np.argmax(e[1])` | The index location (i.e. an integer) of the minimal/maximal element
`d.idxmin()` `d.idxmax()` | The index value of the minimal/maximal element
`d.quantile(0.7)` | Quantile
`d.sum()` | Sum
`d.mean()` | Mean
`d.median()` | Median
`d.mad()` | Mean absolute deviation
`d.var()` | Simple variance
`d.std()` | Sample standard deviation
`d.skew()` | Sample skewness (3rd moment)
`d.kurt()` | Sample kurtosis (4th moment)
`d.cumsum()` | Cumulative sum
`d.cummin()` `d.cummax()` | Cumulative min/max
`d.cumprod()` | Cumulative product
`d.diff()` | 1st arithmetic difference
`d.pct_change())` | Percent change

###Reduction Method Args
Arg | Description
---  | ---
`axis` | Which axis to preserve (the default is to preserve columns)
`skipna` | Exclude missing values (the default is True)
`level` | Reduction level for hierarchical MultiIndex

###Other Statistical Methods
Method | Description
---  | ---
`d.cor()` | The correlation of the frame's columns with each other
`d.cov()` | The covariance of the frame's columns with each other
`d.foo.corr(d.bar)` | The correlation of the columns `foo` and `bar`
`d.foo.cov(d.bar)` | The covariance of the columns `foo` and `bar`
`d.corrwith(e.foo)` | The covariance of `d`'s columns with `e.foo`
`pd.value_counts(s)` | Value counts for series elements
`d.apply(pd.value_counts).fillna(0)` | Value counts for each column with zeros instead of `NaN`s

###Handling Missing Values
Expression | Description
---  | ---
`d.is_null()` `s.is_null()` | Element-wise nullness
`d.dropna()` | Drop rows that contain any null values
`d.dropna(how='all')` | Drop rows that contain only null values
`d.dropna(axis=1)` | Drop columns that contain any null values
`d.dropna(thresh=2)` | Drop rows that contain at least 2 null values
`d.fillna(0)` | Fill in null values with zeros
`d.fillna(0, inplace=True)` | Fill in null values in place with zeros
`d.fillna(method='ffill')` | Forward fill null values (i.e. copy the value just before the null into the null element)
`d.fillna(d.mean())` | Fill in null values with the mean of the column

##Data Loading and Storage

###Data Parsing Functions
Function | Description
---  | ---
`pd.read_csv('data.txt')` | Load the file file into a Pandas DataFrame (the deafult delimiter is `,`)
`pd.read_table('data.txt')` | Load the file file into a Pandas DataFrame (the deafult delimiter is `\t`)
`pd.read_fwf('data.txt')` | Load the fixed width file into a Pandas DataFrame (no delimiter)

###Data Parsing Function Args
Arg | Description
---  | ---
`path` | File path or URL
`sep` `delimiter` | Character sequence or regex as a delimiter between fields
`header` | Row number to use as a header (the default is 0). Should be `None` if there is no header
`index_col` | Column numbers or names to use as a row index
`names` | A list of column names for result (combine with `header=None`)
`skiprows` | Number of rows at the beginning of the file to ignore (or a list of row numbers indexed from 0)
`na_values` | Sequence of values to be replaced with `NaN`
`comment` | Character or char sequence to split off comments from the end of lines
`parse_dates` | Attempt to parse data to Datetime
`converters` | A dict containing the the column names to converter functions
`date_parser` | The function to use for parsing dates
`nrows` | Number of rows to read
`iterator` | Return a `TextParser` object
`chunksize` | The size of file chunks (for iteration)
`skip_footer` | Number of lines to ignore at the end of file
`verbose` | Print parser output info
`encoding` | Text encoding for unicode
`squeeze` | Return a Series for a data file with 1 column
`thousands` | Thousand separator

