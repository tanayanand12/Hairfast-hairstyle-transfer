# Hairfast-hairstyle-transfer

## Introduction
This project addresses the complex task of transferring a hairstyle from a reference image to an input photo for virtual hair try-on. This task is challenging due to the need to adapt to various photo poses, the sensitivity of hairstyles, and the lack of objective metrics. We present the MyProject model, which uniquely solves these problems and achieves high resolution, near real-time performance, and superior reconstruction compared to optimization problem-based methods. Our solution includes a new architecture, an enhanced inpainting approach, and improved encoders for better alignment, color transfer, and a new encoder for post-processing.

## Installation
Clone this repo:
```
git clone https://github.com/AIRI-Institute/MyProject
cd MyProject
```
Download all pretrained models:
```
git clone https://huggingface.co/AIRI-Institute/MyProject
cd MyProject && git lfs pull && cd ..
mv MyProject/pretrained_models pretrained_models
mv MyProject/input input
rm -rf MyProject
```
Setting the environment
Option 1 [recommended], install Poetry and then:
```
poetry install
```
Option 2, just install the dependencies in your environment:
```
pip install -r requirements.txt
```
## Usage
You can use main.py to run the method, either for a single run or for a batch of experiments.

An example of running a single experiment:
```
python main.py --face_path=6.png --shape_path=7.png --color_path=8.png \
    --input_dir=input --result_path=output/result.png
```
To run the batch version, first create an image triples file (face/shape/color):
```
cat > example.txt << EOF
6.png 7.png 8.png
8.png 4.jpg 5.jpg
EOF
```
And now you can run the method:
```
python main.py --file_path=example.txt --input_dir=input --output_dir=output
```
You can use MyProject in the code directly:
```python
from hair_swap import MyProject, get_parser

# Init MyProject
my_project = MyProject(get_parser().parse_args([]))

# Inference
result = my_project(face_img, shape_img, color_img)
```
See the code for input parameters and output formats.

### Alternatively
In addition to the methods mentioned above, you can also directly run this project using a Google Colab file. Here are the steps:

Open the Google Colab file by clicking on the link provided.
Follow the instructions in the Colab file to run the project.
Please note that you need to have a Google account and be signed in to access Google Colab.

Google Colab File: [Hairfast-hairstyle-transfer](https://colab.research.google.com/drive/1ibJN9apSYQLeaTFijDFe4UmKShEOGeJd?usp=sharing)

## Results
The effectiveness of our approach is demonstrated on realism metrics after random hairstyle transfer and reconstruction when the original hairstyle is transferred. In the most difficult scenario of transferring both shape and color of a hairstyle from different images, our method performs in less than a second on the Nvidia V100.

## References
@article{nikolaev2024hairfastgan,
  title={HairFastGAN: Realistic and Robust Hair Transfer with a Fast Encoder-Based Approach},
  author={Nikolaev, Maxim and Kuznetsov, Mikhail and Vetrov, Dmitry and Alanov, Aibek},
  journal={arXiv preprint arXiv:2404.01094},
  year={2024}
}


## Extra Information about the Methodology
Model Development: The authors developed a model called MyProject to address the task of transferring a hairstyle from a reference image to an input photo for virtual hair try-on. This model is designed to overcome the limitations of current state-of-the-art methods, which are either slow due to the use of an optimization process or of low quality due to the use of encoder-based models that operate in StyleGAN’s W+ space or use other low-dimensional image generators.
New Architecture: MyProject includes a new architecture that operates in the FS latent space of StyleGAN. This is a departure from previous methods that operate in StyleGAN’s W+ space.
Enhanced Inpainting Approach: The authors used an enhanced inpainting approach to improve the quality of the hairstyle transfer.
Improved Encoders: The authors improved the encoders used in the model for better alignment and color transfer. They also introduced a new encoder for post-processing.
Performance Evaluation: The effectiveness of the MyProject model was demonstrated on realism metrics after random hairstyle transfer and reconstruction when the original hairstyle is transferred. In the most difficult scenario of transferring both shape and color of a hairstyle from different images, the method performs in less than a second on the Nvidia V100.
This methodology allows the MyProject model to achieve high resolution, near real-time performance, and superior reconstruction compared to optimization problem-based methods. It also addresses the problem of hairstyle transfer when the source pose is very different from the target pose, which is a limitation of both optimization-based and encoder-based models.


