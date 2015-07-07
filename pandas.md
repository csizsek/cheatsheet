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
`s['a']` | An element of a series
`s[['a', 'b']]` | A sub-series

###Series Attributes and Member Functions
Attribute/Function | Description
---  | ---
`s.dtype` | Data type
`s.name` | Name
`s.index` | Index
`s.index.name` | Index name
`s.values` | Values as an array
`s.drop('c')` `s.drop(['c', 'd'])` | Drop elements with the specified index(es)

###Operations
Expression | Description
---  | ---
`pd.isnull(s)` `pd.notnull(s)` | A Series object with the (not) nullness of the elements
`s + t` `s * t` `...` | Perform operations on the series with the indices aligned

###NumPy's Array Operations on Series
Expression | Description
---  | ---
`s[s > 2]` | The series is indexed with a boolean series and the sub-series with the elements at the True indices are returned (preserves the index)
`s * 2` `np.exp(s)` | Array-like operations with a scalar (preserves the index)

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
`d.foo = np.arange(5)` | Assign the elements of the specified list to the elements of the column (assuming that the length of the list is the same as the #rows of the column)
`d.ix['a']` | The row(s) at `index='a'` of the frame

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

##Index Type

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