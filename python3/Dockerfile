FROM python:3.12

COPY requirements.txt ./

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple \
    && pip install --upgrade pip \
    && pip install -r requirements.txt \
    && pip uninstall numpy -y
