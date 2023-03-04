# build
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source
COPY . ./
RUN dotnet restore "./API/API.csproj" --disable-parallel
RUN dotnet publish "./API/API.csproj" -c Release -o /app --no-restore

# serve
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
# copy artifacts from build stage's app directory to current working dir
COPY --from=build /app ./
EXPOSE 5000
ENTRYPOINT ["dotnet", "API.dll"]