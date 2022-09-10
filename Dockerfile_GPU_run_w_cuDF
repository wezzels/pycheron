FROM python:3.6.9 as builder

WORKDIR /usr/src/app

COPY pycheron ./
RUN curl -sSL https://install.python-poetry.org -o install.py
RUN chmod +X install.py &&  POETRY_VERSION=1.1.15 python3 ./install.py
RUN mv /root/.local/bin/poetry /usr/local/bin/ && poetry --version
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get -y install git-lfs
RUN git lfs install && git lfs fetch && git lfs pull
RUN /usr/src/app/build.sh
FROM python:3.6.9
COPY --from=builder /usr/src/app/dist/pycheron-3.0.0-py3-none-any.whl /opt/
RUN pip3 install /opt/pycheron-3.0.0-py3-none-any.whl && rm -rf /opt/pycheron-3.0.0-py3-none-any.whl
RUN ls -al /opt/
RUN pip3 install /opt/pycheron-3.0.0-py3-none-any.whl

#CMD [ "python", "./your-daemon-or-script.py" ]
