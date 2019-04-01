#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime 
WORKDIR /WebApp
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /WebApp
COPY ["WebApp/WebApp.csproj", "WebApp/"]
RUN dotnet restore "WebApp/WebApp.csproj"
COPY . .
WORKDIR "/WebApp"
RUN dotnet build "WebApp.csproj" -c Release -o /WebApp

FROM build AS publish
RUN dotnet publish "WebApp.csproj" -c Release -o /WebApp

FROM base AS final
WORKDIR /WebApp
COPY --from=publish /WebApp .
ENTRYPOINT ["dotnet", "WebApp.dll"]