FROM mcr.microsoft.com/dotnet/sdk:10.0-noble AS build
WORKDIR /src

COPY ["KIFRIOSSE.ASTFRI.Web.API/KIFRIOSSE.ASTFRI.Web.API.csproj", "KIFRIOSSE.ASTFRI.Web.API/"]
COPY ["KIFRIOSSE.ASTFRI.SDK/KIFRIOSSE.ASTFRI.SDK.csproj", "KIFRIOSSE.ASTFRI.SDK/"]
RUN dotnet restore "KIFRIOSSE.ASTFRI.Web.API/KIFRIOSSE.ASTFRI.Web.API.csproj"

COPY . .
WORKDIR "/src/KIFRIOSSE.ASTFRI.Web.API"
RUN dotnet build "KIFRIOSSE.ASTFRI.Web.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KIFRIOSSE.ASTFRI.Web.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:10.0-noble AS final
WORKDIR /app

COPY --from=publish /app/publish .

# Štandardný port pre moderné ASP.NET Core aplikácie v kontajneri je 8080
EXPOSE 8080

ENTRYPOINT ["dotnet", "KIFRIOSSE.ASTFRI.Web.API.dll"]