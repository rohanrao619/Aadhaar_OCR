# Aadhaar OCR
Extraction, Verification and Masking of Aadhaar UIDs from photos and scanned documents.

## Solution

The solution to the problem involves use of PyTesseract OCR engine and OpenCV for image processing. It can be divided into 3 Sub-Tasks:
1. Extracting Aadhaar UID from photo using Tesseract.
2. Verifying the extracted Aadhaar UIDs.
3. Masking the first 8 digits of detected UIDs.

## Extracting Aadhaar UID

This task can be further divided into 2 Sub-Tasks:
1) Preprocess the image and then use PyTesseract library to extract all recognizable text from the image with their corresponding bounding boxes.
2) Use RegEx Search to find possible UID candidates. Aadhaar contains 12 numeric digits, so any 12-digit no. in the text returned by the OCR engine can be a possible UID.

The problem now is that image may need some pre-processing before it is possible to extract text from it. There are may factors affecting the performance of Tesseract engine, such as Orientation, Noise, Resolution, Illumination etc. For tackling these problems, we use the following pipeline:

a) Try without any processing.</br>
b) If (a) doesn’t work, try using OpenCV’s Gaussian Blur to remove random noise, then try again.</br>
c) If (b) doesn’t work, rotate the image by 90 degrees and try (a) and (b) again.


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
