# pkl-python-logging

⚠️ Still in alpha. Open an issue if you'd like to help! ⚠️

A [Pkl](https://pkl-lang.org/) template for writing [Python logging configurations](https://docs.python.org/3/library/logging.config.html#dictionary-schema-details).

## Prerequisites

- The [Pkl CLI](https://pkl-lang.org/main/current/pkl-cli/index.html#installation)

## Usage


### 1. Extend the template

```pkl
amends "package://pkg.pkl-lang.org/github.com/edgarrmondragon/pkl-python-logging/org.python.Logging@[LATEST_VERSION]#/PythonLogging.pkl"

// Define the logging configuration
disable_existing_loggers = false
formatters = new Mapping {
    ["simple"] = new Formatter {
        format = "%(levelname)-8s - %(message)s"
    }
}
handlers = new Mapping {
    ["stdout"] = new Handler {
        `class` = "logging.StreamHandler"
        level = "INFO"
        formatter = "simple"
        kwargs = new Mapping {
            ["stream"] = "ext://sys.stdout"
        }
    }
    ["stderr"] = new Handler {
        `class` = "logging.StreamHandler"
        level = "ERROR"
        formatter = "simple"
        kwargs = new Mapping {
            ["stream"] = "ext://sys.stderr"
        }
    }
    ["file"] = new Handler {
        `class` = "logging.FileHandler"
        formatter = "simple"
        kwargs = new Mapping {
            ["filename"] = "app.log"
            ["mode"] = "w"
        }
    }
}
root = new BaseLogger {
    level = "DEBUG"
    handlers = List(
        "stderr",
        "stdout",
        "file"
    )
}
```

### 2. Convert the Pkl file

```bash
pkl eval examples/snippet.pkl  --format=json
```

## Examples

See the [examples](examples) directory.

## Acknowledgements

- The [Pkl](https://pkl-lang.org/) team.
- [StefMa](https://github.com/StefMa) for publishing [pkl-gha](https://github.com/StefMa/pkl-gha), which was used as a reference for this template.
