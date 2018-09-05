#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 22776
EXPOSE 44365

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY ["NetCoreVS2017WindowDocker/NetCoreVS2017WindowDocker.csproj", "NetCoreVS2017WindowDocker/"]
RUN dotnet restore "NetCoreVS2017WindowDocker/NetCoreVS2017WindowDocker.csproj"
COPY . .
WORKDIR "/src/NetCoreVS2017WindowDocker"
RUN dotnet build "NetCoreVS2017WindowDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreVS2017WindowDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreVS2017WindowDocker.dll"]