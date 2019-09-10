FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["dockersecurity/dockersecurity.csproj", "dockersecurity/"]
RUN dotnet restore "dockersecurity/dockersecurity.csproj"
COPY . .
WORKDIR "/src/dockersecurity"
RUN dotnet build "dockersecurity.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "dockersecurity.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockersecurity.dll"]