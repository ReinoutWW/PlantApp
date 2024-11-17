# Build Stage
FROM --platform=linux/arm64 mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG TARGETARCH=arm64
WORKDIR /src

# Copy and restore dependencies
COPY ["PlantApplication.csproj", "."]
RUN dotnet restore -a $TARGETARCH

# Copy remaining source code and publish the app
COPY . .
RUN dotnet publish -a $TARGETARCH --no-restore -o /app/publish

# Runtime Stage
FROM --platform=linux/arm64 mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["dotnet", "PlantApplication.dll"]