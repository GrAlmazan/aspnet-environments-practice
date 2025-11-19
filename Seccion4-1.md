
﻿
# Práctica guiada: Environments en ASP.NET Core + appsettings + launchSettings + Git

> Objetivo: que al final de la práctica tengas un **repositorio completo** con:
> - Una **Web API .NET**.
> - Configuración por **entornos** (`Development`, `Staging`, `Production`).
> - **Perfiles** en `launchSettings.json`.
> - Documentación en **Markdown** explicando todo.

---

## 0. Requisitos previos

Asegúrate de tener instalado:

- **Git**
- **.NET SDK 8 (o 7 en su defecto)**  
- Una cuenta en **GitHub**  
- Editor de código (VS Code, Rider o Visual Studio)

Opcional (pero recomendable):

- **Postman** o **Thunder Client** (extensión de VS Code) para probar la API.

---

## 1. Crear el repositorio en GitHub

1. Entra a GitHub y crea un repo nuevo:

   - Nombre sugerido: `aspnet-environments-practice`
   - Visibilidad: `Private` o `Public` (como prefieras)
   - No marques nada aún (ni README ni .gitignore) para practicar todo local.

2. Copia la URL del repo, por ejemplo:

   ```text
   https://github.com/tu-usuario/aspnet-environments-practice.git
----------

## 2. Clonar el repositorio en tu máquina

En una terminal:

```bash
cd ruta/donde/quieres/trabajar
git clone https://github.com/tu-usuario/aspnet-environments-practice.git
cd aspnet-environments-practice

```

Verifica que estás dentro de la carpeta del repo:

```bash
pwd        # Linux/Mac
cd         # Windows (o revisa en Explorer)

```

----------

## 3. Crear la estructura base del proyecto

Dentro del repo, crea estas carpetas:

```bash
mkdir src
mkdir docs

```

La idea:

-   `src` → Código fuente de la API.
    
-   `docs` → Documentación Markdown.
    

----------

## 4. Crear el README inicial

Crea el archivo en la raíz:

```bash
code README.md
# o usa tu editor preferido

```

Contenido sugerido:

```markdown
# Práctica: ASP.NET Core Environments + appsettings + launchSettings

## Objetivo

Practicar el uso de:
- Entornos (`Development`, `Staging`, `Production`)
- Archivos `appsettings.*.json`
- `launchSettings.json`
- Configuración condicional en `Program.cs`

## Estructura del repo

- `src/` → Código fuente de la API.
- `docs/` → Documentación técnica en Markdown.

## Tecnologías

- .NET 8 Web API
- ASP.NET Core Environments
- Git / GitHub

```

Guarda el archivo.

----------

## 5. Primer commit (documentación inicial)

Agrega y haz commit:

```bash
git status
git add README.md
git commit -m "chore: add initial README for environments practice"
git push origin main

```

----------

## 6. Crear la Web API con .NET (Minimal API)

Dentro de la carpeta `src`:

```bash
cd src
dotnet new webapi -n Demo.Environments.Api

```

Esto creará:

-   `src/Demo.Environments.Api/`
    
    -   `Program.cs`
        
    -   `appsettings.json`
        
    -   `appsettings.Development.json`
        
    -   `Properties/launchSettings.json`
        
    -   etc.
        

Entra al proyecto:

```bash
cd Demo.Environments.Api

```

Prueba que compila:

```bash
dotnet build

```

----------

## 7. Probar la API en Development (por defecto)

Desde `src/Demo.Environments.Api`:

```bash
dotnet run

```

Verás algo como:

```text
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: https://localhost:7xxx
      Now listening on: http://localhost:5xxx

```

Abre el navegador en la URL HTTPS que te dio y prueba el endpoint `/weatherforecast` o el que venga por defecto.

Detén la ejecución con `Ctrl + C`.

----------

## 8. Crear documentación técnica en `docs`

Regresa a la raíz del repo:

```bash
cd ../../   # desde src/Demo.Environments.Api -> src -> raiz

```

Crea los archivos:

```bash
cd docs
code appsettings.md
code environments.md
code launchSettings.md

```

### 8.1. `docs/appsettings.md` (resumen de configuración)

Ejemplo:

```markdown
# Uso de appsettings.*.json por entorno

ASP.NET Core carga la configuración así:

1. `appsettings.json` (base)
2. `appsettings.{Environment}.json` (ej: `appsettings.Development.json`)
3. Variables de entorno

Lo específico del entorno sobrescribe lo general.

## Secciones típicas

- `Logging`
- `ConnectionStrings`
- Configuración custom, por ejemplo `CustomLogging`, `FeatureFlags`, etc.

```

_(Puedes complementar con lo que tú ya tengas documentado.)_

### 8.2. `docs/environments.md`

```markdown
# Environments en ASP.NET Core

Valores más comunes:

- `Development`
- `Staging`
- `Production`

Se leen desde:

- Variable de entorno `ASPNETCORE_ENVIRONMENT`
- `launchSettings.json`
- Docker / docker-compose

## Métodos de ayuda

- `env.IsDevelopment()`
- `env.IsStaging()`
- `env.IsProduction()`

```

### 8.3. `docs/launchSettings.md`

```markdown
# launchSettings.json

Define perfiles de ejecución locales para:

- `dotnet run`
- Visual Studio / VS Code

Cada perfil puede tener:

- `applicationUrl`
- `launchBrowser`
- `environmentVariables` → `ASPNETCORE_ENVIRONMENT`

```

Guarda todo.

----------

## 9. Commit de código + docs

Desde la raíz del repo:

```bash
cd ..
git status
git add src/Demo.Environments.Api docs
git commit -m "feat: add Demo.Environments.Api and environments documentation"
git push origin main

```

----------

## 10. Explorar y entender `appsettings.json` del proyecto

Ve a:

```bash
cd src/Demo.Environments.Api
code appsettings.json

```

Identifica:

-   Sección `Logging`
    
-   Puede haber `AllowedHosts`
    
-   Tal vez `ConnectionStrings` si el template lo trae
    

Observa también `appsettings.Development.json`.

----------

## 11. Crear `appsettings.Staging.json` y `appsettings.Production.json`

Si no existen, créalos a partir del base.

### 11.1. Crear archivos

```bash
code appsettings.Staging.json
code appsettings.Production.json

```

### 11.2. Ejemplo de contenido (muy simple)

`appsettings.Development.json`:

```json
{
  "EnvironmentName": "Development",
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "Microsoft.AspNetCore": "Information"
    }
  }
}

```

`appsettings.Staging.json`:

```json
{
  "EnvironmentName": "Staging",
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  }
}

```

`appsettings.Production.json`:

```json
{
  "EnvironmentName": "Production",
  "Logging": {
    "LogLevel": {
      "Default": "Warning",
      "Microsoft.AspNetCore": "Warning"
    }
  }
}

```

> Nota: `EnvironmentName` es solo para que tú lo leas luego desde la API y veas qué archivo se cargó.

----------

## 12. Modificar `Program.cs` para exponer un endpoint `/env`

Abre `Program.cs`:

```bash
code Program.cs

```

Añade algo como esto (en .NET 8 Minimal API):

```csharp
var builder = WebApplication.CreateBuilder(args);

var env = builder.Environment;
var configuration = builder.Configuration;

// Servicios
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Swagger según entorno (Dev/Staging)
if (app.Environment.IsDevelopment() || app.Environment.IsStaging())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

// Endpoint para ver entorno y configuración
app.MapGet("/env", () =>
{
    var currentEnv = app.Environment.EnvironmentName;
    var envNameFromConfig = configuration["EnvironmentName"];

    return Results.Ok(new
    {
        EnvironmentFromHost = currentEnv,
        EnvironmentFromConfig = envNameFromConfig,
        Message = $"Hola, estás en el entorno: {currentEnv}"
    });
});

app.Run();

```

Guarda.

----------

## 13. Configurar `launchSettings.json` con 3 perfiles

Abre:

```bash
code Properties/launchSettings.json

```

Edita la sección `profiles` para que quede algo así:

```jsonc
"profiles": {
  "Development": {
    "commandName": "Project",
    "dotnetRunMessages": true,
    "launchBrowser": true,
    "launchUrl": "env",
    "applicationUrl": "https://localhost:7205;http://localhost:5063",
    "environmentVariables": {
      "ASPNETCORE_ENVIRONMENT": "Development"
    }
  },
  "Staging": {
    "commandName": "Project",
    "dotnetRunMessages": true,
    "launchBrowser": true,
    "launchUrl": "env",
    "applicationUrl": "https://localhost:7206;http://localhost:5064",
    "environmentVariables": {
      "ASPNETCORE_ENVIRONMENT": "Staging"
    }
  },
  "Production": {
    "commandName": "Project",
    "dotnetRunMessages": true,
    "launchBrowser": true,
    "launchUrl": "env",
    "applicationUrl": "https://localhost:7207;http://localhost:5065",
    "environmentVariables": {
      "ASPNETCORE_ENVIRONMENT": "Production"
    }
  }
}

```

Puntos clave:

-   Cada perfil tiene su propio puerto.
    
-   Cambiamos `launchUrl` a `"env"` para que abra directamente el endpoint que creamos.
    

----------

## 14. Probar la API con cada perfil desde CLI

### 14.1. Development

```bash
dotnet run --launch-profile "Development"

```

Abre el navegador en la URL que indique, por ejemplo:

```text
https://localhost:7205/env

```

Deberías ver un json similar a:

```json
{
  "environmentFromHost": "Development",
  "environmentFromConfig": "Development",
  "message": "Hola, estás en el entorno: Development"
}

```

Detén con `Ctrl + C`.

### 14.2. Staging

```bash
dotnet run --launch-profile "Staging"

```

Ve a:

```text
https://localhost:7206/env

```

Debes ver:

```json
{
  "environmentFromHost": "Staging",
  "environmentFromConfig": "Staging",
  "message": "Hola, estás en el entorno: Staging"
}

```

### 14.3. Production

```bash
dotnet run --launch-profile "Production"

```

Ve a:

```text
https://localhost:7207/env

```

Resultado esperado:

```json
{
  "environmentFromHost": "Production",
  "environmentFromConfig": "Production",
  "message": "Hola, estás en el entorno: Production"
}

```

> Con esto confirmas que:
> 
> -   Cambia el entorno según el perfil.
>     
> -   Se está leyendo el `appsettings.{Environment}.json` correcto.
>     

----------

## 15. Documentar esta práctica en un Markdown extra

En `docs`, crea:

```bash
cd ../../../   # asegúrate de estar en la raíz del repo
cd docs
code practica-guiada.md

```

Contenido sugerido (resumen de lo que hiciste):

```markdown
# Práctica guiada: Environments en ASP.NET Core

## Pasos realizados

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

```

Guarda.

----------

## 16. Commit final de la práctica

Desde la raíz del repo:

```bash
git status
git add .
git commit -m "feat: complete environments practice with profiles and /env endpoint"
git push origin main

```

----------

## 17. Retos opcionales (para subir de nivel)

Si quieres extender la práctica aún más, puedes agregar:

### 17.1. Integrar Serilog + Seq por entorno

-   Crear sección `CustomLogging` en tus `appsettings.*.json`.
    
-   Ajustar `LogEventLevel` según el entorno.
    
-   En `Program.cs` integrar `Serilog` usando:
    
    ```csharp
    Log.Logger = new LoggerConfiguration()
        .ReadFrom.Configuration(builder.Configuration)
        .CreateLogger();
    
    builder.Host.UseSerilog();
    
    ```
    

### 17.2. Simular una ConnectionString distinta

-   Agregar `ConnectionStrings:DefaultConnection` en cada `appsettings.*.json`.
    
-   Exponer un endpoint `/connection-info` que devuelva la cadena actual (o solo el nombre de la BD) para ver que cambia por entorno.
    

### 17.3. Añadir Docker

-   Crear un `Dockerfile` simple para la API.
    
-   Usar variable de entorno `ASPNETCORE_ENVIRONMENT` en `docker run`:
    
    ```bash
    docker run -e ASPNETCORE_ENVIRONMENT=Staging ...
    
    ```
    

----------

## 18. Qué aprendiste con esta práctica

-   Crear un repo y estructurarlo con `src` y `docs`.
    
-   Crear una Web API con .NET y correrla localmente.
    
-   Configurar archivos `appsettings.*.json` por entorno.
    
-   Configurar perfiles en `launchSettings.json`.
    
-   Cambiar comportamiento según `ASPNETCORE_ENVIRONMENT`.
    
-   Usar un endpoint sencillo (`/env`) como “panel de diagnóstico” del entorno actual.
    

----------

Práctica guiada — Sesión 4 - 1.md
Usuarios externos
Mostrando Práctica guiada — Sesión 4 - 1.md