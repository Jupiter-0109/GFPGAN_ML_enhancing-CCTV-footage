# GFPGAN_ML_enhancing-CCTV-footage

Dependencies and Installation
Python >= 3.7 (Recommend to use Anaconda or Miniconda)
PyTorch >= 1.7
Option: NVIDIA GPU + CUDA
Option: Linux
Installation
We now provide a clean version of GFPGAN, which does not require customized CUDA extensions.
If you want to use the original model in our paper, please see PaperModel.md for installation.

Clone repo

git clone https://github.com/TencentARC/GFPGAN.git
cd GFPGAN
Install dependent packages

# Install basicsr - https://github.com/xinntao/BasicSR
# We use BasicSR for both training and inference
pip install basicsr

# Install facexlib - https://github.com/xinntao/facexlib
# We use face detection and face restoration helper in the facexlib package
pip install facexlib

pip install -r requirements.txt
python setup.py develop

# If you want to enhance the background (non-face) regions with Real-ESRGAN,
# you also need to install the realesrgan package
pip install realesrgan
⚡ Quick Inference
We take the v1.3 version for an example. More models can be found here.

Download pre-trained models: GFPGANv1.3.pth

wget https://github.com/TencentARC/GFPGAN/releases/download/v1.3.0/GFPGANv1.3.pth -P experiments/pretrained_models
Inference!

python inference_gfpgan.py -i inputs/whole_imgs -o results -v 1.3 -s 2
Usage: python inference_gfpgan.py -i inputs/whole_imgs -o results -v 1.3 -s 2 [options]...

  -h                   show this help
  -i input             Input image or folder. Default: inputs/whole_imgs
  -o output            Output folder. Default: results
  -v version           GFPGAN model version. Option: 1 | 1.2 | 1.3. Default: 1.3
  -s upscale           The final upsampling scale of the image. Default: 2
  -bg_upsampler        background upsampler. Default: realesrgan
  -bg_tile             Tile size for background sampler, 0 for no tile during testing. Default: 400
  -suffix              Suffix of the restored faces
  -only_center_face    Only restore the center face
  -aligned             Input are aligned faces
  -ext                 Image extension. Options: auto | jpg | png, auto means using the same extension as inputs. Default: auto
If you want to use the original model in our paper, please see PaperModel.md for installation and inference.

🏰 Model Zoo
Version	Model Name	Description
V1.3	GFPGANv1.3.pth	Based on V1.2; more natural restoration results; better results on very low-quality / high-quality inputs.
V1.2	GFPGANCleanv1-NoCE-C2.pth	No colorization; no CUDA extensions are required. Trained with more data with pre-processing.
V1	GFPGANv1.pth	The paper model, with colorization.
The comparisons are in Comparisons.md.

Note that V1.3 is not always better than V1.2. You may need to select different models based on your purpose and inputs.

Version	Strengths	Weaknesses
V1.3	✓ natural outputs
✓better results on very low-quality inputs
✓ work on relatively high-quality inputs
✓ can have repeated (twice) restorations	✗ not very sharp
✗ have a slight change on identity
V1.2	✓ sharper output
✓ with beauty makeup	✗ some outputs are unnatural
