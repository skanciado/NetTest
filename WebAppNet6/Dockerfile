﻿#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app 
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app 
COPY . .
RUN dotnet restore "WebAppNet6.csproj" 
WORKDIR "/app"
RUN dotnet build "WebAppNet6.csproj"  -o /app/build

FROM build AS publish
RUN dotnet publish "WebAppNet6.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAppNet6.dll"]