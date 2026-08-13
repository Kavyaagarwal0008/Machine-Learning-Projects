##
```
df['milage'] = (
    df['milage'].astype(str)
    .str.replace(r'[^\d]', '', regex=True)
    .replace('', np.nan)
    .astype(float)
)
```

```
df['price'] = (
    df['price'].astype(str)
    .str.replace(r'[^\d]', '', regex=True)
    .replace('', np.nan)
    .astype(float)
)
```
