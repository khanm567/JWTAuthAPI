FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["JWTAuthAPI.csproj", "."]
RUN dotnet restore "JWTAuthAPI.csproj"
COPY . .
RUN dotnet build "JWTAuthAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JWTAuthAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JWTAuthAPI.dll"]