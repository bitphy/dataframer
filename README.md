<img src="images/logo_small.jpg" height=110>

# Dataframer by [Bitphy](https://bitphy.com)

A small library for creating pandas DataFrame fixtures.

========

<img src="images/logo_small.jpg" height=110>

When testing with pandas dataframe, to generate easily fixture use this library

# The problem: how do we generate pandas DataFrame fixtures?

To manually define dataframe fixtures in python you have to do things such as:

```python 
import pandas as pd
from pytest import fixture

@fixture
def df():
    d = {
        'a': [1, 2, 3],
        'b': [5, 6, 7],
    }
    return pd.DataFrame(d)
``` 

Which generate a fixture dataframe that looks like:

a | b
--|--
1 | 5
2 | 6
3 | 7

Nevertheless, this method is slow to write, naughty and does not 
allow you to define many rows or cases in an acceptable time.


# Solution

Dataframer allows you by passing a dictionary of columns and its dtypes
generate a fixture dataframe that fulfills what you want.

Plus, as far as you use the same seed when you initialize the class the 
fixture is consistent, namely, is always the same dataframe while the call
inputs are the same.


# Examples

```python
from dataframer import DataFrameMaker

maker = DataFrameMaker()
df = maker.make_df(nrows=5)
```

yields

index |id
------|-------
0     | 98539
1     | 77708
2     | 5192
3     | 98047
4     | 50057


```python
from dataframer import DataFrameMaker

maker = DataFrameMaker()

df = (
    maker
    .make_df(nrows=3, 
             cols={
                'a': 'str', 
                'b': 'float', 
                'c': 'int'
             }
        )
    )
```

a | b | c
--------------|--------------|--------------
LRmijlfpaqbmhT |  1.624345 |  98539
8gzYuLsul8QCDo | -0.611756 |  77708
YexxPX3EGwnPjh | -0.528172 |   5192


### License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
