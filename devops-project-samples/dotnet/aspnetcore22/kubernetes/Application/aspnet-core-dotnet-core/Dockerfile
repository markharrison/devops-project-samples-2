FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["aspnet-core-dotnet-core/aspnet-core-dotnet-core.csproj", "aspnet-core-dotnet-core/"]
RUN dotnet restore "aspnet-core-dotnet-core/aspnet-core-dotnet-core.csproj"
COPY . .
WORKDIR "/src/aspnet-core-dotnet-core"
RUN dotnet build "aspnet-core-dotnet-core.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aspnet-core-dotnet-core.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnet-core-dotnet-core.dll"]