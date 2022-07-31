#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Rezume/Rezume.csproj", "Rezume/"]
RUN dotnet restore "Rezume/Rezume.csproj"
COPY . .
WORKDIR "/src/Rezume"
RUN dotnet build "Rezume.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Rezume.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Rezume.dll"]