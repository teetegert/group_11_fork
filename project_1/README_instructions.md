* Maybe we do not need those :D :
* Pull a Python image, e.g. `docker pull python:3.13.2-slim-bookworm`
* Pull a Jupyter Pyspark image, e.g. `docker pull quay.io/jupyter/pyspark-notebook:spark-3.5.3`

#### Docker and compose.yml

* Review compose.yml. Maybe we can improve it and add some functionality. Right now the one from practise sessions is used
* `docker compose -f project_1/compose.yml up -d`
* when in project_1 directory then `docker compose -f compose.yml up -d`


* Review Jupyter UI (localhost:8888), run the example notebook
* Review Spark UI (localhost:4040)