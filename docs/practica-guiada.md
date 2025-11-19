# Práctica guiada: Environments en ASP.NET Core {#práctica-guiada-environments-en-aspnet-core  data-source-line="603"}

## Pasos realizados {#pasos-realizados  data-source-line="605"}

1. Creación de repositorio en GitHub.
2. Clonado del repo en local.
3. Creación de estructura (`src`, `docs`).
4. Creación de la Web API `.NET` (template `webapi`).
5. Configuración de `appsettings.*.json` por entorno:
   - Development
   - Staging
   - Production
6. Edición de `launchSettings.json` para definir 3 perfiles.
7. Creación del endpoint `/env` para mostrar:
   - `EnvironmentFromHost`
   - `EnvironmentFromConfig`
8. Pruebas de ejecución con:
   - `dotnet run --launch-profile "Development"`
   - `dotnet run --launch-profile "Staging"`
   - `dotnet run --launch-profile "Production"`