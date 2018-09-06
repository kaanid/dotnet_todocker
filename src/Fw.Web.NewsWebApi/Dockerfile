FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["src/Fw.Web.NewsWebApi/Fw.Web.NewsWebApi.csproj", "src/Fw.Web.NewsWebApi/"]
RUN dotnet restore "src/Fw.Web.NewsWebApi/Fw.Web.NewsWebApi.csproj"
COPY . .
WORKDIR "/src/src/Fw.Web.NewsWebApi"
RUN dotnet build "Fw.Web.NewsWebApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Fw.Web.NewsWebApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Fw.Web.NewsWebApi.dll"]