#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app 
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /app 
COPY . .
RUN dotnet restore "WebAppNet31.csproj" 
WORKDIR "/app"
RUN dotnet build "WebAppNet31.csproj"  -o /app/build

FROM build AS publish
RUN dotnet publish "WebAppNet31.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAppNet31.dll"]