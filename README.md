# A SUMO Docker container 

Containerized version of Sumo. 

## Obtain 

Get the executable container via:

```
  git clone https://github.com/aladinoster/docker-sumo.git
```


## Build 

Go inside `docker-sumo/build-sumo`

```
 docker build --rm -f "Dockerfile" -t local:sumo "." 
```

**Note**: Source files are not included for licenses purposes. 


## Run 

```
  docker run --rm -it local:sumo
```