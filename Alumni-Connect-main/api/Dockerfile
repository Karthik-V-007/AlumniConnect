FROM python
RUN groupadd --gid 1000 api
RUN useradd --uid 1000 --gid api --shell /bin/bash --create-home api
USER api
ENV PATH="/home/api/.local/bin:$PATH"
RUN mkdir /home/api/app
WORKDIR /home/api/app
COPY ./requirements.txt ./
RUN pip install --upgrade pip setuptools wheel
RUN pip install -r requirements.txt
EXPOSE 8000
COPY . .
CMD ["sh", "-c", "gunicorn api.wsgi:application --bind 0.0.0.0:${PORT:-8000} --workers ${WEB_CONCURRENCY:-1}"]
