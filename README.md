# DeepSeaAI
## Pipeline used for the cleaning and analysis of citizen science data with AI.

This markdown will list the basic requirements and knowledge you need for the cleaning/analysis of citizen science data. It has been first developed with the intent to deal with DeepSeaSpy data (accessible from : https://ocean-spy.ifremer.fr/). 

### Contents
You should have 1 python file, a Jupyter notebook and a markdown file (download here):

```
DeepSeaAI
├── README.md                <- **You are here**
├── requirements.txt            <- Necessary files for the cleaning/installation of Yolov8 (will soon be added)
├── Functions.py            <- Functions used for the cleaning/analysis.
├── Notebook.ipynb          <- Ready-to-use jupyter notebook. 
├── Pipeline_txt.py         <- Ready-to-use python script. Same as the Notebook, but does everything in a single go.
├── config.txt              <- Config file to tweak the Pipeline_txt.py arguments.
```

## Prerequisites
We recommend you to build a virtual environnement for all the necessary packages of this project.
An easy way to do so is to use
```
pip install requirements.txt
```
### Default settings/parameters

We manually set some settings at default values. If you need more insights on their use and where to modify them, we provided where to find them in the notebook.

lines2bb --> Z = 5



It's best that your dataset has the following information:

name_img|species|xmin |ymin |xmax |ymax |
--------|-------|-----|-----|-----|-----|
4366.jpg|buccin |972  |982  |549  |559  |

If you want to calculate your x/y min/max, it is possible. You should at least have your coordinates like this :

|x1 |y1 |x2 |y2 |
|---|---|---|---|
|761|451|859|364|


The pipeline expects image resolution of 1920x1080. You can input images with a different size by changing width_images and height_images in the beginning of Functions.py. If you have images of varying resolutions, you can modify the functions so that they take in the type of image you have.

To obtain it for each image, you can use this bit of code :

```
path_img=r'/path/to/img'
im=Image.open(path_img) 
w= int(im.size[0])
h= int(im.size[1])
```


**Functions** contains all the functions needed for the cleaning and analysis of citizen science datasets. Detailed explanations of the functions are to be found here. You can modify them and use them as the basis for your work. There are also functions that are useful just for the exploration of your dataset.

**Notebook** is a ready-to-use file that you can change based on your needs/dataset. 

## Function details

Here you will find functions that were developed in the Functions.py, You may find those useful depending on your needs/study case. Their explanation are not covered in the Notebook file.

### Vision 
Function that can be used to visualize your bounding boxes on your images.

You need to enter the colors you want for the bounding boxes, in the form of a dictionary :

```
# Colors are in Blue Green Red
colors = {
        'Autre poisson': (0, 0, 255),  # Red
        'Couverture de moules': (255, 0, 0),  # Blue
        'Couverture microbienne': (0, 255, 0),  # Green
        'Couverture vers tubicole': (255, 255, 0),  
        'Escargot buccinidé': (0, 0, 255),  
    }

vision(path_img,df,colors)

```
This function copies all of the images corresponding to the one present in path_img, and draws the bounding boxes present in the dataframe. We recommend 
There is also **plot_line** and **plot_bb** that can be used to visualize specific bounding boxes. They are useful for debugging, they don't generate/copy images and can be

### Check_img
Function that returns image names present in the dataframe but not in the images folder. Useful to know the reality in your dataset.





