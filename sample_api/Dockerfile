#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["sample_api/sample_api.csproj", "sample_api/"]
RUN dotnet restore "sample_api/sample_api.csproj"
COPY . .
WORKDIR "/src/sample_api"
RUN dotnet build "sample_api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "sample_api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "sample_api.dll"]