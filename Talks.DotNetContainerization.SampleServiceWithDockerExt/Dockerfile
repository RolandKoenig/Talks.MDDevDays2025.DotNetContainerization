#####################################
# Build image
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Restore first for improved cache usage
COPY "Talks.DotNetContainerization.SampleServiceWithDocker/Talks.DotNetContainerization.SampleServiceWithDocker.csproj" "Talks.DotNetContainerization.SampleServiceWithDocker/Talks.DotNetContainerization.SampleServiceWithDocker.csproj"
RUN dotnet restore "Talks.DotNetContainerization.SampleServiceWithDocker/Talks.DotNetContainerization.SampleServiceWithDocker.csproj"

# Build the application
COPY . .
WORKDIR "/src/Talks.DotNetContainerization.SampleServiceWithDocker"
RUN dotnet build "Talks.DotNetContainerization.SampleServiceWithDocker.csproj" -c Release -o /app/build

# Publish the application to /app/publish
FROM build AS publish
RUN dotnet publish "Talks.DotNetContainerization.SampleServiceWithDocker.csproj" -c Release -o /app/publish /p:UseAppHost=false

#####################################
# Runtime image
## Configure OS
FROM mcr.microsoft.com/dotnet/aspnet:9.0-alpine AS final
EXPOSE 80

## Create a group, user and work directory for the application
RUN mkdir /home/app/net && \
    chown -R app:app /home/app/net
WORKDIR /home/app/net

## Copy application and define entrypoint
USER app
COPY --chown=app:app --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Talks.DotNetContainerization.SampleServiceWithDocker.dll"]