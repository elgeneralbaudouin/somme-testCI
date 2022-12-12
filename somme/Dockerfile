#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["somme/somme.csproj", "somme/"]
RUN dotnet restore "somme/somme.csproj"
COPY . .
WORKDIR "/src/somme"
RUN dotnet build "somme.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "somme.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "somme.dll"]