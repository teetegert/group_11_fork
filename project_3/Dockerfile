FROM quay.io/jupyter/pyspark-notebook:spark-3.5.3

# Run setup commands as root
USER root

# ✅ Add Delta Lake JAR (needed for DeltaCatalog support)
RUN curl -L -o ${SPARK_HOME}/jars/delta-spark_2.12-3.0.0.jar \
    https://repo1.maven.org/maven2/io/delta/delta-spark_2.12/3.0.0/delta-spark_2.12-3.0.0.jar

# ✅ Add GraphFrames JAR (needed for GraphFrame JVM support)
RUN curl -L -o ${SPARK_HOME}/jars/graphframes-0.8.4-spark3.5-s_2.12.jar \
    https://repos.spark-packages.org/graphframes/graphframes/0.8.4-spark3.5-s_2.12/graphframes-0.8.4-spark3.5-s_2.12.jar

# ✅ Install Python packages
RUN mamba install --yes 'delta-spark' && \
    pip install graphframes && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# ✅ Add Delta config to Spark
RUN echo 'spark.sql.extensions io.delta.sql.DeltaSparkSessionExtension' >> "${SPARK_HOME}/conf/spark-defaults.conf" && \
    echo 'spark.sql.catalog.spark_catalog org.apache.spark.sql.delta.catalog.DeltaCatalog' >> "${SPARK_HOME}/conf/spark-defaults.conf"

# Return to default user
USER ${NB_UID}

# Optional: Trigger JAR download by initializing a dummy Delta session
RUN echo "from pyspark.sql import SparkSession" > /tmp/init-delta.py && \
    echo "from delta import *" >> /tmp/init-delta.py && \
    echo "spark = configure_spark_with_delta_pip(SparkSession.builder).getOrCreate()" >> /tmp/init-delta.py && \
    python /tmp/init-delta.py && \
    rm /tmp/init-delta.py
