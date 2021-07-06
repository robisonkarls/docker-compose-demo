FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY "DockerComposeDemo.csproj" "DockerComposeDemo.csproj"

RUN dotnet restore

COPY . .

WORKDIR /src/DockerComposeDemo

RUN dotnet publish --no-restore -c Release -o /app --no-cache /restore

FROM build AS publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerComposeDemo.dll"]
