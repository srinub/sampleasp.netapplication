#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1803 AS base
WORKDIR /webApplication
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-nanoserver-1803 AS build
WORKDIR /webApplication
COPY ["./webApplication/webApplication/webApplication.csproj", "webApplication/"]
RUN dotnet restore "./webApplication/webApplication.csproj"
COPY . .
WORKDIR "/webApplication/webApplication"
RUN dotnet build "./webApplication/webApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "./webApplication/webApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "webApplication.dll"]