FROM mcr.microsoft.com/dotnet/core/runtime:3.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["DatingApp.API.csproj", "./"]
RUN dotnet restore "./DatingApp.API.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DatingApp.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DatingApp.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DatingApp.API.dll"]