FROM hbpmip/r-job:239492a

MAINTAINER anze.vavpetic@ijs.si

LABEL eu.humanbrainproject.function=hedwig \
      eu.humanbrainproject.function.location=node \
      eu.humanbrainproject.function.version=0.3.0 \
      eu.humanbrainproject.function.author="Anze Vavpetic" \
      eu.humanbrainproject.function.organisation="JSI" \
      eu.humanbrainproject.function.date="2016-02-05"

# Temporary fix for the proxy issue
RUN echo "Acquire::http::Proxy \"false\";" > /etc/apt/apt.conf.d/01proxy
# End temporary fix

RUN apt-get update && apt-get install -y \
	python-dev \
	python-pip \
	python-scipy \
	git \
    && rm -rf /var/lib/apt/lists/*

RUN git clone -b hbp https://github.com/anzev/hedwig.git /src/hedwig
COPY main.R /src/
WORKDIR /src/hedwig
RUN pip install -r requirements.txt
RUN python setup.py install

