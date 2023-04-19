Dat255 Project – Computer Vision 

Identifying shipping container IDs 

Endre Johannesen Rossavik and Alexander Nordstrand 

Introduction

Shipping containers are used globally to transport goods, by road, train or by sea. It is a massive logistic undertaking to make sure shipping containers and the goods within get to where they are supposed to go, within a reasonable time, for as little cost as possible. Global shipping is a competitive market where squeezing out every bit of added efficiency, and reduction of man hours, is very compelling.

Most shipping containers have a unique ID signature printed on all sides, the international standard for these signatures is the BIC-code but not all container owners follow these standards, but have a variety of their own ways to issue ID's for their containers. These codes could be identified by an AI model just from images of the containers. The containers have uneven surfaces, wear and tear (rust, dirt, dents) and varying ID locations and text directions which make the task more difficult. They can often contain other unimportant text as well, so the model needs to be able to locate the relevant text and read it accurately. 

Goals 

- Investigate models and methods for extracting identification codes automatically from image data. 

- Explore and compare solutions based on ready-made OCR technology vs a specially trained model for this specific purpose.  

- Gain solid experience of the difficulties, challenges and pitfalls of extracting characters reliably from complex, imperfect real-life image data. 

- Implement a prototype proof of concept solution that demonstrates the feasibility of the ID identification solution. 

Methods

Two different approaches that were investigated: 

- Object detection to find the area of the container ID -> read the text form the cropped area by Tesseract OCR
 - pros:
 - cons:
 
- Full object detection approach, find each individual char of the container IDs with object detecton, then combine the detections into a full container ID String 
 - pros:
 - cons:

Results



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
