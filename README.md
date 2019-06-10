# Run shiny app in singularity container

In singularity we have recipes, which are files to define custom containers. So I made simple one from modified example shinyproxy docker image:

 ```
Bootstrap: docker

From: kfoltynski/shinyproxy-demo:singularity


%runscript

    echo "Running Shiny app on port $*"

    exec R -e "shinyproxy::run_01_hello($@)"
 ```

Then container needs to be build:

```
 sudo singularity build shiny.simg Singularity.recipe
```

and then container can be run with custom port of app:

```
singularity run shiny.simg 3839
```

or started as system service:

```
singularity instance start shiny.simg shiny 3839

```
**NOTE**: Building image from recipe requires `sudo`.