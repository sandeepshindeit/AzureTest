FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56410
EXPOSE 44329

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AzureTest/AzureTest.csproj", "AzureTest/"]
RUN dotnet restore "AzureTest/AzureTest.csproj"
COPY . .
WORKDIR "/src/AzureTest"
RUN dotnet build "AzureTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AzureTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AzureTest.dll"]