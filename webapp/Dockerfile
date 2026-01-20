#write Docker code here

# ---------- BUILD STAGE ----------
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /app

# Copy entire repo
COPY . .

# Restore ONLY Web project (correct full path)
RUN dotnet restore /app/src/Web/Web.csproj

# Publish Web project
RUN dotnet publish /app/src/Web/Web.csproj -c Release -o /app/publish

# ---------- RUNTIME STAGE ----------
FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app

COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Web.dll"]

