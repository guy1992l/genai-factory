# GenAI Factory

Demo an end to end LLM agent solution with modular architecture, persistent storage and front-end UI that can work with various LLM models and storage solutions.

the configuration is specified in a YAML file, which indicate the model, embeddings, storage to use, and various parameters. 
the user can point to the configuration file by setting the `AGENT_CONFIG_PATH` environment variable.

environment variables and credentials can be loaded from a `.env` file in the root directory. or an alternate path set by the `AGENT_ENV_PATH` environment variable.
data can be stored in local files or remote SQL and Vector databases. the local file storage path can be set by the `AGENT_DATA_PATH` environment variable (defaults to `./data/`).

# Getting it to work

## Deploy the controller
This command will start the API controller server into a local docker container.
```shell
make controller
```

## Initialize the database:
The database is Initialized when building the controller.
In order to erase and start fresh, we can simply use the controller's command line interface.

```shell
python -m controller.src.main initdb
```

## To start the application's API:

```shell
uvicorn pipeline:app
```

## To start UI:
Future work will include a UI command to run the UI.
```shell
make ui
```

# CLI usage

To ingest data into the vector database:
```shell
python -m controller.src.main ingest -l web https://milvus.io/docs/overview.md
```

To ask a question:
```shell   
python -m controller.src.main query "What is a vector?" 
```


Full CLI:

```shell
python -m controller.src.main

Usage: python -m controller.src.main [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  config  Print the config as a yaml file
  ingest  Ingest documents into the vector database
  initdb  Initialize the database (delete old tables)
  list    List the different objects in the database (by category)
  query   Run a chat query on the vector database collection
```
