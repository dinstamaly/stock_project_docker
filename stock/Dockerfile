# pull official python alpine image
FROM python:3.7-alpine

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV C_FORCE_ROOT true


# install dependencies
# Update pip
RUN pip install --upgrade pip
RUN pip install --upgrade pip setuptools wheel

RUN apk update && apk add --no-cache \
    postgresql \
    zlib \
    jpeg \
    openblas \ 
    libstdc++

RUN apk add --no-cache --virtual build-deps \
    gcc \  
    python3-dev \ 
    musl-dev \
    postgresql-dev\
    zlib-dev \
    jpeg-dev \
    g++ \
    openblas-dev \
    cmake \
    && ln -s /usr/include/locale.h /usr/include/xlocale.h

# Installing numpy, scipy, psycopg2, gensim
RUN pip install --no-cache-dir \
    pandas \
    numpy \
    psycopg2 

COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy entrypoint.sh
COPY ./entrypoint.sh .

# copy project
COPY . .

# ENTRYPOINT ["/usr/src/app/entrypoint.sh"]