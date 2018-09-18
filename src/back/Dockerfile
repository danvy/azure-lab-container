FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 81
ENV ASPNETCORE_URLS=http://+:81

FROM  microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY back.csproj back/
RUN dotnet restore back/back.csproj
WORKDIR /src/back
COPY . .
RUN dotnet build back.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish back.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "back.dll"]
