```
import re
import numpy as np
import pandas as pd

def parse_engine(text):
    text = str(text)
    hp = re.search(r'([\d.]+)\s*HP', text)
    liters = re.search(r'([\d.]+)\s*L(?:iter)?\b', text)
    cyl = re.search(r'(\d+)\s*Cylinder', text)
    if not cyl:
        cyl = re.search(r'\b[VIH](\d+)\b', text)
    is_electric = 1 if 'Electric' in text else 0
    is_turbo = 1 if 'Turbo' in text or 'Supercharged' in text else 0
    return pd.Series({
        'horsepower': float(hp.group(1)) if hp else np.nan,
        'engine_liters': float(liters.group(1)) if liters else np.nan,
        'cylinders': float(cyl.group(1)) if cyl else np.nan,
        'is_electric': is_electric,
        'is_turbo': is_turbo
    })

engine_features = df['engine'].apply(parse_engine)
df = pd.concat([df, engine_features], axis=1)
```
