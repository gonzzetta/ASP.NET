FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 51033
EXPOSE 44368

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY prueba1/prueba1.csproj prueba1/
RUN dotnet restore prueba1/prueba1.csproj
COPY . .
WORKDIR /src/prueba1
RUN dotnet build prueba1.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish prueba1.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "prueba1.dll"]
