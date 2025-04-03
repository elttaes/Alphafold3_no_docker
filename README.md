# Alphafold3_no_docker
conda create -n alphafold3 python=3.11

conda activate alphafold3

conda install bioconda::hmmer
pip install jmp==0.0.4 ml-dtypes==0.5.0 opt-einsum==3.4.0
pip install nvidia-cublas-cu12==12.6.3.3 nvidia-cuda-cupti-cu12==12.6.80 nvidia-cuda-nvcc-cu12==12.6.77 nvidia-cuda-runtime-cu12==12.6.77

pip install nvidia-cufft-cu12==11.3.0.4 nvidia-cusolver-cu12==11.7.1.2 nvidia-cusparse-cu12==12.5.4.2 nvidia-nccl-cu12==2.23.4 nvidia-nvjitlink-cu12==12.6.77
pip install rdkit==2024.3.5 scipy==1.14.1 tabulate==0.9.0 toolz==1.0.0  
pip install typeguard==2.13.3 typing-extensions==4.12.2 zstandard==0.23.0

pip install dm_haiku==0.0.13
pip install numpy==2.1.3

pip install jax==0.4.34
pip install jaxtyping==0.2.34
pip install jax_cuda12_plugin==0.4.34

pip install triton==3.1.0
pip install jax_triton==0.2.0
pip install pillow==11.0.0
pip install nvidia_cudnn_cu12==9.5.1.17
pip install tqdm==4.67.0

if zlib error:
conda install conda-forge::zlib
export ZLIB_ROOT=$CONDA_PREFIX
export ZLIB_LIBRARY=$CONDA_PREFIX/lib/libz.so
export ZLIB_INCLUDE_DIR=$CONDA_PREFIX/include

if g++ version error:
conda install -c conda-forge cxx-compiler

if:
FileNotFoundError: [Errno 2] No such file or directory: “/xxx/chemical_component_sets.pickle”
run $CONDA_PREFIX/bin/build_data
