![ASync API RI and CTK Architecture](https://github.com/tmforum-rand/async-api-assets/blob/main/TMF-Specmatic-AsyncAPI-RI-CTK-Arch.gif?raw=true)

# Instructions

## 1. Start the reference implementation

*IMPORTANT NOTES:*
- Please ensure you have stopped any other RI before starting this RI.
- Please ensure you are on Docker Desktop 4.27.2 or lower (download Docker Desktop 4.27.2 from https://docs.docker.com/desktop/release-notes/#4272).

```shell | powershell
docker compose -f *-async-ri.yaml pull
docker compose -f *-async-ri.yaml down
docker compose -f *-async-ri.yaml up --build
```

## 2. Check if the following are working
* [Mongo DB Compass](http://admin:password@localhost:8081/)
* [KafDrop and Async API Bridge](http://localhost:9000)

## 3. Check if HTTP RI is working
Run the below command and open the outputted URL in your browser:

### Linux/MacOS
```shell
DOCKER_CLI_HINTS=false docker exec $(docker ps --format '{{.Names}}' | grep http-ri) sh -c "curl -sL http://localhost:$(docker ps --format '{{.Names}}:{{.Ports}}' | grep http-ri | sed -n 's/.*:\([0-9]*\)->.*/\1/p' | head -1) | grep swagger-ui | sed 's/.*localhost/http:\/\/localhost/' | sed 's/api-docs.*/api-docs/'"
```
OR

### Windows
```powershell
$env:DOCKER_CLI_HINTS = "false"
docker exec $(docker ps --format '{{.Names}}' | grep http-ri) sh -c "curl -sL http://localhost:$(docker ps --format '{{.Names}}:{{.Ports}}' | grep http-ri | sed -n 's/.*:\([0-9]*\)->.*/\1/p' | head -1) | grep swagger-ui | sed 's/.*localhost/http:\/\/localhost/' | sed 's/api-docs.*/api-docs/'"
```
