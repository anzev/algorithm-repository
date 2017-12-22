FROM hbpmip/python-mip:0.2.4

MAINTAINER anze.vavpetic@ijs.si

ENV DOCKER_IMAGE=hbpmip/python-hedwig:0.1.0 \
    FUNCTION=python-hedwig

# Install system packages
RUN apt-get update
RUN apt-get install -y git gcc python3-dev

# Update pip
RUN python -m pip install --upgrade pip

# Install mip packages
COPY requirements_mip.txt /requirements_mip.txt
RUN pip install -r requirements_mip.txt

# Install hedwig and its requirements
RUN git clone -b python3 https://github.com/anzev/hedwig.git /src/hedwig

WORKDIR /src/hedwig
RUN pip install -r requirements.txt
RUN python setup.py install

COPY preprocess.py /src/hedwig/
COPY mip_hedwig.py /src/hedwig/

ENTRYPOINT ["python", "/src/hedwig/mip_hedwig.py"]

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="hbpmip/python-hedwig" \
      org.label-schema.description="Hedwig method for semantic subgroup discovery" \
      org.label-schema.url="https://github.com/LREN-CHUV/algorithm-repository" \
      org.label-schema.vcs-type="git" \
      org.label-schema.vcs-url="https://github.com/LREN-CHUV/algorithm-repository.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.version="$VERSION" \
      org.label-schema.vendor="LREN CHUV" \
      org.label-schema.license="AGPLv3" \
      org.label-schema.docker.dockerfile="Dockerfile" \
      org.label-schema.schema-version="1.0"
