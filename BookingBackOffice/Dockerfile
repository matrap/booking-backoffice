FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["BookingBackOffice/BookingBackOffice.csproj", "BookingBackOffice/"]
RUN dotnet restore "BookingBackOffice/BookingBackOffice.csproj"
COPY . .
WORKDIR "/src/BookingBackOffice"
RUN dotnet build "BookingBackOffice.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BookingBackOffice.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BookingBackOffice.dll"]