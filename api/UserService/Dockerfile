# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /app

# Copy the project file and restore dependencies
COPY UserService.csproj .
RUN dotnet restore

# Copy the rest of the application code and build the app
COPY . .
RUN dotnet publish -c Release -o /publish

# Stage 2: Run the application
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app

# Copy the published app from the build stage
COPY --from=build /publish .

# Expose the port for the API
EXPOSE 80

# Set the entry point for the container
ENTRYPOINT ["dotnet", "UserService.dll"]
