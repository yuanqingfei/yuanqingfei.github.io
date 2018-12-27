---
published: true
categories: technique
tags: zipline pyfolio finance trading
---
Update on 201181227
re-install the zipline based on Unbuntu 18.04

## Steps:

### Install:

```bash
sudo pip uninstall zipline
sudo apt install python3-pip
sudo pip3 install zipline

QUANDL_API_KEY=[QUANDL_KEY] zipline ingest -b quandl
```

### Run:

```bash
zipline run --bundle quantopian-quandl -f buyapple.py -s 2016-01-01 -e 2018-12-01 -o apple.pickle
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

目前遇到一个问题就是zipline和pyfolio使用的[pandas版本不兼容](https://github.com/quantopian/zipline/issues/2132)。需要在不同的环境下运行才可以。[这里](https://github.com/quantopian/pyfolio/issues/407)也有记录。
