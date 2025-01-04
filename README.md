# Data Engineering. Practice #1.

[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/README.md)
[![pt-br](https://img.shields.io/badge/lang-ru--ru-green.svg)](https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/README.ru-ru.md)

## Report

### Stage 1. Setup

Cloned repo named `Prerequisites`

    git clone https://github.com/ssau-data-engineering/Prerequisites.git

Run all necessary commands from [this practice guide](https://github.com/ssau-data-engineering/Prerequisites#%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BE%D0%BA-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0).

### Stage 2. Airflow + EK

Got up and runngin Airflow and EK

    docker compose -f docker-compose.airflow.yaml up --build -d
    docker compose -f docker-compose.elasticsearch.yaml up --build -d

I spent some time at this point trying to login in Airflow WebUI (didn't see credentials in practice guide) and so I created user myself.


Created the following Airflow graph

<p align="center">
  <img width="800" height="300" src="https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/screenshots/resulting_graph.png"/>
</p>

Copied file with graph definition in container with Airflow.

Run graph via Airflow WebUI (it took 25 tries to achieve success). Encountered various issues with documentation understanding. Several times rewrote code from scratch (gradually refined it).

<p align="center">
  <img width="600" height="350" src="https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/screenshots/total_runs.png"/>
</p>

Defined task <i><b>save_to_elastic</b></i> after reading EK documentation and building several dashboards.

Created dashboard only after I had created Kibana index pattern and uploaded data.

<p align="center">
  <img width="600" height="300" src="https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/screenshots/airflow-kibana-panel.png"/>
</p>

The plot above shows how mean vine's score depends on it's price.

For better showcase plotted mean price against points.

<p align="center">
  <img width="600" height="300" src="https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/screenshots/airflow-kibana-panel2.png"/>
</p>

### Stage 3. Apache Nifi

Created graph via WebUI.

<p align="center">
  <img width="800" height="400" src="https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/screenshots/nifi-graph.png"/>
</p>

While doing this part, I encountered bug in my graph, that made `GetFile` continously read files from source directory and trash memory with them. All due set flag `keepSourceFiles` in `GetFile`.

Plot in Kibana identical to the plot in previous stage.

<p align="center">
  <img width="600" height="300" src="https://github.com/Anteii/ssau-data-engineering-lab-1/blob/main/screenshots/nifi-kibana-panel.png"/>
</p>

### Stage 4. Conclusion

NiFi as a no-code (or low-code) solution has it's own limitations and a certain stiffnes to it. It gets complicated to work with UI beyond simple tasks and requires better understanding of this tool. Airflow, on the other hand, requires to write code, but feels more natural / pleasant to work with (at least for those who familiar with Python).