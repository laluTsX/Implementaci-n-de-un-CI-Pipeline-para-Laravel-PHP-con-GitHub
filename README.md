# CI Pipeline para Laravel

## Objetivo
Automatizar la instalación de dependencias y la ejecución de pruebas de la aplicación Laravel mediante GitHub Actions.

## Tecnologías
- PHP 8.2
- Laravel 11
- Composer y PHPUnit
- Git y GitHub Actions

## Requisitos
- PHP compatible con el proyecto (8.2 o superior)
- Composer
- Git
- Acceso al repositorio de GitHub

## Instalación local
1. Clonar el repositorio
2. Ejecutar `composer install`
3. Copiar `.env.example` a `.env`
4. Ejecutar `php artisan key:generate`
5. Configurar la base de datos requerida (SQLite)
6. Ejecutar las migraciones con `php artisan migrate`
7. Ejecutar `php artisan test`

## Integración continua
El workflow `.github/workflows/ci.yml` se ejecuta al enviar cambios a la rama `main` o al crear una solicitud de integración dirigida a ella. Instala dependencias con Composer, prepara el entorno de Laravel y ejecuta las pruebas con SQLite en memoria.

## Pruebas
- `Tests\Unit\ExampleTest`: prueba de ejemplo de Laravel.
- `Tests\Feature\ExampleTest`: prueba de ejemplo de Laravel.
- `Tests\Feature\HomePageTest`: verifica que la ruta `/` responda con éxito.

Resultado esperado: 3 pruebas aprobadas (3 passed). Resultado obtenido: 3 pruebas aprobadas.

## Evidencias
- Ejecución exitosa (#1): https://github.com/laluTsX/Implementaci-n-de-un-CI-Pipeline-para-Laravel-PHP-con-GitHub/actions/runs/38982327196
- Ejecución fallida controlada (#2): https://github.com/laluTsX/Implementaci-n-de-un-CI-Pipeline-para-Laravel-PHP-con-GitHub/actions/runs/38983463029
- Ejecución exitosa tras la corrección (#3): https://github.com/laluTsX/Implementaci-n-de-un-CI-Pipeline-para-Laravel-PHP-con-GitHub/actions/runs/38983772750

## Conclusiones
Se cambió temporalmente la aserción de `HomePageTest` a `assertStatus(404)`. La prueba falló porque la página responde 200, y GitHub Actions marcó la ejecución como fallida (exit code 1). Al restaurar `assertSuccessful()` y subir el cambio, el pipeline volvió a aprobarse. La integración continua permite detectar errores de forma automática en cada cambio, antes de que lleguen a la rama principal.