# Create an array of string from a numerical range

```kql
print Column1 = range(200,299)
| mv-apply Column1 on (
    summarize Column1 = make_list(tostring(Column1))
)
```

# boolean expression to determine if value is in a range

## Example 1

```kql
print  array_index_of(range(200,299), 200) > -1
```

## Example 2

```kql
| where array_index_of( range(200,299), toint(StatusCode)) > -1
```