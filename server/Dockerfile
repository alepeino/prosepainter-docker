FROM python:3.7

WORKDIR /app

# ProsePainter deps
# RUN pip install --upgrade "jax[cuda]" -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html
# RUN pip install "jax[cpu]"
RUN pip install "jax[cuda]"
RUN pip install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

# Anaconda deps
RUN apt-get update && apt-get install -y libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6

# Install Anaconda
RUN curl https://repo.anaconda.com/archive/Anaconda3-2023.07-1-Linux-x86_64.sh -o anaconda.sh
RUN bash anaconda.sh -b
#RUN rm anaconda.sh
RUN . /root/anaconda3/bin/activate && conda init

# Clone ProsePainter repo
RUN git clone https://github.com/Morphogens/ProsePainter.git

WORKDIR ProsePainter
RUN bash -lc "conda env create -f server/env-server.yml"
RUN bash -lc "conda activate prosepaint"

ENV PYTHONPATH=.:/root/anaconda3/envs/prosepaint/lib/python3.7/site-packages

EXPOSE 8004

CMD ["python", "server/server_deploy.py"]

# https://github.com/Morphogens/ProsePainter/issues/14
# https://github.com/google/jax#installation