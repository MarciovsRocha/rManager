FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["rManager/rManager.csproj", "rManager/"]
RUN dotnet restore "rManager/rManager.csproj"
COPY . .
WORKDIR "/src/rManager"
RUN dotnet build "rManager.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "rManager.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "rManager.dll"]
