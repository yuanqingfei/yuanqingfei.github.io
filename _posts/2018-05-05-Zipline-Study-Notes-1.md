---
published: false
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

```bash
sudo pip install pyfolio

```