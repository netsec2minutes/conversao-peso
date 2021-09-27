FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS DOTNET
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS STAGE01
WORKDIR /app
COPY ./ConversaoPeso.Web.csproj ./
RUN dotnet restore "./ConversaoPeso.Web.csproj"
COPY . .
WORKDIR "/app/."

FROM STAGE01 AS publish
RUN dotnet publish "ConversaoPeso.Web.csproj" -c Release -o /app/publish

FROM DOTNET AS STAGE02
WORKDIR /app
EXPOSE 5678
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]
