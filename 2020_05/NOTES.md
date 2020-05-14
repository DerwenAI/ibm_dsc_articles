```
sudo apt-get update
sudo apt-get install emacs25-nox unzip lynx
sudo apt-get install virtualenv python-pip python-dev python3-dev
sudo apt-get install libproj-dev proj-data proj-bin
sudo apt-get install libgeos-dev
sudo apt-get install libspatialindex-dev

virtualenv -p python3 ~/venv
source ~/venv/bin/activate

pip install -r requirements.txt

pip install shapely --no-binary shapely 
pip install git+https://github.com/SciTools/cartopy.git --no-binary cartopy
pip install pysal --no-binary pysal

pip install geopandas
pip install geoplot
```

```
# https://towardsdatascience.com/walkthrough-mapping-basics-with-bokeh-and-geopandas-in-python-43f40aa5b7e9
# https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.html
# https://www.census.gov/newsroom/press-kits/2018/pop-estimates-national-state.html

wget https://www2.census.gov/geo/tiger/GENZ2018/shp/cb_2018_us_state_20m.zip

mkdir maps
pushd maps
unzip ../cb_2018_us_state_20m.zip
popd

wget http://www2.census.gov/programs-surveys/popest/datasets/2010-2018/national/totals/nst-est2018-alldata.csv
mv nst-est2018-alldata.csv data
```

```
jupyter lab --no-browser --port=8888 --ip=0.0.0.0
```


```
wget https://ihmecovid19storage.blob.core.windows.net/latest/ihme-covid19.zip
unzip ihme-covid19.zip 
mv 2020_*/Hospitalization_all_locs.csv data
```
