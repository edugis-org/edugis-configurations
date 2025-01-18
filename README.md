# EduGIS Atlas configurations

This repository is a collection of Atlas configurations. Such a configuration is defined in a JSON file. Configurations can be loaded into the [edugis-viewer](https://github.com/edugis-repo/edugis-viewer) by setting parameter ```configurl``` in the hash of the URL.

Example:
```
https://kaart.edugis.nl/v2#configurl=https://raw.githubusercontent.com/edugis-repo/edugis-configurations/refs/heads/master/layers.json
```

This repository is also a submodule of the [edugis-viewer](https://github.com/edugis-repo/edugis-viewer). The contents of this repostory can be pulled into the edugis-viewer repository with the following commands:

1. at clone time:
    ```bash
    git clone --recurse-submodules https://github.com/edugis-repo/edugis-viewer
    ```
2. after the clone is created:
    ```bash
    git submodule update --init
    ```

When used as submodule, the configurl parameter can be a relative path and will usually load faster than directly loading from github.  
Example configuration defined in a relative path (maps/layers.json):
```
https://kaart.edugis.nl/v2#configurl=maps/layers.json
```