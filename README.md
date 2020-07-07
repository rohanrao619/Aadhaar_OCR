# Aadhaar OCR
Extraction, Verification and Masking of Aadhaar UIDs from photos and scanned documents.

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
