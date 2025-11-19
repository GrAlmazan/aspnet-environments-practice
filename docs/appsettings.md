# Uso de appsettings.*.json por entorno {#uso-de-appsettingsjson-por-entorno  data-source-line="225"}

ASP.NET Core carga la configuración así:

1. `appsettings.json` (base)
2. `appsettings.{Environment}.json` (ej: `appsettings.Development.json`)
3. Variables de entorno

Lo específico del entorno sobrescribe lo general.

## Secciones típicas {#secciones-típicas  data-source-line="235"}

- `Logging`
- `ConnectionStrings`
- Configuración custom, por ejemplo `CustomLogging`, `FeatureFlags`, etc.