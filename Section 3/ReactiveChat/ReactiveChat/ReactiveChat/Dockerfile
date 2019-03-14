FROM microsoft/dotnet:3.0-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:3.0-sdk-stretch AS build
WORKDIR /src
COPY ["ReactiveChat/ReactiveChat.csproj", "ReactiveChat/"]
RUN dotnet restore "ReactiveChat/ReactiveChat.csproj"
COPY . .
WORKDIR "/src/ReactiveChat"
RUN dotnet build "ReactiveChat.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ReactiveChat.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ReactiveChat.dll"]