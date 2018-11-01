FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 55233
EXPOSE 44317

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY . NewProject/
RUN dotnet restore "NewProject/NewProject.csproj"
COPY . .
WORKDIR "/src/NewProject"
RUN dotnet build "NewProject.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NewProject.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NewProject.dll"]