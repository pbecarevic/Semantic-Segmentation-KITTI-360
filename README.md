# Semantic-Segmentation-KITTI-360


### 1.

To begin download the available 2D semantic segmentation images and masks from http://www.cvlibs.net/datasets/kitti-360/download.php
NOTE: you will need to download the 128 GB test and validation data in addition to the test data and the semantic 2D data.

### 2.

We must do some data preprocessing before we load the data into PyTorch's Dataset class due to the nature of the directories

We will not be using the folder named image_01 in each drive and the folder in each drive can be removed.

format for the folder is `2013_05_28_drive_00XX_sync/image_01`

### 3.

Next we must parse through the raw images and make sure to locate the raw images that are corresponding to the train and val masks in the `2013_05_28_drive_train_frames.txt` file

We can do that with the `File_Parsing_KITTI.ipynb` using pandas

Moving the masks does not need to be done unless the number of raw_images ≠ number of masks after all raw images have been parsed which should not be the case.

### 4.

The shell file `rename.sh` contains code that can be run at the top level directory within the dataset for both the train/val raw images and the train/val masks

```
find -name '*.png' | sort -n | # find pngs
gawk 'BEGIN{ a=1 }{ printf "mv %s %04d.png\n", $0, a++ }' | # build mv command
bash
```

This script will look through the subfolders in order and move the images to the top level folder and number the images in order from 1 to the last image number

This ensures that the order of the train/val raw images does not change so that the corresponding train/val masks are still mapped correctly
