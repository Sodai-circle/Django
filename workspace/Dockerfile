ARG APP_CODE_PATH_CONTAINER
ARG PYTHON_VERSION

FROM python:${PYTHON_VERSION}
ENV PYTHONUNBUFFERED 1
RUN mkdir /var/www
WORKDIR /var/www
COPY requirements.txt /var/www/
RUN pip install -r requirements.txt
COPY . /var/www/


# CMD ["/bin/bash", "-c", "python manage.py runserver 0.0.0.0:8000"]