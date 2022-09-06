# FAE Common Voice 2022   

### Foreign-Accented English from the crowdsourced [Common Voice corpus](https://commonvoice.mozilla.org/en).

### Design Criteria:

- Use `validated.tsv` recordings only from `cv-corpus-10.0-2022-07-04`.
- ~20sec per speaker.
- ~100-500 speakers per accent-class.
- Favor speaker diversity and gender balance.

---

#### Requirements.

- Install docker-compose version > 1.29 or [Compose V2](https://www.docker.com/blog/announcing-compose-v2-general-availability/) preferrably.
- Create a `.env` file and define these variable:
  - `PATH_CORPORA=/local/directory/where/cv/was/downloaded/`
  - `PORT_JUPY=8888` # local port of choice

For example `.env`:
```
PATH_CORPORA=/data/corpora/CommonVoice
PORT_JUPY=0  # 0 picks random port
```

---

#### Build docker image.

Note: If using Compose V2, simply replace `docker-compose` with `docker compose`.

```
docker-compose build
```

#### Run docker container.

```
docker-compose -p fae$USER up -d --force-recreate
```

#### Running Jupyter notebook

Find the assigned local port by inspecting

```
docker-compose -p fae$USER ps
       Name                    Command                 State                         Ports                   
-------------------------------------------------------------------------------------------------------------
faejsmith_FAECV_1   tini -g -- start-notebook.sh   Up (healthy)   0.0.0.0:49153->8888/tcp,:::49153->8888/tcp
```

The container is listening to that port: http://server:49153/

Find the corresponding access token in the container logs:

```
docker-compose -p fae$USER logs
```

