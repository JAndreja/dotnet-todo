# Build stage
# Use the official .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /source

# Copy the project files ,restore any dependencies and build the project
COPY . .
RUN dotnet restore ./src/TodoApi.csproj --disable-parallel
RUN dotnet publish TodoApi.csproj -c release -o /app --no-restore

# Server stage
FROM mcr.microsoft.com/dotnet/sdk:8.0
WORKDIR /app
COPY --from=build /app ./

EXPOSE 8090

# with this command we can access localy at local http://localhost:[port]

ENV ASPNETCORE_URLS http://*:8090

ENTRYPOINT ["dotnet", "TodoApi.dll"]