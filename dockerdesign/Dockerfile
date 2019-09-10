FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

# copy everything else and build app
COPY dockerdesign/. ./dockerdesign/
WORKDIR /app/dockerdesign
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/dockerdesign/out ./
ENTRYPOINT ["dotnet", "dockerdesign.dll"]

#FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
#WORKDIR /src
#COPY ["dockerdesign/dockerdesign.csproj", "dockerdesign/"]
#RUN dotnet restore "dockerdesign/dockerdesign.csproj"
#COPY . .
#WORKDIR "/src/dockerdesign"
#RUN dotnet build "dockerdesign.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish "dockerdesign.csproj" -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "dockerdesign.dll"]
#
## docker run -d -p 8085:80 --name dockerdesign dockerdesign:latest