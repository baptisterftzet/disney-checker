FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DisneyChecker/DisneyChecker.csproj", "DisneyChecker/"]
RUN dotnet restore "DisneyChecker/DisneyChecker.csproj"
COPY . .
WORKDIR "/src/DisneyChecker"
RUN dotnet build "DisneyChecker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DisneyChecker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DisneyChecker.dll"]
