AlphaFold 3 Installation Guide (No Docker)This guide provides step-by-step instructions for installing AlphaFold 3 and its dependencies using Conda and Pip, specifically avoiding Docker.1. Environment SetupStart by creating a dedicated Conda environment and activating it. Python 3.11 is specified in these steps.# Create a new conda environment named 'alphafold3' with Python 3.11
conda create -n alphafold3 python=3.11

# Activate the environment
conda activate alphafold3
2. Install DependenciesNext, install the necessary packages using both Conda and Pip.a) Core Dependencies (Conda)Install hmmer from the bioconda channel:conda install bioconda::hmmer
b) Python Packages (Pip)Install the required Python libraries. It's often best to install these in batches as shown:# Install foundational libraries with specific versions
pip install jmp==0.0.4 ml-dtypes==0.5.0 opt-einsum==3.4.0

# Install NVIDIA CUDA libraries (ensure these versions are compatible with your GPU driver)
pip install nvidia-cublas-cu12==12.6.3.3 nvidia-cuda-cupti-cu12==12.6.80 nvidia-cuda-nvcc-cu12==12.6.77 nvidia-cuda-runtime-cu12==12.6.77
pip install nvidia-cufft-cu12==11.3.0.4 nvidia-cusolver-cu12==11.7.1.2 nvidia-cusparse-cu12==12.5.4.2 nvidia-nccl-cu12==2.23.4 nvidia-nvjitlink-cu12==12.6.77

# Install scientific computing, cheminformatics (RDKit), and utility libraries
pip install rdkit==2024.3.5 scipy==1.14.1 tabulate==0.9.0 toolz==1.0.0
pip install typeguard==2.13.3 typing-extensions==4.12.2 zstandard==0.23.0

# Install DeepMind Haiku (neural network library)
pip install dm_haiku==0.0.13

# Install NumPy (specific version)
pip install numpy==2.1.3

# Install JAX (machine learning framework) and related type hinting/plugin
pip install jax==0.4.34
pip install jaxtyping==0.2.34
pip install jax_cuda12_plugin==0.4.34 # Make sure this matches your JAX version and CUDA setup

# Install Triton (GPU programming) and its JAX integration
pip install triton==3.1.0
pip install jax_triton==0.2.0

# Install Pillow (image processing) and tqdm (progress bars)
pip install pillow==11.0.0
pip install tqdm==4.67.0

# Install NVIDIA cuDNN library
pip install nvidia_cudnn_cu12==9.5.1.17
3. TroubleshootingHere are solutions for some common issues you might encounter:a) Zlib ErrorIf you see errors related to zlib during installation or runtime:# Install zlib via conda-forge
conda install conda-forge::zlib

# Set environment variables to point to the installed zlib library and headers
# $CONDA_PREFIX is an environment variable automatically set by conda to the path of the active environment
export ZLIB_ROOT=$CONDA_PREFIX
export ZLIB_LIBRARY=$CONDA_PREFIX/lib/libz.so
export ZLIB_INCLUDE_DIR=$CONDA_PREFIX/include
b) G++ Version ErrorIf the installation complains about the g++ compiler version:# Install a C++ compiler from conda-forge
conda install -c conda-forge cxx-compiler
c) FileNotFoundError: ... chemical_component_sets.pickleIf you get an error stating chemical_component_sets.pickle cannot be found:This typically means the data build script needs to be run. This script processes downloaded data files into formats AlphaFold 3 uses. Execute it using:# Run the data building script located in the bin directory of your conda environment
$CONDA_PREFIX/bin/build_data
(Ensure you have downloaded the necessary AlphaFold 3 data files before running this script).
