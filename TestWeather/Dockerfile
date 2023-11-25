FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src
COPY ["TestWeather/TestWeather.csproj", "TestWeather/"]
RUN dotnet restore "TestWeather/TestWeather.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "TestWeather/TestWeather.csproj" -c Release -o /app/build
#RUN dotnet test "DockerCourseApi.Tests.Integration/DockerCourseApi.Tests.Integration.csproj"
RUN dotnet publish "TestWeather/TestWeather.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:7.0
EXPOSE 80
EXPOSE 443
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "TestWeather.dll"]
