
FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM  microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY front.csproj front/
RUN dotnet restore front/front.csproj
WORKDIR /src/front
COPY . .
RUN dotnet build front.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish front.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "front.dll"]
