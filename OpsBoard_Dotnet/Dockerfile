# Development Dockerfile for .NET 10
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS development

WORKDIR /src

# Copy solution file
COPY OpsBoard_Dotnet.sln ./

# Copy project files
COPY OpsBoard_Api/OpsBoard_Api.csproj ./OpsBoard_Api/
COPY OpsBoard_Application/OpsBoard_Application.csproj ./OpsBoard_Application/
COPY OpsBoard_Domain/OpsBoard_Domain.csproj ./OpsBoard_Domain/
COPY OpsBoard_Infrastructure/OpsBoard_Infrastructure.csproj ./OpsBoard_Infrastructure/

# Copy test project files
COPY tests/OpsBoard_Api.Tests/OpsBoard_Api.Tests.csproj ./tests/OpsBoard_Api.Tests/
COPY tests/OpsBoard_Application.Tests/OpsBoard_Application.Tests.csproj ./tests/OpsBoard_Application.Tests/
COPY tests/OpsBoard_Domain.Tests/OpsBoard_Domain.Tests.csproj ./tests/OpsBoard_Domain.Tests/
COPY tests/OpsBoard_Infrastructure.Tests/OpsBoard_Infrastructure.Tests.csproj ./tests/OpsBoard_Infrastructure.Tests/

# Restore dependencies
RUN dotnet restore

# Copy everything else
COPY . .

# Expose port
EXPOSE 5140

WORKDIR /src/OpsBoard_Api

# Run the application with restore
CMD ["dotnet", "watch", "run"]
