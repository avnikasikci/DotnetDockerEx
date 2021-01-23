# FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
# WORKDIR /app

# # Copy csproj and restore as distinct layers
# COPY *.csproj ./
# RUN dotnet restore

# # Copy everything else and build
# COPY . ./
# RUN dotnet publish -c Release -o out

# # Build runtime image
# FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
# WORKDIR /app
# COPY --from=build-env /app/out .
# ENTRYPOINT ["dotnet", "aspnetcoreapp.dll"]

# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.csproj .
RUN dotnet restore

# copy and publish app and libraries
COPY . .
RUN dotnet publish -c release -o /app --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/runtime:5.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "aspnetcoreapp.dll"]



# # https://hub.docker.com/_/microsoft-dotnet
# FROM mcr.microsoft.com/dotnet/sdk:2.2 AS build-env
#  WORKDIR /app
# # WORKDIR /source

# # copy csproj and restore as distinct layers
# COPY *.sln .
# COPY aspnetcoreapp/*.csproj ./aspnetcoreapp/
# RUN dotnet restore

# # copy everything else and build app
# COPY aspnetapp/. ./aspnetapp/
# WORKDIR /source/aspnetapp
# RUN dotnet publish -c release -o /app --no-restore

# # final stage/image
# FROM mcr.microsoft.com/dotnet/aspnet:5.0
# WORKDIR /app
# COPY --from=build /app ./
# ENTRYPOINT ["dotnet", "aspnetcoreapp.dll"]