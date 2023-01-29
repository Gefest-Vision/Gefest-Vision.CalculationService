FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Gefest-Vision.CalculationService/Gefest-Vision.CalculationService.csproj", "Gefest-Vision.CalculationService/"]
RUN dotnet restore "Gefest-Vision.CalculationService/Gefest-Vision.CalculationService.csproj"
COPY . .
WORKDIR "/src/Gefest-Vision.CalculationService"
RUN dotnet build "Gefest-Vision.CalculationService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Gefest-Vision.CalculationService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Gefest-Vision.CalculationService.dll"]
