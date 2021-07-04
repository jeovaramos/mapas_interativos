# Interactive maps with folium and geobr packages

## Download dataset
First of all, get the districts map. When you download it from geobr package, it comes for all over the contry. So you will need to subset it for your interesting region. In this case, I choosed São Paulo city.

```
bairros = geobr.read_neighborhood(verbose=True)
bairros = bairros[bairros['name_muni'] == 'São Paulo']

escolas = geobr.read_schools()
escolas = escolas[escolas['name_muni'] == 'São Paulo']
```

The schools dataset is a real large one. Perhaps it longing a while until the download is done. Then, subset again. Note tha I always take a look in the column's types. I Think it is a good practice. You can antecipate some problems and avoid some unacessary frustration further.

## Data preparation
All right, whith the data in your hands, lets do some stuff first. In the school dataset, the geometry field indicates a Point (yes, with capitalized P). Let's separate it in two columns: longitude and latitude with a simple lambda function.

But if you examine row by row, you may notice that we're not in plenty luck with this dataset. Some geometry Points are empty. And, with a great regret, we'll need to trash those out away. You can take a minute if you need it. I totally got you.

And with the data ready, now let's put our hands on the map. But first, make sure when you plotting it appears right on the center of the screen. For that, take the longitude and latitude medians.

```
escolas['lon'] = escolas.geometry.apply(lambda p: p.x)
escolas['lat'] = escolas.geometry.apply(lambda p: p.y)

escolas = escolas[~escolas['lat'].isnull()]

x = escolas['lon'].median()
y = escolas['lat'].median()
```

## The first map

The first map will be a simple one. Just with the district. The steps are:

1. Create your base map setting the center and the default zoom.
2. Bind the data containded in the Geo Data Frame.
3. Add it to your base map.
4. Plot it. :)

For more details about plot, please check the jupyter notebook file.
Thanks for reading.
Best regards.
