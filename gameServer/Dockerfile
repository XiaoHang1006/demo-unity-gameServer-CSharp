FROM microsoft/dotnet:2.0-sdk AS build-env
WORKDIR /app

# copy csproj and restore as distinct layers

COPY *.csproj ./
RUN dotnet restore

EXPOSE 7777

# copy and build everything else
COPY . ./
RUN dotnet publish -c Release -o out

# build runtime image
FROM microsoft/dotnet:2.0-runtime 
WORKDIR /app
COPY --from=build-env /app/out ./
ADD conf ./conf

ENTRYPOINT ["dotnet", "gameServer.dll"]
