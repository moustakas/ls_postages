# Legacy Surveys galleries generator

This repository contains a script to generate galleries of the Legacy Surveys images in the form of postage images in html format. Images are taken from the Sky viewer (https://www.legacysurvey.org/viewer) of the official Legacy Surveys webpage.


## Usage
At first instance, only coordinates (in the form of `RA` and `DEC`), indexes of centred targets and image layer(s) such as raw, model or residual, are needed to run the script, however, it's possible to include more parameters if passed throughout the `info` input that appears as tooltips for each target.

Make sure you have bookeh installed.

```python
from main import html_postages

#
dr = 'dr8'
survey = 'south'
layer_list = ['%s-%s' %(dr, survey), '%s-%s-model' %(dr, survey), '%s-%s-resid' %(dr, survey)]
coord = [dr8['RA'], dr8['DEC']]
idx = list(np.where((bgs_any) & (dr8['RMAG'] < 16)))[0]

#
html_postages(coord=coord, idx=idx, layer_list=layer_list)
```
Further options included are saving the html file with `savefile`, make classifications (e.g., BGS or not BGS target) with `veto`, add more information for each target besides possitions (`RA` and `DEC`) with `info`, define grid size of postage images gallery with `grid`, choose postage boxsize in degrees with `m` and `radius` and other useful input parameters to add some text to html page and to save multiple galleries in one html page using tabs (examples below).

A more complete example is shown below.

```python
from main import html_postages

#
bgs_any = ((dr8['BGSBITS'] & 2**(20)) != 0)
dr = 'dr8'
survey = 'south'

#script input parameters
veto = {'BGS':(bgs_any),'Not BGS':(~bgs_any)}
info_list = ['RA', 'DEC', 'RMAG', 'GMAG', 'ZMAG', 'TYPE']
info = {key:dr8[key] for key in info_list}
layer_list = ['%s-%s' %(dr, survey), '%s-%s-model' %(dr, survey), '%s-%s-resid' %(dr, survey)]
coord = [dr8['RA'], dr8['DEC']]
idx = list(np.where((bgs_any) & (dr8['RMAG'] < 16)))[0]
title = 'Title of gallery'
main_text = 'Main text to describe gallery'
buttons_text = 'select which images and object \n markers you want to display'
grid = [4,4]
savefile = 'example_gallery'

#
html_postages(coord=coord, idx=idx, veto=veto, info=info, grid=grid, layer_list=layer_list, title=title, 
              main_text=main_text, buttons_text=buttons_text, savefile=savefile)

```
For a more complete examples see `examples.ipynb`.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
