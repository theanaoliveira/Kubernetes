FROM mcr.microsoft.com/dotnet/core/runtime:3.1-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["csharp-demo.csproj", "csharp-demo/"]

RUN dotnet restore "csharp-demo/csharp-demo.csproj"
COPY . .

WORKDIR "/src/csharp-demo"
COPY . .
RUN dotnet build "csharp-demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "csharp-demo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "csharp-demo.dll"]