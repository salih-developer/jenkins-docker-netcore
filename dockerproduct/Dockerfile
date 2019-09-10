FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

# copy everything else and build app
COPY /. ./
WORKDIR /app
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/out ./
ENTRYPOINT ["dotnet", "dockerproduct.dll"]

#FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
#WORKDIR /src
#COPY ["dockerproduct/dockerproduct.csproj", "dockerproduct/"]
#RUN dotnet restore "dockerproduct/dockerproduct.csproj"
#COPY . .
#WORKDIR "/src/dockerproduct"
#RUN dotnet build "dockerproduct.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish "dockerproduct.csproj" -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "dockerproduct.dll"]