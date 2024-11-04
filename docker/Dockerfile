# docker/Dockerfile
FROM python:3.10-slim

RUN pip install --upgrade pip && \
    pip install jupyterlab

ENV JUPYTER_PORT=8888

EXPOSE $JUPYTER_PORT

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--no-browser", "--allow-root"]
