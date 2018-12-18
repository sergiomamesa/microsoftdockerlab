FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DocsMicrosoftLab/DocsMicrosoftLab.csproj", "DocsMicrosoftLab/"]
RUN dotnet restore "DocsMicrosoftLab/DocsMicrosoftLab.csproj"
COPY . .
WORKDIR "/src/DocsMicrosoftLab"
RUN dotnet build "DocsMicrosoftLab.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DocsMicrosoftLab.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DocsMicrosoftLab.dll"]