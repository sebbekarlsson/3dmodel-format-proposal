# 3D model file format proposal
> This can be seen as a better version of
> the famous [Wavefront .obj format](https://en.wikipedia.org/wiki/Wavefront_.obj_file).  
> The advantages of this format is that it can be parsed a lot quicker, and it
> only includes the data that is actually interesting.

## The format
> Here is my proposal:

    vx  vy  vz  vnx vny vnz tx  ty 

    1.0 1.0 0.0 3.5 2.5 1.0 0.0 1.0
    3.0 0.2 1.5 1.0 1.0 0.0 0.0 1.0
    4.0 1.0 3.0 0.0 1.0 0.0 0.0 1.0
    ...

> Here is a little description of all the values:  
> **vx**:   _This is the x position of the vertex._  
> **vy**:   _This is the y position of the vertex._  
> **vz**:   _This is the z position of the vertex._  
> **vnx**:  _This is the x vertex normal._  
> **vny**:  _This is the y vertex normal._  
> **vnz**:  _This is the z vertex normal._  
> **tx**:   _This is the x texture coordinate._  
> **ty**:   _This is the y texture coordinate._

> One might also want to include RGB values in this format, but one might
> also think that it is not very interesting, but here is how that would look:

    vx  vy  vz  vnx vny vnz tx  ty  r   g   b

    1.0 1.0 0.0 3.5 2.5 1.0 0.0 1.0 255 255 255
    3.0 0.2 1.5 1.0 1.0 0.0 0.0 1.0 255 255 255
    4.0 1.0 3.0 0.0 1.0 0.0 0.0 1.0 255 255 255
    ...

> Now, of course; the first row in these examples would not be included, and
> this is how it actually would look like:

    1.0 1.0 0.0 3.5 2.5 1.0 0.0 1.0 255 255 255
    3.0 0.2 1.5 1.0 1.0 0.0 0.0 1.0 255 255 255
    4.0 1.0 3.0 0.0 1.0 0.0 0.0 1.0 255 255 255
    ... 

### One model per file
> This format also follows a "one model per file" philosophy, the
> _Wavefront .obj_ format does not do this, and it makes things confusing.

### Materials
> For materials, we basically use the same syntax as in the `.obj` format, but
> _slightly different._  

> To reference a .mtl file we write it like this in the top of our file:

    mtllib "<filename>"

> The main difference here comparing to the `.obj` format, is that we use
> _quotes_ around the filename.

> To set the material for some faces we do it like this, right before we define
> faces:

    usemtl "<material name>"

    1.0 1.0 0.0 3.5 2.5 1.0 0.0 1.0 255 255 255
    3.0 0.2 1.5 1.0 1.0 0.0 0.0 1.0 255 255 255
    4.0 1.0 3.0 0.0 1.0 0.0 0.0 1.0 255 255 255
    ...  

> Again, here we use quotes around the material name.

### Full example
> Here is a full example of how one of these files could look like:

    mtllib "materials.mtl"

    usemtl "shiny"
    1.0 1.0 0.0 3.5 2.5 1.0 0.0 1.0 255 255 255
    3.0 0.2 1.5 1.0 1.0 0.0 0.0 1.0 255 255 255
    4.0 1.0 3.0 0.0 1.0 0.0 0.0 1.0 255 255 255
    ...

    usemtl "matte"
    2.0 1.0 0.0 3.5 2.5 1.0 0.0 1.0 255 255 255
    4.0 0.2 1.5 1.0 1.0 0.0 0.0 1.0 255 255 255
    5.0 1.0 3.0 0.0 1.0 0.0 0.0 1.0 255 255 255
    ...  
