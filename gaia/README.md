## Gaia  

A first attempt to put the OHDSI GIS working group Gaia assemblage all together in Broadsea. This builds on Jared's initial containerization implementation on the ['containerize' branch](https://github.com/TuftsCTSI/GIS/tree/containerize) of https://github.com/TuftsCTSI/GIS/.  

At to level of the Broadsea-GISland repository run:  
`$ docker compose --profile gaia-core up -d`

If the gaia-core image fails to build with docker compose, then build it from docker and rerun the above command:  
`$ docker build -t gaia-core -f gaia/gaia-core/Dockerfile .`

Notes:
- Still very proof of concept. at this stage it runs four Gaia containers
   - gaia-core
   - gaia-solr
   - gaia-db
   - gaia-catalog
- It also runs the
   - Network broadsea-gisland_default
   - traefik (default webserver from what I understand)
- All containers can see each other on their local docker network
- http://gaia-core:8000/load?variable_id=id will load a variable into the database .... but this is currently failing in the createGeomInstanceTable() function with a problematic 'DEAFULT' keyword in the SQL statement ...
- For this integration with the catalog, the gaia-core needs the "plumber" r package, currently this is installed in the Dockerfile, but should be moved to the actual Gaia R Package
- It may be good to do a major refactor of where things are in the current OHDSI/GIS repository. I like Jared's idea of a docker folder, and move everything docker related out of the inst folder (as it currently is), then we could modify the Broadsea docker-compose to install from git (and *not* keep the gaia Dockerfiles on Broadsea)
