# About
This is the Julia bindings for the fst format (http://www.fstpackage.org) although the format was originally designed to work with R it is language independent.

# How to use
```julia
Pkg.clone("https://github.com/xiaodaigh/fstformat.jl.git")
using fstformat
using DataFrames
import DataFrames.DataFrame

df = DataFrame(col1 = rand(1:5,1_000_000),
    col2 = rand(1:100, 1_000_000),
    col3 = rand(Bool, 1_000_000))


# df can be any object that DataFrames.DataFrame(df) can make into a DataFrame
# any IterableTables.jl compatible table like object is supported
fstformat.write(df, "df.fst")

# compression = 100; the highest
fstformat.write(df, "df.fst", 100)

# read the metadata
fstformat.readmeta("df.fst")

# read the data
fstformat.read("df.fst")

# read some columns
fstformat.read("df.fst"; columns = ["col1", "col2"])

# read some rows
fstformat.read("df.fst"; from = 500, to = 1000)

# read some columns and rows up to 1000
fstformat.read("df.fst"; columns = ["col1", "col2"], to = 1000)

# read some columns and rows from 500
fstformat.read("df.fst"; columns = ["col1", "col2"], from = 500)

# read some columns and rows from 500 to 1000
fstformat.read("df.fst"; columns = ["col1", "col2"], from = 500, to = 1000)

```