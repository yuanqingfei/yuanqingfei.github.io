---
published: false
---

## Steps:

### Install:

```bash
pip install zipline
sudo apt-get install libatlas-base-dev python-dev gfortran pkg-config libfreetype6-dev

QUANDL_API_KEY=[QUANDL_KEY] zipline ingest -b quantopian-quandl
```

### Run:

```bash
zipline run --bundle quantopian-quandl -f buyapple.py --start 2016-01-01 --end 2018-01-01 -o apple.pickle
```

### Plot:

```python
>>> import pandas as pd
>>> perf = pd.read_pickle('apple.pickle')

```