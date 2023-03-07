#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebAppPipeline.csproj", "WebAppPipeline/"]
RUN dotnet restore "WebAppPipeline/WebAppPipeline.csproj"
COPY . .
WORKDIR /src/
RUN dotnet build "WebAppPipeline/WebAppPipeline.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAppPipeline.csproj" -c Release -o /app/publish


FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
COPY  /wwwroot ./wwwroot

ENTRYPOINT ["dotnet", "WebAppPipeline.dll"]
