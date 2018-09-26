FROM ichizero/cuda-opencv:latest

LABEL maintainer="ichizero"

RUN pip3 install  --no-cache-dir \
  chainer \
  chainercv \
  chainerui \
  hdf5storage \
  h5py \
  scipy \
  py3nvml \
  cython \
  argparse \
  tqdm \
  matplotlib

# RUN chainerui db create && \
#   chainerui db upgrade
