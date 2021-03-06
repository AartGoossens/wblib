# wblib

Wblib offers a set of tools to work with Wattbike data. Wattbike session data can be downloaded directly from the Wattbike Hub.

## Installation
The easiest way to install wblib is via `pip`:
```
pip install wblib
```
Otherwise you can clone this repository:
```
git clone git@github.com:AartGoossens/wblib.git
```

## Example usage
Start with importing WattbikeDataFrame:
```python
from wblib.models import WattbikeDataFrame
```

If you are running this code from a Jupyter Notebook, run this code to show the plots inline:
```python
%matplotlib inline
```

Then finally, these lines are all you need to get all data from a Wattbike session:
```python
wdf = WattbikeDataFrame().load('LYPWXEjF9B')
```
...where `LYPWXEjF9B` is the session id from a Wattbike session that your can retrieve from the session page on the Wattbike Hub.

`wdf` is a WattbikeDataFrame, a sub class of [Pandas](http://pandas.pydata.org/) `DataFrame` so all features of a Pandas `DataFrame` are available. In addition, some Wattbike specific features are added.

To plot the average polar plot of the session:
```python
wdf.plot.polar()
```
![Image of polar plot](docs/resources/polar_plot.png)

It is also possible to plot all revolutions in the same plot:
```python
wdf.plot.polar(full=True)
```
![Image of polar plot full](docs/resources/polar_plot_full.png)

...even without the mean polar plot:
```python
wdf.plot.polar(full=True, mean=False)
```
![Image of polar plot full without mean](docs/resources/polar_plot_full_without_mean.png)

To plot the power output during the session:
```python
wdf.power.plot()
```
![Image of power plot](docs/resources/power_plot.png)

To make a scatter plot of e.g. power and right_max_angle:
```python
wdf.plot.scatter(x='power', y='right_max_angle')
```
![Image of scatter polot](docs/resources/scatter_plot.png)

To calculate the average power, standard Pandas syntax is used:
```python
wdf.power.mean()
>> 206.10530695107892
```

It is also possible to do analyses on asubset of the data, again in a Pandas-like way. For example, it is possible to plot the mean polar view for all revolutions over 400 Watt:
```python
wdf.loc[wdf.power > 400].plot.polar()
```
![Image of polar plot over 400 Watt](docs/resources/polar_plot_gt_400.png)

To retrieve all workouts from an in a certain date range (depending on the number of workouts this can take a while):
```python
import datetime
wdf = WattbikeDataFrame().load_for_user(user_id='u-1756bbba7e2a350', after=datetime.datetime(2017, 1, 1), before=datetime.datetime(2017, 3, 1))
```

It is also possible to add an extra session to an already existing wdf by using the aforementioned `load` method:
```python
wdf = wdf.load('Gbf8NgdcjH')
```

If you are working with a WattbikeDataFrame with multiple sessions you can make your dataset more manageable by averaging all the data per session:
```python
wdf.average_by_session()
```

## License
This library is licensed under a MIT license. See [LICENSE](LICENSE).

## To do
- [x] Add support for multiple sessions in a single WattbikeDataFrame
- [x] Make it possible to plot all revolutions in a single polar plot
- [ ] Add import of .wse files

Feature request? Create an issue!
