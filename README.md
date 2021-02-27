# Lattice.py
#### Version 2

Lattice.py is a python module created to produce 2D and 3D lattices. It can produce lattices of equal spheres with several kinds of geometric arrangements. Currently supported lattice types are:  
- Hexagonal close-packing (hcp; abab)
- Face-centered cubic packing (fcc; abcabc)
- Simple cubic packing (scp)
- Body-centered cubic packing (bcc)

Several shapes of lattice layers can be used and are made 3D by stacking multiple layers on top of each other according to the packing arrangement. Current available shapes are:
- Circle
- Hexagon
- Rectangle

Current functionality allows you to generate the cartesian coordinates of a lattice and plot the lattice in 2D and 3D.

### Using Lattice.py
#### Importing and initializing a lattice
To initiate a lattice, first make sure lattice.py is located in the directory you are working in and use an import statement. Then you can generate a lattice by calling the Lattice( ) class. For example:  
```
import lattice at lt
lattice = lt.Lattice(**kwargs)
```

#### Class Attributes
- `name`: This is currently optional and can be whatever you want. The default is just `'lattice'`.
- `form`: This specifies the kind of packing. Options are `'hcp'` (default), `'fcc'`, `'scp'`, and `'bcc'`.
- `shape`: This specifies the shape of a lattice layer. Options are `'circle'` (default), `'hexagon'`, and `'rectangle'`.
- `n_layers`: The number of lattice layers stacked on top of each other. The default is `n_layers = 3`
- `layer_radius`: This attribute must be specified for circle and hexagon shapes. For circles, this is the radius of the circle in # of spheres. For hexagons, this is the circumradius/side length of the hexagon in # of spheres.
- `layer_dims`: This attribute must be specified for rectangular shapes. Provide a tuple in the form (x, y), where x and y are an integer number of spheres.

#### Class Methods
- `__init__(self, name='lattice', form = 'hcp', shape = 'circle', n_layers = 3, layer_radius = 0, layer_dims=(0,0))`: initialization function
- `layer_coords(self, layer, z=False)`: A function to return the coordinates of a specified layer. The `layer` argument is the index of the layer, starting at 0 and ending with `n_layers - 1`. The argument `z` specifies whether the z coordinates of the layer are returned or not. If `False`, a 2D array is returned with the x and y coordinates of the layer. If `True`, a 3D array is returned with the x, y, and z coordinates.
- `list_coordinates(self)`: A function that returns all of the coordinates of the lattice, including all of the layers. Use this if you need a list of all of the coordinates of sphere centers in the lattice.
- `mpl(self)`: This method will make a 2D plot of the lattice using matplotlib, showing all of the layers projected onto the xy plane.
- `k3d(self, point_size=.8, color = True)`: This will make a 3D plot of the lattice using k3d using the x, y, and z coordinates of all of the layers. `point_size` will adjust the size of the spheres in the lattice, and `color` will determine whether or not each layer of the lattice is in a different color.

#### Other Functions:
- `gen_coords(num=37, length=10)`: This function is used to generate the (x, y) coordinates for a hexagon-shaped layer of hcp/fcc lattice. This code was developed for earlier research by Kathryn Krycka, Ian Hunt-Isaak, and Yumi Ijiri.
    - `num_rings(num)`: Returns the number of rings in a hexagon of `num` spheres, rounded up if the number of points passed is not able to generate a complete hexagon. This is used by `gen_coords()` function.
    - `num_points(rings)`: This is the inverse of `num_rings`; it returns the number of points in a hexagon of `rings` rings.
- `cubic_packing_coords(layer_spacing=1, layer_radius=0, shape='circle', layer_dims=(0,0))`: This function is used to generate the (x, y) coordinates of a layer of scp/bcc lattice in any of the three shapes.
- `hexa_packing_coords(layer_spacing=1/(3**.5 * 2/3), layer_radius=0, shape='circle', layer_dims=(0,0))`: This function is used to generate the (x, y) coordinates of a layer of hcp/fcc lattice. It can generate in any of the three shapes, and it calls the `gen_coords()` function for hexagons.

#### Acknowledgements:
This module benefits from and makes use of code developed by Kathryn Krycka, Ian Hunt-Isaak, and Yumi Ijiri for previous research in modeling hcp lattices.

#### Changelog:
- Version 2 (26 Feb. 2021)
    - Added scp and bcc packing
    - Added circle and rectangle layer shapes
    - Reformated `layer_coords()` function
    - Updated attributes and added error warnings to the `__init__` method
- Version 1 (24 Feb. 2021)
    - WIP code to generate hexagon-shaped hcp and fcc lattices
    - 2D and 3D plotting capabilities using matplotlib and k3d
    - Ability to return all of the coordinates of the centers of spheres in a lattice