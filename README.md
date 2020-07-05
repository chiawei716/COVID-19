# COVID-19 Feature Detection


---

<!-- #region -->
## Installation

### 1. install dependecies

`
$ sudo apt-get update
`

`
$ sudo apt-get install libopencv-dev
`


`
$ pip install -r requirement.txt
`

### 2. Clone Yolo-v4

`
$ git clone https://github.com/AlexeyAB/darknet.git & cd darknet/
`

### 3. Edit Makefile of Darknet repo
Set GPU. CUDNN. CUDNN_HALF. OPENCV to 1

### 4. Build
`
$ make
`
<!-- #endregion -->

## Data pre-processing

### Generate dataset for Yolo-v4

Yolo requires training datasets with images which have their annotation text files in the same directory.<br>
And annotations are writen in seperate lines, in the format:<br>
`
[class] [X center] [Y center] [Width] [Height]
`
<br>

Please follow .ipynb files below to get it ready:<br>
a. [Download Data](download_data.ipynb)<br>
b. Generate annotation files<br>
   1. with data augmentation:<br>
   [Generate augmentation data & Split training and validation data](gen_data_augmentation.ipynb)<br>
   [Shuffle data](train_valid.ipynb)<br>
   
   2. original data:<br>
   [Generate .txt annotation files](gen_yolo_annotation.ipynb)<br>
   [Split training and validation data & generate .data .names files](split_train_valid.ipynb)<br>
   
c. Move our config file to the cfg directory (from root directory of this repo)<br>
    `
    $ cp ./COVID19.cfg ./darknet/cfg/COVID19.cfg
    `




## Start training 
    | at darknet/ directory 

Without pre-trained weights:<br>
`
$ ./darknet detector train data/COVID19.data cfg/COVID19.cfg -map -dont_show 2>/dev/null
`

Apply pre-trained weights:<br>
`
$ ./darknet detector train data/COVID19.data cfg/COVID19.cfg [filename.weights] -map -dont_show 2>/dev/null
`

If you want to use our pre-trained weight, please enter this command:<br>
`
$ cp ../COVID19_best.weights backup/COVID19_best.weights
`


## Test single image
`
$ ./darknet detector test data/COVID19.data cfg/COVID19.cfg backup/COVID19_best.weights
`

We also wrote a jupyter notebook for [single image testing](display_test_result.ipynb).


## Compute mAP
`
$ ./darknet detector map data/COVID19.data cfg/COVID19.cfg backup/COVID19_best.weights
`


```python

```
