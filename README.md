# Team A2 BD4H project

## Prerequisites
Refer to the `requirements.txt` file.

## Data
Used a set of pediatric Chest X-ray images publicly available from:

Kermany, D.S.; Goldbaum, M.; Cai, W.; Valentim, C.C.S.; Liang, H.; Baxter, S.L.; McKeown, A.; Yang, G.; Wu, X.; Yan, F.; et al. Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning. Cell 2018, 172, 1122–1131.

## ROI segmentation
The CXRs contain regions other than the lungs that are not useful for diagnosing pneumonia.
The methodology presented in this project uses an algorithm based on anatomical atlases to automatically
detect the region that encompass the lungs in the CXRs, and then crop the image to only include the
lungs region and resample to 1024x1024 pixel dimensions. The source code for the same can be found at 
https://ceb.nlm.nih.gov/proj/tb/Segmentation_Module_Version_2017_11_04.zip.

## Instructions
1. Download the CXRs, and use the ROI segmentation algorithm to pre-process the data.
2. Place the images in the data folder using the following folder structure:
`data/train/NORMAL`, `data/train/PNEUMONIA`, `data/test/NORMAL`, `data/test/PNEUMONIA`.
3. Run `train_augmentation.py`, it will generate some additional images for `data/train/NORMAL`.
The goal of this step is to balance class distribution in the data.
4. Train the binary classification model (Normal vs Pneumonia) using the notebook `resnet50_training.ipynb`.
5. Extract the features of the model from the previous step using `etl_extract_features.ipynb`
6. Train the multi-class classification model (Normal vs Viral vs Bacterial) using the features
extracted in the previous step. The code for this step is in `multi_class_model_train.ipynb`

Both notebooks used on step 4 and 6 to train the models include the computation of the
performance metrics.


## Code references:
1. https://github.com/mdbloice/Augmentor
2. https://github.com/sivaramakrishnan-rajaraman/Visualization-of-CNN-toward-Pneumonia-Detection-in-CXRs
3. https://lhncbc.nlm.nih.gov/LHC-downloads/downloads.html#chest-x-ray
4. https://keras.io/guides/transfer_learning/
5. https://docs.databricks.com/_static/notebooks/deep-learning/deep-learning-transfer-learning-keras.html
6. https://github.com/tntn123/spark_transferlearning/blob/main/main.py
