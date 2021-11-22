# Pychet Labeller
A python based annotation/labelling toolbox for images. The program allows the user to
annotate individual objects in images.

## Annotation variants
Currently the pychet labeller supports **Circle Annotation** and **Rectangle
Annotation**.

The circle annotation enables the user to annotate objects in an image with its centroid and its radius. This makes the
annotation toolbox particularly suitable for round objects such as fruits, balls, coins etc.

The rectangle annotation annotates a box with top left position and its width
and height. This is more standard to what is used in the ML community where a
bounding box is scribed around objects.

## Why this toolbox
There are other examples out there (which also use PyQt) for labelling images.
Generally I found that they offered a lot of flexibility in the types of annotations
that could be done. However, this also meant that labelling very basic things
was very slow. For example, many tools allow you to annotate the vertices of
polygons and then type in the object name. However, the dataset I created this
for contained circular objects. All I wanted was to annotate a centroid and
object radius. For the rectangles, I didn't want to click on the vertices, which
can be difficult for complex shaped objects.

Additionally, I wanted a toolbox where you could see your bounding box/bounding
region live while moving the mouse around. And wanted some simple shortcuts to
changes its size and change the labelling output. Pychet Labeller aims to
address these features.

## Prerequisites
```    
sudo apt-get install libgeos-dev libgeos++-dev python-pip python2.7-dev libxext-dev python-qt4 qt4-dev-tools build-essential
sudo -H pip install -U svgwrite shapely simplejson
```
## Installation
1. Install prerequisites (svgwrite)
2. Clone this repository
```
git clone https://github.com/acfr/pychetlabeller.git pychetlabeller
```
3. Build and install
```
python setup.py build && sudo python setup.py install
```


## Usage
### Circle labelling toolbox
    python -m pychetlabeller <img dir> <label dir> --tool <circle | rectangle> --labelmap <labelmap.json>

See src/pychetlabeller/sample_labelmap.json for example labelmap file

### Labelling multiple images
Pychet Labeller makes it very easy to label a group of images in a folder, one
after the other. Simply run the labeller and open up the images directory form the push button on
the top right.

Annotations are made by simple clicking on the image. The user has the option to
move the image, change the size of the annotation tool, zoom in/out of the
image, change the object label, save the label or go to the next image. Press F1
to view the shortcuts for these things.

For circles, the size is the radius, and for rectangles, the size is the width
and height.

A few notes:
* Currently the program will automatically detect any files with extensions: png, jpg, , jpeg, tiff, bmp
* When labelling multiple images, can enable save_label to automatically save
  the labels - otherwise press ctrl-x to save current annotations
* Individual annotations can be deleted by selecting them on the table (or shift clicking on the image) and
  pressing delete.
* Backspace deletes the last annotation added

### Annotations
The annotations are saved in csv format with the same name as the input image
file. The csv entries for circles are *item, centre-x, centre-y, radius, label id*. The csv entries for rectangles are *item, topleft-x, topleft-y, width, height, label id*. 
The annotations are also automatically saved in .svg format

By default the annotations are saved in the image parent directory under a new
folder: labels. The user can choose to manually set a different folder
for the labels.

### Single images
We can also edit objects/object_labeler.py to quickly label one image. Under the object
MainWindow, uncomment self.quickview(), then under function quickview() set your image path.

## Future work
Extentions to labeller - coming soon:
* Currently can choose only one or the other - circles or rectangles - due to strict csv format. Should resort to svg only format and save all shapes
* Add generic polygon shape - and test other shapes
* Change brightness and contrast sliders to levels slider. Allows for much better control of the image contrast

## Bugs
Please contact author to report bugs @ bargoti.suchet@gmail.com

## Qt6 and Python 3.8.10
Calls to the classes were adapted for PyQt6, the adaptation carried out has been used as a point of comparison
by ramon.morros@upc.edu at https://github.com/imatge-upc/pychetlabeller . Calls to signals and slots changed.
Fixed code to bring it closer to pythonic notation. 
Contact juancarlos.miranda@udl.cat for bugs in Qt4 --> Qt6 conversion

###Install in Ubuntu 20.04.03 LTS
```
sudo apt-get install python3-pip
sudo pip3 install virtualenv
source ./venv/bin/activate
pip install --upgrade pip
pip install -r requirements_linux.txt
```

###Install Windows
TODO:


