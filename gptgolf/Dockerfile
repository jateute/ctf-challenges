FROM python:3.11

RUN addgroup --gid 1001 ctf && \
    yes | adduser --disabled-password --uid 1001 --ingroup ctf ctf && \
    mkdir /var/www && \
    chgrp ctf /var/www && \
    chmod g+w /var/www

ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1
ENV FLASK_DEBUG=0

ENV FLAGS="flag{example0},flag{example1},flag{example2},flag{example3},flag{example4}"
ENV RESET_PATH="/reset"

WORKDIR /usr/bin/gptgolf/src
COPY ./src/requirements.txt ./

RUN pip install -r requirements.txt

USER ctf

COPY --chown=ctf ./src ./

HEALTHCHECK --interval=10s --timeout=5s --retries=5 CMD [ "curl", "localhost:8080" ]

CMD ["gunicorn", "--bind", "0.0.0.0:8080", "run:app"]