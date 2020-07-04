# pynse

Library to extract realtime and historical data from NSE website.EOD data like bhavcopy and option chain are also saved to directory. First run will create directories for storing the data and will download the index symbols.

## Installation

This module is installed via pip:

```
pip install pynse
```

### Prerequisites

Python 3.6


## Using the API

### Overview
There is only one class in the whole library `Nse`. 

### Logging
The whole library is equipped with python's `logging` moduele for debugging. If more debug information is needed, enable logging using the following code.

```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

```python
from pynse import *

# path where data will be stored
datapath='C:/Users/goldFisher/pynse'

nse=Nse(path=datapath)
```
make sure datapath is absolute otherwise it will create data folders in every run

### Get Market Status

```python
nse.market_status()
```

### Get Symbol Information
```python
nse.info('SBIN')
```

### Get Quote
Get realtime quote for EQ, FUT and OPT. If no expiry date is provided for derivatives, returns date for nearest expiry.

for cash
```python
nse.get_quote('RELIANCE')
```
for futures
```python
nse.get_quote('TCS', segment=Segment.FUT, expiry=dt.date( 2020, 6, 30 ))
```
for options
```python
nse.get_quote('HDFC', segment=Segment.OPT, optionType=OptionType.PE)
```

### Bhavcopy for Cash
download bhavcopy from nse
or
read bhavcopy if already downloaded

```python
nse.bhavcopy()
``` 
or
```python
nse.bhavcopy(dt.date(2020,6,17))
``` 

### Bhavcopy for F&O
download bhavcopy from nse
or
read bhavcopy if already downloaded
```python
nse.bhavcopy_fno()
```
or 
```python
nse.bhavcopy_fno(dt.date(2020,6,17))
```

### Pre Open data
get pre open data from nse
```python
nse.pre_open()
```

### Option Chain

Downloads the option chain or reads if already downloaded.
if req_date is not specified returns latest available option chain from nse website

This returns dictonary containing
timestamp as str
option chain as pd.Dataframe
expiry_list as list
```python
nse.option_chain('INFY')
```
or
```python
nse.option_chain('INFY',expiry=dt.date(2020,6,30))
```

### FII and DII Data
get FII and DII data from nse
```python
nse.fii_dii()
```

### Historical Data
get historical data from nse
symbol index or symbol
```python
nse.get_hist('SBIN')
```
or
```python
nse.get_hist('NIFTY 50', from_date=dt.date(2020,1,1),to_date=dt.date(2020,6,26))
```

### Realtime Index
Get realtime index value
```python
nse.get_indices(IndexSymbol.NiftyInfra)
```
or
```python
nse.get_indices(IndexSymbol.Nifty50)
```

### Top Gainers and Losers
presently works only for SECURITIES IN F&O

```python
nse.top_gainers(10)
```
or
```python
nse.top_losers(10)
```
### Update Symbol Lists
Update list of symbols.No need to run frequently, its only required when constituent of an index is changed or list of securities in fno are updates

```python
nse.update_symbol_list()
```

## License

© 2020 Anoop Jangra

This repository is licensed under MIT license.
See LICENSE for details.
