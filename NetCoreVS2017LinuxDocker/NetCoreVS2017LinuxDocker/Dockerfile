FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 24532
EXPOSE 44378

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["NetCoreVS2017LinuxDocker/NetCoreVS2017LinuxDocker.csproj", "NetCoreVS2017LinuxDocker/"]
RUN dotnet restore "NetCoreVS2017LinuxDocker/NetCoreVS2017LinuxDocker.csproj"
COPY . .
WORKDIR "/src/NetCoreVS2017LinuxDocker"
RUN dotnet build "NetCoreVS2017LinuxDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreVS2017LinuxDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreVS2017LinuxDocker.dll"]