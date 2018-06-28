# Build runtime image
FROM microsoft/aspnetcore:2.0
ENV ASPNETCORE_URLS=http://+:8080
RUN useradd --create-home -s /bin/bash svcwebuser
WORKDIR /app
USER svcwebuser
COPY publish/* ./
ENTRYPOINT ["dotnet", "CoreWebApiTest.dll"]
