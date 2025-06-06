# Rotational-Equivariant-VAE

An experiment in fine-tuning a Variational Autoencoder (VAE) to understand 180-degree rotations, making the latent space equivariant to the pixel space.

PI: Xinqi Liu

---

## About The Project

This project showcases a fine-tuned Variational Autoencoder (VAE) that has been specifically trained to understand a 180-degree rotation. Unlike a standard VAE where rotating the latent space produces a scrambled, unrecognizable image, this model learns to associate a 180-degree rotation of a latent vector with a 180-degree rotation of the corresponding output image, without forgetting 0 degree rotation reconstruction.

The core of this experiment is a custom training objective that teaches the model this specific geometric property.

### Key Features & Methodology
* **Base Model:** The VAE was extracted from the popular **`Disty0/SoteMix`** model, which is based on Stable Diffusion v1.5.
* **Custom Loss Function:** The model was fine-tuned using a dual-objective loss function composed of:
    1.  **Reconstruction Loss:** A standard Mean Squared Error (MSE) loss to ensure the VAE can accurately reconstruct images.
    2.  **Rotation Loss:** A MSE loss that explicitly penalizes the model if decoding a 180°-rotated latent vector does not produce a 180°-rotated version of the original image.
* **Training Environment:** All data collection, model training, and testing were performed using Google Colab.

## Results & Verification

The model successfully learned the desired rotational property. This was quantitatively verified by performing a round-trip transformation:
1.  An image is encoded into a latent vector.
2.  The latent vector is flipped/rotated 180°.
3.  The modified latent is decoded, producing a rotated image.
4.  The final image is rotated back 180°.

The Mean Squared Error (MSE) between the final image and the original input was exceptionally low (**~0.0023**), proving that the transformation is nearly perfectly flipped and that the model has learned the intended rotational equivariance.

## View the Notebook

Due to how GitHub renders (or fails to render) notebooks with interactive widget outputs, it's recommended to view the project notebook using nbviewer.

**[Click here to view `vaeTrain.ipynb` on nbviewer](https://nbviewer.org/github/alfredchleong/Rotational-Equivariant-VAE/main/vaeTrain.ipynb)**
