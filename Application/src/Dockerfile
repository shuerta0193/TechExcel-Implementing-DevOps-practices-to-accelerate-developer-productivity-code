FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out


# Use the official image as a parent image.
FROM mcr.microsoft.com/dotnet/aspnet:6.0

# Set the working directory.
WORKDIR /app

# Copy the rest of your app's source code from your host to your image filesystem.
COPY --from=build-env /app/out .

# Configure the main process to run when running the container
ENTRYPOINT ["dotnet", "RazorPagesTestSample.dll"]