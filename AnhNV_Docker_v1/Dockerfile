#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["AnhNV_Docker_v1/AnhNV_Docker_v1.csproj", "AnhNV_Docker_v1/"]
RUN dotnet restore "AnhNV_Docker_v1/AnhNV_Docker_v1.csproj"
COPY . .
WORKDIR "/src/AnhNV_Docker_v1"
RUN dotnet build "AnhNV_Docker_v1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AnhNV_Docker_v1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AnhNV_Docker_v1.dll"]