```
docker run -it --rm \
  -v "$(pwd)/data:/data" \
  -e SYNAPSE_SERVER_NAME=server.com \
  -e SYNAPSE_REPORT_STATS=no \
  matrixdotorg/synapse:latest generate
```
