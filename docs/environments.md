# Environments en ASP.NET Core {#environments-en-aspnet-core  data-source-line="248"}

Valores más comunes:

- `Development`
- `Staging`
- `Production`

Se leen desde:

- Variable de entorno `ASPNETCORE_ENVIRONMENT`
- `launchSettings.json`
- Docker / docker-compose

## Métodos de ayuda {#métodos-de-ayuda  data-source-line="262"}

- `env.IsDevelopment()`
- `env.IsStaging()`
- `env.IsProduction()`

``` {data-source-line="268"}

### 8.3. `docs/launchSettings.md`

```markdown
# launchSettings.json {#launchsettingsjson  data-source-line="273"}

Define perfiles de ejecución locales para:

- `dotnet run`
- Visual Studio / VS Code

Cada perfil puede tener:

- `applicationUrl`
- `launchBrowser`
- `environmentVariables` → `ASPNETCORE_ENVIRONMENT`