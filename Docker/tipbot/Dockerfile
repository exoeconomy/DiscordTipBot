FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env

ARG discordUrlRepo
ARG discordRepoName

WORKDIR /app
RUN apt-get update && apt-get install -y git

# Discord Tipbot Github Repo
RUN git clone ${discordUrlRepo}
WORKDIR /app/${discordRepoName}/TipBot

# restore as distinct layers
RUN dotnet restore

# build binaries
RUN dotnet publish -c Release
WORKDIR /app/${discordRepoName}/TipBot/bin/Release/netcoreapp2.1

# Build runtime image
ENTRYPOINT exec dotnet TipBot.dll -daemonUrl="${daemonUrl}" -rpcUsername="${rpcUsername}" -rpcPassword="${rpcPassword}" -walletPassword="${walletPassword}" -token="${token}" -connectionString="${connectionString}"
