FROM python:3.9.6
RUN apt update
# Upgrade pip 
RUN python3 -m pip install --upgrade pip
RUN python -m venv /venv
COPY ./app/requirements.txt /
RUN . venv/bin/activate && python -m pip install psycopg2 && python -m pip install -r requirements.txt
COPY ./app /app
ENV SECRET_KEY=b'kepWAzz432vra5QC@TE5'
#ENV SESSION_TYPE=redis
#ENV SESSION_REDIS=redis://redis:6379
ENV FLASK_APP=app.app.py
ENV VIRTUAL_ENV=/venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"
#COPY ./app/config /config
COPY ./docker/docker_entrypoint.sh /
RUN chmod +x /docker_entrypoint.sh
WORKDIR /
EXPOSE 8000

ENTRYPOINT [ "./docker_entrypoint.sh" ]
CMD [ "flask", "run", "--host", "0.0.0.0", "--port", "8000" ]