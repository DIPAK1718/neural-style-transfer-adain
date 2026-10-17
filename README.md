# Neural Style Transfer with Adaptive Instance Normalization (AdaIN)

An AI-powered image stylization application that combines the content of one image with the artistic style of another using deep learning.

The project implements **Adaptive Instance Normalization (AdaIN)** with a pretrained VGG-19 encoder and a trained decoder. A Flask web application provides an interface for uploading images and generating stylized results.

## Overview

Neural Style Transfer (NST) is a computer vision technique that combines the semantic content of one image with the visual appearance of another.

This project uses AdaIN to align the feature statistics of a content image with those of a style image, enabling arbitrary style transfer without training a separate model for every artistic style.

## Key Features

* Upload a content image and an artistic style image.
* Generate stylized images using a pretrained VGG-19 encoder and trained decoder.
* Control the strength of the style transfer using an alpha parameter.
* Preview generated results through a Flask web interface.
* Run inference using PyTorch on a supported CPU or CUDA device.

## How It Works

The inference pipeline follows these steps:

1. **Input:** Receive a content image and a style image.
2. **Feature extraction:** Pass both images through the pretrained VGG-19 encoder.
3. **Adaptive Instance Normalization:** Adjust the content features using the channel-wise mean and standard deviation of the style features.
4. **Style-strength adjustment:** Interpolate between the original content features and the AdaIN-transformed features using alpha.
5. **Image reconstruction:** Pass the resulting features through the trained decoder.
6. **Output:** Return the generated stylized image.

### Architecture

Content Image ──┐
　　　　　　　　├── VGG-19 Encoder ── AdaIN ── Alpha Blending ── Decoder ── Stylized Image
Style Image ────┘

The VGG-19 encoder extracts image features, while the decoder reconstructs an image from the transformed features.

## Technologies Used

* Python
* PyTorch
* Torchvision
* Flask
* Pillow (PIL)
* NumPy
* HTML and CSS
* Adaptive Instance Normalization (AdaIN)
* Convolutional Neural Networks (CNNs)

## Project Structure

```text
ai-nst-project/
├── Demo_IO_Images/
│   ├── i-p/
│   └── o-p/
├── NST_Code/
│   ├── app.py
│   ├── train.py
│   ├── vgg_normalised.pth
│   ├── content_data/
│   ├── style_data/
│   ├── examples/
│   ├── experiment/
│   │   └── final_exp/
│   │       └── decoder_final.pth
│   ├── templates/
│   │   └── index.html
│   └── utils/
│       ├── models.py
│       └── utils.py
├── code.ipynb
├── requirements.txt
├── .gitignore
└── README.md
```

## Installation

### Prerequisites

* Python 3.10 or a compatible Python version
* pip
* Git

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd ai-nst-project
```

Replace the placeholder with the URL of your published repository.

### 2. Create a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```powershell
pip install -r requirements.txt
```

### 4. Verify the model files

Ensure that the following files are present at their expected locations:

* `NST_Code/vgg_normalised.pth`
* `NST_Code/experiment/final_exp/decoder_final.pth`

These files are required by the current inference implementation. Follow the repository's model-download instructions if the weights are distributed separately.

### 5. Start the application

```powershell
cd NST_Code
python app.py
```

Open `http://localhost:5000` in your browser.

## Style Strength

The alpha parameter controls the interpolation between the original content features and the AdaIN-transformed features.

* **Alpha = 0.0:** Uses the original content features before decoding.
* **Alpha = 0.5:** Blends content features and style-transformed features equally.
* **Alpha = 1.0:** Uses the fully AdaIN-transformed features.

The final visual appearance also depends on the decoder and the input images.

## Training

The project includes `NST_Code/train.py` and the supporting model utilities.

During training, the encoder extracts content and style features, AdaIN transforms the content features, and the decoder reconstructs the output image. The training losses guide the decoder toward preserving content while reproducing the style characteristics.

The encoder is pretrained; the decoder is the trainable component in the standard AdaIN training pipeline.

## Limitations

* Output quality depends on the input images and trained decoder.
* Fine details and image geometry may change during stylization.
* Inference speed depends on the hardware and image dimensions.
* The current implementation uses pretrained model weights rather than training a new model from scratch.
* The project implements an established AdaIN approach; it does not claim a novel style-transfer algorithm.

## References

1. Huang, X., and Belongie, S. *Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization.* ICCV, 2017. https://arxiv.org/abs/1703.06868
2. Simonyan, K., and Zisserman, A. *Very Deep Convolutional Networks for Large-Scale Image Recognition.* https://arxiv.org/abs/1409.1556

## Credits and Licensing

This project builds on established neural style transfer research and pretrained model weights.

Before redistributing model weights, datasets, or example images, verify the applicable licenses and attribution requirements. Preserve the original authors' credits and include the relevant license information.

## Author

**Dipak Chaudhari**

B.Tech CSE (Data Science) | AI/ML Engineering

GitHub: [DIPAK1718](https://github.com/DIPAK1718)
