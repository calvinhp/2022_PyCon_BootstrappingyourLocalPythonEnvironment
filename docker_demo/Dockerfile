FROM python:3.10-slim-bullseye AS build

ARG DEVEL="no"

RUN set -x \
    && python -m venv /app

ENV PATH="/app/bin:${PATH}"

RUN pip --no-cache-dir --disable-pip-version-check install --upgrade pip setuptools wheel

COPY requirements /tmp/requirements

RUN set -x \
    && if [ "$DEVEL" = "yes" ]; then pip --no-cache-dir --disable-pip-version-check install --upgrade pip-tools; fi

RUN set -x \
    && pip --no-cache-dir --disable-pip-version-check install --no-deps \
        -r /tmp/requirements/base.txt

FROM python:3.10-slim-bullseye

ENV PATH="/app/bin:${PATH}"

WORKDIR /app/src

COPY --from=build /app/ /app/
COPY main.py /app/src