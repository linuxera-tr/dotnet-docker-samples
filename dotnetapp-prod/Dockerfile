FROM 2.1-sdk-alpine AS build-env
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./
COPY *.config ./
RUN dotnet restore

# copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# build runtime image
FROM microsoft/dotnet-nightly:2.1-runtime-alpine
WORKDIR /app
COPY --from=build-env /app/out ./
ENTRYPOINT ["dotnet", "dotnetapp.dll"]
