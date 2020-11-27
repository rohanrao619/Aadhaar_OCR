# Aadhaar OCR
Extraction, Verification and Masking of Aadhaar UIDs from photos and scanned documents.

## Solution

The solution to the problem involves use of PyTesseract Optical Character Recognition engine and OpenCV for image processing. It can be divided into 3 Sub-Tasks:
1. Extracting Aadhaar UID from photo using Tesseract.
2. Verifying the extracted Aadhaar UIDs.
3. Masking the first 8 digits of detected UIDs.

## Extracting Aadhaar UIDs

This task can be further divided into 2 Sub-Tasks:
1) Preprocess the image and then use PyTesseract library to extract all recognizable text from the image with their corresponding bounding boxes.
2) Use RegEx Search to find possible UID candidates. Aadhaar contains 12 numeric digits, so any 12-digit no. in the text returned by the OCR engine can be a possible UID.

The problem now is that image may need some pre-processing before it is possible to extract text from it. There are may factors affecting the performance of Tesseract engine, such as Orientation, Noise, Resolution, Illumination etc. For tackling these problems, we use the following pipeline:

a) Try without any processing.</br>
b) If (a) doesn’t work, try using OpenCV’s Gaussian Blur to remove random noise, then try again.</br>
c) If (b) doesn’t work, rotate the image by 90 degrees and try (a) and (b) again.

In this way steps (a), (b) and (c) are repeated 4 times (for 0, 90, 180 and 270 degrees rotation) and if at any point UID candidates are found, we stop (as all UIDs in the image can be found in that particular setting). In case these steps fail to produce desired results, we produce the super resolution version of the image using ESRGAN and retry with the pipeline described above.

## Verifying and Masking Aadhaar UIDs

In this step we try to filter the invalid UIDs using the Verhoeff Algorithm as there can be many unintended RegEx matches that are not of use. It is basically a checksum validation method. We use OpenCV’s functions to black out the first 8 digits of every UID with the help of character wise bounding boxes found in the previous step.

## Algorithms Used

In our solution pipeline we use some algorithms such as:
1. Verhoeff Algorithm: Aadhaar UID is a 12-digit number in which the last digit is a checksum digit calculated using this algorithm. It utilizes some tables (multiplication, inverse and permutation) for calculating the checksum bit. For validating, same tables are used.
2. ESRGANs: Enhanced Super-Resolution Generative Adversarial Networks are capable of generating realistic textures during single image super-resolution. It achieves better visual quality with more realistic and natural textures than the original picture.

## Tools Used
1) Google Colab : Used as the development environment.
2) NumPy : Used for handling high dimensional arrays.
3) OpenCV and PIL : Used for image processing.
4) PyTesseract : Used for OCR.
5) RegEx : Used for Regular Expression searches.
6) img2pdf and pdf2image : Used for handling .pdf files.
7) ISR : Used for generating Super Resolution images.

## Final Notes
**Thanks for going through this Repository! Have a nice day.**</br>
</br>**Got any Queries? Feel free to contact me.**</br>
</br>**Saini Rohan Rao**
<p align="left">
<a href="mailto:rohanrao619@gmail.com"><img src="https://github.com/rohanrao619/Icons/blob/master/SVGs/Gmail.svg" height ="45" title="Gmail" alt="mailto:rohanrao619@gmail.com"></a>
<a href="https://github.com/rohanrao619"><img src="https://github.com/rohanrao619/Icons/blob/master/SVGs/GitHub.svg" height ="45" title="GitHub" alt="https://github.com/rohanrao619"></a>
<a href="https://www.linkedin.com/in/rohanrao619"><img src="https://github.com/rohanrao619/Icons/blob/master/SVGs/LinkedIn.svg" height ="45" title="LinkedIn" alt="https://www.linkedin.com/in/rohanrao619"></a>
<a href="https://rohanrao619.github.io/"><img src="https://github.com/rohanrao619/Icons/blob/master/SVGs/Portfolio.svg" height ="45" title="Portfolio Website" alt="https://rohanrao619.github.io/"></a>
</p>
