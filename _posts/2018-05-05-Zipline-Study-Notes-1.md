---
published: false
categories: technique
tags: zipline pyfolio finance trading
---

## Steps:

### Install:

```bash
sudo apt-get install libatlas-base-dev python-dev gfortran pkg-config libfreetype6-dev
sudo pip install --upgrade setuptools
sudo pip install zipline

QUANDL_API_KEY=[QUANDL_KEY] zipline ingest -b quantopian-quandl
```

### Run:

```bash
zipline run --bundle quantopian-quandl -f buyapple.py --start 2016-01-01 --end 2018-01-01 -o apple.pickle
```

### Plot:

[pyfolio](https://quantopian.github.io/pyfolio/notebooks/zipline_algo_example/#extract-metrics)

```bash
sudo pip install pyfolio
sudo apt-get install python-tk
```

```python
import pyfolio as pf
import pandas as pd

results = pd.read_pickle('apple.pickle')
returns, positions, transactions = pf.utils.extract_rets_pos_txn_from_zipline(results)
pf.plot_drawdown_periods(returns, top=5).set_xlabel('Date')

```

目前遇到一个问题就是zipline和pyfolio使用的[pandas版本不兼容](https://github.com/quantopian/zipline/issues/2132)。需要在不同的环境下运行才可以。
