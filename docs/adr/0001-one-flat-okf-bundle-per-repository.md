# One flat OKF bundle per repository

Each PythonEDA domain repository owns a single OKF bundle at `<org>/<repo>/okf/`, flat — no hexagonal-layer subdirectories inside it. The layers (domain / infrastructure / application) decompose at the repository level, each layer being its own repository with its own bundle. We chose flat per-repo over layer subdirectories or a single consolidated bundle because the repository is the unit of versioning and distribution, and the layers are slated to split into separate repositories (each of which will carry its own bundle).
