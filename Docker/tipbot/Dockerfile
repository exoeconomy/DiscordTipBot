FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env

RUN apt-get update && apt-get install -y git
WORKDIR /app

COPY ./ .
WORKDIR /app/TipBot

COPY /Docker/tipbot/Logo.png /app/TipBot/Content/

# restore as distinct layers
RUN dotnet restore

# build binaries
RUN dotnet publish -c Release
WORKDIR /app/TipBot/bin/Release/netcoreapp2.1

# Build runtime image
ENTRYPOINT exec dotnet TipBot.dll -daemonUrl="${daemonUrl}" -rpcUsername="${rpcUsername}" -rpcPassword="${rpcPassword}" -walletPassword="${walletPassword}" -token="${token}" -connectionString="${connectionString}"
