#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["TargetingFeatureFlagsEntraID/TargetingFeatureFlagsEntraID.csproj", "TargetingFeatureFlagsEntraID/"]
RUN dotnet restore "TargetingFeatureFlagsEntraID/TargetingFeatureFlagsEntraID.csproj"
COPY . .
WORKDIR "/src/TargetingFeatureFlagsEntraID"
RUN dotnet build "TargetingFeatureFlagsEntraID.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TargetingFeatureFlagsEntraID.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TargetingFeatureFlagsEntraID.dll"]