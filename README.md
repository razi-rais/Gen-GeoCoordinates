# Geo Coordinates Generator
Python script to generate random geo-coordinates based on country codes based on [Faker](https://faker.readthedocs.io/en/master/fakerclass.html) library.

### Install Faker
```
pip install Faker
```

### Generate Geo-Coordinates 

```
from faker import Faker
fake = Faker()
Faker.seed(0)

lat_log = []
counter = 0 ;
countries = ['US', 'GB', 'AU', 'IN'] # Available locales: https://faker.readthedocs.io/en/master/locales.html
total = 10 #You can also use Panda's Dataframe len(df)
size = total / len(countries) -1
country = -1
for _ in range(total):
    if counter >= size:
        counter =0
        country = country + 1
        #print (countries[country])
    lat_log.append(fake.local_latlng(country_code= countries[country]))
    counter = counter + 1 

```
### Print Geo-Coordinates 
```
[('Latitude: (' + lat_log[_][0] + ') | Longitude:(' + lat_log[_][1] + ") | Country:(" + lat_log[_][3] + ")" ) for _ in range(total)] 
```
```
['Latitude: (25.75728) | Longitude:(75.37991) | Country:(IN)',
 'Latitude: (27.9247) | Longitude:(78.40102) | Country:(IN)',
 'Latitude: (30.17746) | Longitude:(-81.38758) | Country:(US)',
 'Latitude: (41.72059) | Longitude:(-87.70172) | Country:(US)',
 'Latitude: (51.65) | Longitude:(-0.2) | Country:(GB)',
 'Latitude: (53.0233) | Longitude:(-1.48119) | Country:(GB)',
 'Latitude: (-33.79176) | Longitude:(151.08057) | Country:(AU)',
 'Latitude: (-25.54073) | Longitude:(152.70493) | Country:(AU)',
 'Latitude: (10.10649) | Longitude:(76.35484) | Country:(IN)',
 'Latitude: (17.54907) | Longitude:(82.85749) | Country:(IN)']
```

## Using with Pandas

```
import pandas as pd
df = pd.DataFrame(lat_log)
```

```
df.head()
```

```

25.75728	75.37991	Deoli	IN	Asia/Kolkata
27.9247	  78.40102	Chharra	IN	Asia/Kolkata
30.17746	-81.38758	Palm Valley	US	America/New_York
41.72059	-87.70172	Evergreen Park	US	America/Chicago
51.65	    -0.2	Barnet	GB	Europe/London
```

### Plot Geo-Coordinates on the World Map
```
pip install geopandas

```

```
import plotly.express as px
import plotly.graph_objects as go
import geopandas as gpd

fig = go.Figure(data=go.Scattergeo(
        lon = df[1],
        lat = df [0],
        text = df [3],
        mode = 'markers',        
        ))
fig.update_layout(
        title = 'Map',
    )
fig.show()
```

![image](https://user-images.githubusercontent.com/7940117/122821438-d8e39980-d2aa-11eb-8dbb-695b2d291647.png)

