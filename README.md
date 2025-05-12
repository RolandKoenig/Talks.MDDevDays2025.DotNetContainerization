
## SampleServiceWithDocker
```powershell
docker build -f Talks.DotNetContainerization.SampleServiceWithDocker/Dockerfile -t sample-service-with-docker .
```

Show all processes inside the container
```bash
ls -l /proc/*/exe
```

## SampleServiceWithDockerExt
```powershell
docker build -f Talks.DotNetContainerization.SampleServiceWithDockerExt/Dockerfile -t sample-service-with-docker-ext .
```

## SampleServiceWithDockerChiseled
```powershell
docker build -f Talks.DotNetContainerization.SampleServiceWithDockerChiseled/Dockerfile -t sample-service-with-docker-chiseled .
```

## SampleServiceWithDockerBySdk
```powershell
dotnet publish Talks.DotNetContainerization.SampleServiceWithDockerBySdk/Talks.DotNetContainerization.SampleServiceWithDockerBySdk.csproj /t:PublishContainer
```