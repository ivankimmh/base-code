FROM python:3.11-slim

ARG APP_NAME=/app

ENV PYTHONUNBUFFERED 1 
ENV PYTHONDONTWRITEBYTECODE 1 

WORKDIR ${APP_NAME}

COPY ./requirements.txt ./

RUN pip install --upgrade pip
RUN apt-get update && apt-get upgrade -y && apt-get install -y build-essential
RUN pip install --no-cache-dir -r requirements.txt

COPY . ${APP_NAME}

COPY ./scripts/start.sh /start
RUN sed -i 's/\r$//g' /start
RUN chmod +x /start

COPY ./scripts/entrypoint.sh /entrypoint
RUN sed -i 's/\r$//g' /entrypoint
RUN chmod +x /entrypoint

ENTRYPOINT ["/entrypoint"]
CMD ["/start"]