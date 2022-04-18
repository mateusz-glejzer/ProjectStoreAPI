FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ProjectStore/ProjectStore.csproj", "ProjectStore/"]
RUN dotnet restore "ProjectStore/ProjectStore.csproj"
COPY . .
WORKDIR "/src/ProjectStore"
RUN dotnet build "ProjectStore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ProjectStore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ProjectStore.dll"]
