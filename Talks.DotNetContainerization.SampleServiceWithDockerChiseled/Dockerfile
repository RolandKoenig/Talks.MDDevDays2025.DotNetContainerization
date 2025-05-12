#####################################
# Build image
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore "Talks.DotNetContainerization.SampleServiceWithDocker/Talks.DotNetContainerization.SampleServiceWithDocker.csproj"
WORKDIR "/src/Talks.DotNetContainerization.SampleServiceWithDocker"
RUN dotnet build "Talks.DotNetContainerization.SampleServiceWithDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Talks.DotNetContainerization.SampleServiceWithDocker.csproj" -c Release -o /app/publish /p:UseAppHost=false

#####################################
# Runtime image
## Configure OS
FROM mcr.microsoft.com/dotnet/aspnet:9.0-noble-chiseled AS final
EXPOSE 80

## Copy application and define entrypoint
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Talks.DotNetContainerization.SampleServiceWithDocker.dll"]