FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /app
EXPOSE 80

LABEL maintainer="petar.gjeorgiev@interworks.com.mk"

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "BlogApp.dll"]
