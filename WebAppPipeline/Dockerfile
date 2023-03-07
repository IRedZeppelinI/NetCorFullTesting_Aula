#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS publish
WORKDIR /src
COPY . .
RUN dotnet restore WebAppPipeline.csproj
RUN dotnet build WebAppPipeline.csproj -c Release -o /build/
RUN dotnet publish WebAppPipeline.csproj -c Release -o /publish/

FROM base AS final
WORKDIR /app
COPY --from=publish /src/bin/Release/net6.0/ .
COPY  /wwwroot ./wwwroot

ENTRYPOINT ["dotnet", "WebAppPipeline.dll"]
