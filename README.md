# .NET Core Buildpack
This is a buildpack for Heroku. It fetches the latest version of .NET Core for Linux and runs the following commands on the code:
- `dotnet restore`
- `dotnet publish ${CSPROJ_FILE} --output ${BUILD_DIR} $DNU_FLAGS --configuration Release`

The `dotnet` binary will be made available to the slug afterwards (it should be used in your `Procfile`.)

Create a `.deployment` file in your repository's root with the following:
```
[config]
project = <project dir>
```

The buildpack will search that directory for `*.csproj` files and use that with `dotnet publish`

Sample compatible `Procfile`:
```
web: ASPNETCORE_URLS='http://+:$PORT' dotnet ./<app name>.dll --urls http://+:$PORT
```
