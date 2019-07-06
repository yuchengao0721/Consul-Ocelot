FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Client1.2/API1-2.csproj", "Client1.2/"]
COPY ["ConsulClient/ConsulRegister.csproj", "ConsulClient/"]
RUN dotnet restore "Client1.2/API1-2.csproj"
COPY . .
WORKDIR "/src/Client1.2"
RUN dotnet build "API1-2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "API1-2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "API1-2.dll"]
