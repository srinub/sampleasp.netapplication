#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:sdk AS build-env
WORKDIR /WebApp
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /WebApp
COPY ["/WebApp/WebApp/WebApp.csproj", "/WebApp/WebApp/"]
RUN dotnet restore "/WebApp/WebApp/WebApp.csproj"
COPY . .
WORKDIR "/WebApp/WebApp/"
RUN dotnet build "WebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApp.dll"]