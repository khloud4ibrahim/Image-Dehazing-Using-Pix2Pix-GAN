# Image-Dehazing-Using-Pix2Pix-GAN

## Overview

Image dehazing is the process of removing haze from an image to recover a clearer and more visually informative version of the scene. Haze can reduce visibility, contrast, and overall image quality.

This project uses a **Pix2Pix Generative Adversarial Network (GAN)** for **image-to-image translation from hazy images to clear images**.

Pix2Pix is suitable for this task because it is designed for **paired image-to-image translation**, where each hazy image has a corresponding clear ground-truth image.

The project covers the complete workflow, including dataset verification, preprocessing, Pix2Pix architecture, model training, evaluation, generated results, and a simple Gradio interface for testing the trained model.

---

## Dataset

The project uses the **RESIDE-6K** dataset for image dehazing.

### Dataset Details

* **Training set:** 6,000 hazy images + 6,000 corresponding clear images
* **Test set:** 1,000 hazy images + 1,000 corresponding clear images
* **Image resolution:** 400 × 400 pixels
* **Image format:** RGB
* Hazy and ground-truth filenames are matched between each pair.

The paired structure makes the dataset suitable for training a Pix2Pix model.

---

## Preprocessing

The images were preprocessed before being passed to the model.

The preprocessing pipeline includes:

* Resizing images to **256 × 256 pixels**
* Converting images to tensors
* Normalizing image values to the range **[-1, 1]**
* Creating paired hazy/clear samples
* Splitting the data into training and testing sets

The training pipeline uses a batch size of **16**.

---

## Pix2Pix Architecture

Pix2Pix consists of two main networks:

### Generator

The Generator receives a hazy image as input and generates a dehazed version of the image.

The Generator is based on a **U-Net architecture**, allowing it to preserve useful spatial information through skip connections.

### Discriminator

The Discriminator evaluates the generated image together with the input hazy image and tries to distinguish between:

* Real hazy/clear image pairs
* Hazy/generated-clear image pairs

The Generator learns to produce increasingly realistic dehazed images while the Discriminator learns to distinguish generated results from ground-truth images.

---

## Training

The Pix2Pix model was trained for **170 epochs**.

The training process includes:

1. Loading paired hazy and clear images
2. Generating dehazed images using the Generator
3. Training the Discriminator
4. Training the Generator using adversarial and reconstruction losses
5. Monitoring training progress
6. Evaluating generated images using PSNR and SSIM
7. Saving model checkpoints during training

The final trained Generator was used for evaluation and testing.

---

## Evaluation

The model was evaluated using two image-quality metrics:

### PSNR

**Peak Signal-to-Noise Ratio (PSNR)** measures the similarity between the generated image and the ground-truth image. Higher PSNR generally indicates better reconstruction quality.

### SSIM

**Structural Similarity Index Measure (SSIM)** evaluates structural similarity between the generated and ground-truth images. Higher SSIM indicates better preservation of image structure and visual details.

### Final Results

| Metric |       Result |
| ------ | -----------: |
| PSNR   | **25.99 dB** |
| SSIM   |      **92%** |

---

## Generated Results

The trained Generator was tested on hazy images to evaluate its ability to recover clearer versions of the scenes.

The generated results are compared with the original hazy inputs and the corresponding ground-truth clear images to visually assess the dehazing performance.

---

## Gradio UI

A simple **Gradio** interface was created to make the trained model easier to test.

The interface allows the user to:

1. Upload a hazy image
2. Pass it through the trained Generator
3. View the generated dehazed image

This provides a simple way to interact with the trained model without manually running the inference pipeline.

---

## Project Structure

```text
Image-Dehazing-Pix2Pix/
│
├── Image_Dehazing_Pix2Pix.ipynb
├── README.md
├── requirements.txt
└── results/
```

---

## Technologies & Libraries

* Python
* PyTorch
* NumPy
* Pandas
* Matplotlib
* scikit-image
* Gradio
* Google Colab / Jupyter Notebook

---

## Key Takeaways

This project helped me apply the concepts I learned about **GANs and image-to-image translation** to a practical computer vision problem.

It also provided hands-on experience with:

* Working with paired image datasets
* Building Generator and Discriminator networks
* Training GAN-based models
* Evaluating image restoration results
* Saving and loading trained models
* Building a simple interface for model inference

---

## Author

**Khloud Ibrahim**


```


**ملاحظة صغيرة:** أنا متعمد ما أضيفش حاجات زي `Autoencoders` في الـREADME بتاع المشروع، لأن ده مشروع **Pix2Pix** تحديدًا، فالأفضل الـREADME يركز على اللي اتعمل فعلًا فيه. وكمان لو عندك صور للـresults أو Screenshot للـGradio UI، إضافتهم للـREADME هتخليه أقوى بصريًا جدًا.
```
