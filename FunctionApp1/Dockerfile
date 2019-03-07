FROM mcr.microsoft.com/azure-functions/dotnet AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src

COPY FunctionApp1/FunctionApp1.csproj FunctionApp1/
RUN dotnet restore FunctionApp1/FunctionApp1.csproj
COPY . .
WORKDIR /src/FunctionApp1
RUN dotnet build FunctionApp1.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish FunctionApp1.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FunctionApp1.dll"]
