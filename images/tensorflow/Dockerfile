FROM rhel7-cuda:latest

ENV APP_DIR=/opt/ml-on-ocp
ENV NVIDIA_VISIBLE_DEVICES=all
ENV NVIDIA_DRIVER_CAPABILITIES=compute,utility
ENV NVIDIA_REQUIRE_CUDA'="cuda>=8.0"

RUN yum -y install python-pip python-devel && yum clean all
RUN pip install --no-cache-dir --upgrade pip
RUN pip install --no-cache-dir tensorflow-gpu==1.3.0
RUN pip install --no-cache-dir jupyter
RUN pip install --no-cache-dir matplotlib
RUN pip install --no-cache-dir keras

#setup dir
RUN mkdir -p $APP_DIR
COPY *.ipynb $APP_DIR/
COPY data $APP_DIR/data
COPY figures $APP_DIR/figures

WORKDIR "$APP_DIR"

# Set up our notebook config.
COPY jupyter_notebook_config.py /root/.jupyter/
COPY run_jupyter.sh /

EXPOSE 8888 6006

CMD /run_jupyter.sh --allow-root