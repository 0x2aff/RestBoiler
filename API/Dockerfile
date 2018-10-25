FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["BoilerRest/BoilerRest.csproj", "BoilerRest/"]
RUN dotnet restore "BoilerRest/BoilerRest.csproj"
COPY . .
WORKDIR "/src/BoilerRest"
RUN dotnet build "BoilerRest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BoilerRest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BoilerRest.dll"]