#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

ENV TZ="Europe/Paris"

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["TimeZoneLinuxContainerDateTime/TimeZoneLinuxContainerDateTime.csproj", "TimeZoneLinuxContainerDateTime/"]
RUN dotnet restore "TimeZoneLinuxContainerDateTime/TimeZoneLinuxContainerDateTime.csproj"
COPY . .
WORKDIR "/src/TimeZoneLinuxContainerDateTime"
RUN dotnet build "TimeZoneLinuxContainerDateTime.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TimeZoneLinuxContainerDateTime.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TimeZoneLinuxContainerDateTime.dll"]