# CT Scan Image Manipulation Detection using VGG16 and Feature Extraction


This repository contains code for detecting manipulated CT scan images by finding their closest match to the original images in a database. This approach helps identify if an image has been altered through adversarial or cyber-attacks, thus maintaining the integrity and trustworthiness of CT scan data. The model uses deep learning for feature extraction and a combination of texture and histogram analysis, along with VGG16 pre-trained on ImageNet, to compare and find the most similar original image corresponding to a manipulated CT scan.

# Project Overview


In this project, we tackle the problem of detecting manipulated CT images by comparing them with a dataset of original images. The workflow involves two key steps: generating a manipulated image using image processing techniques (such as Gaussian blur, contrast adjustments, or edge enhancement) and finding the closest match in a set of original images. The matching algorithm ensures that, even if a CT scan image is altered by an adversarial attack, the system can trace back to the original, unaltered version.


This application of VGG16 in combination with texture and histogram features enhances the robustness of the model. The texture features extracted from a Gray Level Co-occurrence Matrix (GLCM) help capture fine details in CT images, which are sensitive to any minor manipulations. The histogram analysis provides a pixel intensity distribution, adding another layer of validation. By calculating the cosine distance between extracted features of the manipulated image and each original image, the model can determine which original image is the closest match.

# Implementation Details


Step 1: Loading and Manipulating the CT Image


The code first loads a CT image from Google Drive and applies a series of image manipulations to simulate potential attacks or adversarial changes. The manipulated image undergoes techniques like Gaussian blur, contrast adjustment, and edge enhancement within a defined region of interest (ROI). This process allows for a controlled transformation of the image to mimic real-world manipulation.

Step 2: Feature Extraction


To detect manipulations, the model employs a VGG16 network pre-trained on ImageNet. However, instead of using VGG16 for classification, we use it as a feature extractor. The VGG16 network outputs high-level feature vectors that capture the essential characteristics of the CT image. Additional features include histogram and texture information, where:


Histogram Features: Capture the intensity distribution of pixel values across the image.
Texture Features: Extracted using GLCM to analyze image texture properties like contrast, dissimilarity, homogeneity, energy, and correlation.


Step 3: Finding the Most Similar Original Image
The main goal is to detect if the manipulated image resembles any image in the original dataset. Using cosine distance, the algorithm compares the feature vector of the manipulated image with feature vectors of the original images in the database. The original image with the smallest cosine distance is considered the closest match, thus allowing us to identify which original image was likely manipulated.

# Key Functions


load_ct_image(image_path): Loads CT images, supporting .tif, .tiff, and other standard image formats, and resizes them to 224x224 pixels for VGG16 compatibility.
extract_combined_features(image, model): Extracts combined features from the CT image, including VGG16 features, histogram features, and GLCM-based texture features.
find_most_similar_original(manipulated_image, original_paths): Finds the closest original image by comparing the manipulated image features with those of each original image using cosine distance.


# Applications


This project has significant applications in fields where image authenticity and integrity are crucial, such as in healthcare, where diagnostic CT images must remain unaltered for accurate diagnoses. The approach can be extended to other imaging modalities and used as a countermeasure against adversarial attacks targeting sensitive medical imaging data.
