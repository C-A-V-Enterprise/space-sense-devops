FROM mcr.microsoft.com/dotnet/sdk:10.0-preview AS build
WORKDIR /src

COPY ["SpaceSense.Api.csproj", "./"]
RUN dotnet restore "./SpaceSense.Api.csproj"

COPY . .
RUN dotnet publish "SpaceSense.Api.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0-preview AS final
WORKDIR /app

COPY --from=build /app/publish .

# Cria usuário sem privilégios
RUN useradd -m appuser

# Dá permissão sobre a pasta da aplicação
RUN chown -R appuser:appuser /app

# Executa como usuário não-root
USER appuser

ENTRYPOINT ["dotnet", "SpaceSense.Api.dll"]
