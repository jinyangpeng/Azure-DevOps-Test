#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
run ll
  
COPY ["Mindray.CustomerCenter.API.csproj", "Mindray.CustomerCenter.API/"]
RUN dotnet restore "src/Mindray.CustomerCenter.API/Mindray.CustomerCenter.API.csproj"
COPY . .
WORKDIR "/src/Mindray.CustomerCenter.API"
RUN dotnet build "Mindray.CustomerCenter.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Mindray.CustomerCenter.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Mindray.CustomerCenter.API.dll"]
