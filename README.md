# Dat255 Project – Computer Vision 

**Identifying Shipping Container IDs**

_Endre Johannesen Rossavik and Alexander Nordstrand_

## Introduction

Shipping containers are used globally to transport goods, by road, train or by sea. It is a massive logistic undertaking to make sure shipping containers and the goods within get to where they are supposed to go, within a reasonable time, for as little cost as possible. Global shipping is a competitive market where squeezing out every bit of added efficiency, and reduction of man hours, is very compelling.

Most shipping containers have a unique ID signature printed on all sides, the international standard for these signatures is the BIC-code but not all container owners follow these standards, but have a variety of their own ways to issue ID's for their containers. These codes could be identified by an AI model just from images of the containers. The containers have uneven surfaces, wear and tear (rust, dirt, dents) and varying ID locations and text directions which make the task more difficult. They can often contain other unimportant text as well, so the model needs to be able to locate the relevant text and read it accurately.

## Goals

- Investigate models and methods for extracting identification codes automatically from image data.
- Explore and compare solutions based on ready-made OCR technology vs a specially trained model for this specific purpose.
- Gain solid experience of the difficulties, challenges and pitfalls of extracting characters reliably from complex, imperfect real-life image data.
- Implement a prototype proof of concept solution that demonstrates the feasibility of the ID identification solution.
- 95+% accuracy for OCR on each container. Not necessary to acheive this immediately but but further develpment will be on whichever solution seems most promising. 

## Methods

Two different approaches that were investigated:

- Object detection to find the area of the container ID -> read the text from the cropped area by Tesseract OCR

  - Pros: ID detection is very simple and reliable. Uses industry tested technology. Huge access to guides and resources to acheive desired reults. Less dependant on large and varied trainingsets. 
  
  - Cons: Understadning how Tesseract works can be very esoteric, works well in some cases and not in others with no clear reason why. Preprocessing can be very timeconsuming to set up.
  

- Full object detection approach, find each individual char of the container IDs with object detection, then combine the detections into a full container ID String

  - Pros: Object detection seems to perform very well, seems like a clear path towards better container ID accuracy with more training data.
  
  - Cons: Requires a lot of training data and takes a lot of manual time to label (Potentially 11 bounding boxes of Chars per image)

## Demo


<p><small>Huggingface spaces demo of full object detection approach is <a target="_blank" href="https://huggingface.co/spaces/alenor/ContainerCodeV1"> available here</a>. </small></p>


## Results

- Object detection + tesseract:

ID detection very simple and reliable. Tesseract OCR not so reliable. Creating a preprocessing-pieline that reliably handles a large variety of images taken in a varying conditions seems almost impossible. Other OCR engines may be considered for further development. 

### Training Results

![Training Results](https://raw.githubusercontent.com/587763/Container-identification/main/reports/figures/TextDetectFigures/results.png)

### Confusion Matrix

test123
![Confusion Matrix](https://raw.githubusercontent.com/587763/Container-identification/main/reports/figures/TextDetectFigures/confusion_matrix.png)

### Test samples

![Test samples](https://github.com/587763/Container-identification/blob/main/reports/figures/TextDetectFigures/TesseractOCRResults.pdf)

- Full object detection:

The approach seems promising, the YOLOv8 object detection model seems to do well at finding the text characters that belong to the ID while ignoring other text on the container. The final trained "bestChar45.pt" gets about 70% correct container ID on the test set, and with post-processing of the output by, for example, comparing the predicted ID with a list of known possible IDs it could be, the final accuracy was 98%+ on the test set. The mistakes the model makes are quite understandable (sometimes confuses "1" and "I", "8" sometimes becomes two "0"'s etc). From the confusion matrix you can also observe that it does very poorly with "j", that is because that letter is severely underrepresented in the training data, because "j" is a reserved letter along with "U" and "Z" that signifies what type of contents a container has, and the training data for this model lacked the "j" type in particular. Perhaps with more training data and more training time, this approach could have results pushed even further.


### Training Results

![Training Results](https://github.com/587763/Container-identification/blob/main/reports/figures/bestChar45TrainingResults/results.png?raw=true)

### Confusion Matrix

![Confusion Matrix](https://github.com/587763/Container-identification/blob/main/reports/figures/bestChar45TrainingResults/confusion_matrix.png?raw=true)


## Conclusion



Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project using <a target="_blank" href="https://github.com/ultralytics/ultralytics">YOLOv8 model architecture</a>. </small></p>
<p><small><a target="_blank" href="https://docs.ultralytics.com/">YOLOv8 Documentation</a>. </small></p>

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
