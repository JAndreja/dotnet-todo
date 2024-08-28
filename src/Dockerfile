# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /source
COPY . .

# works for github actions
RUN dotnet restore ./src/TodoApi.csproj --disable-parallel
RUN dotnet publish ./src/TodoApi.csproj -c release -o /app --no-restore

# works for local
#RUN dotnet restore TodoApi.csproj --disable-parallel
#RUN dotnet publish TodoApi.csproj -c release -o /app --no-restore

# Server stage
FROM mcr.microsoft.com/dotnet/sdk:8.0
WORKDIR /app
COPY --from=build /app ./

EXPOSE 8090

# for accessing localy http://localhost:[localport]
ENV ASPNETCORE_URLS http://*:8090

ENTRYPOINT ["dotnet", "TodoApi.dll"]
