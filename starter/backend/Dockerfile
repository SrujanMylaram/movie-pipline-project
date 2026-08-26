FROM public.ecr.aws/docker/library/python:3.10-alpine

RUN adduser -u 1000 -D app

RUN apk update && \
    apk add \
    pcre \
    pcre-dev \
    build-base \
    gcc \
    linux-headers \
    openssl \
    libffi-dev \
    && pip install pipenv

RUN mkdir -p /var/www/app && \
    mkdir /app

COPY Pipfile* /app

RUN cd /app && \
    CFLAGS="-Wno-error=incompatible-pointer-types" \
    pipenv install --system --deploy

COPY . /app

WORKDIR /app

EXPOSE 5000

CMD ["pipenv", "run", "serve"]