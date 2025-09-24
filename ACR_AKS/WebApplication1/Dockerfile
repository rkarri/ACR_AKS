# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore
COPY ["ACR_AKS/WebApplication1/RaviK.CICD.API.csproj", "WebApplication1/"]
RUN dotnet restore "WebApplication1/RaviK.CICD.API.csproj"

# Copy everything else
COPY . .
WORKDIR "/src/ACR_AKS/WebApplication1"
RUN dotnet build "RaviK.CICD.API.csproj" -c Release -o /app/build

# Publish
RUN dotnet publish "RaviK.CICD.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "RaviK.CICD.API.dll"]
