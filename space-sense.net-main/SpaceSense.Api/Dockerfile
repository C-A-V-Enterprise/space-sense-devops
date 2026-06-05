# Build Stage
FROM mcr.microsoft.com/dotnet/sdk:10.0-preview AS build
WORKDIR /src

COPY ["SpaceSense.Api.csproj", "./"]
RUN dotnet restore "./SpaceSense.Api.csproj"

COPY . .
WORKDIR "/src/."
RUN dotnet build "SpaceSense.Api.csproj" -c Release -o /app/build
RUN dotnet publish "SpaceSense.Api.csproj" -c Release -o /app/publish

# Runtime Stage
FROM mcr.microsoft.com/dotnet/aspnet:10.0-preview AS final
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["dotnet", "SpaceSense.Api.dll"]
