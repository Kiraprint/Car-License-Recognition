# Car-License-Recognition

## Description

License plate recognition systems consist of two modules: detection and Optical Character Recognition (OCR). The detector extracts a rectangle with a license plate number from the image, and OCR converts it into text. We will assume that the detector is already implemented. The project proposes to independently train an OCR model for license plates.

**Input example:**
![Car License](https://algocode.ru/files/course_dlfall22/number.png)

**Output examlpe:** 皖AD16688

## Proposed solution architecture

It is proposed to realize a model consisting of two blocks, Fully-convolutional CNN (FCNN) and Bi-LSTM. Cross-entropy or CTC-loss is proposed to be used on the output.

Example architecture:

![Architecture](https://algocode.ru/files/course_dlfall22/architecture.png)

## Database

It is suggested to use the corpus [CCPD2019](https://github.com/detectRecog/CCPD). The test includes images from CCPD-weather. The prepared corpus can be downloaded from [link](https://disk.yandex.ru/d/adjYzzNayB1pag).

## Project steps

1. **Data preparation.** I need implemented a data class (inheritor of torch.utils.data.Dataset). The class reads input images and extract labels from file names. To read images it uses OpenCV library (methods cv2.imread, cv2.resize and cv2.cvtColor).
2. **Model creation and training.** The model code is implemented through layers of the torch standard library (torchvision.models and analogs cannot be used). Since the number of characters in the numbers is fixed, the usual cross-entropy criterion is be used.
3. **Calculation of metrics.** The quality of the model should be evaluated by two metrics: accuracy and Character Error Rate (CER). Accuracy counts the proportion of correctly recognized license plates. CER estimates the number of character errors.
4. **Analysis of model errors.** In this section I found images from the test corpus, where the model is wrong most of all (by loss or by CER).

## Results

The model was trained on a train corpus. The model was trained for 10 epochs. The accuracy on the test corpus is 0.95, the CER is 0.01. The model is able to recognize license plates in different weather conditions, with different angles of inclination and different distances to the camera.
