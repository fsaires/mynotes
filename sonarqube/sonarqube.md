## SONARQUBE

- Executar Scanner no docker

```
$ docker run -e SONAR_HOST_URL=http://localhost:9000 -e SONAR_TOKEN=<TOKEN> -it -v ${pwd}:/data --network <NETWORK> --rm sonarsource/sonar-scanner-cli sonar-runner
```