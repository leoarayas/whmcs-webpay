# AGENTS.md

> Este archivo fue creado automáticamente por R:\_shared\sync-workflow.ps1.
> El contenido principal es el bloque de workflow Clevers al final.
> Enriquecelo con reglas específicas del proyecto arriba del bloque si necesitás.

<!-- BEGIN CLEVERS WORKFLOW v1 -->
# Flujo de trabajo Clevers — todos los proyectos R:\

> Fuente única de verdad sincronizada en cada `AGENTS.md` de los proyectos R:\
> por el script `R:\_shared\sync-workflow.ps1`. No editar manualmente en los
> proyectos; editar acá y volver a correr el script.

## Idioma y tono (cross-cutting)

- Responde en **español latinoamericano neutro**.
- Sin voseo rioplatense ni marcadores argentinos ("che", "vos", "re" como adverbio, "guita", "boludo", "dale" como confirmación vaga, "de una"). Sí es aceptable el español chileno natural cuando surge ("cachai", "po", "lucas").
- Conciso: respuestas <4 líneas salvo que pidan detalle.
- Sin emojis salvo pedido explícito.
- Profesional pero cercano, sin diminuciones innecesarias.
- Si el `AGENTS.md` de un proyecto define convenciones distintas, **prevalece el del proyecto**.

## 1. Skill discovery (inicio de sesión)

Antes de actuar en una tarea no trivial:

- Listá las skills disponibles con la herramienta `skill`.
- Activá las relevantes al dominio (`laravel-best-practices`, `livewire-development`, `fluxui-development`, `pest-testing`, `fortify-development`, `tailwindcss-development`, `laravel-permission-development`, `ai-sdk-development`, `cloudflare`, `echo-development`, etc.).
- Si el proyecto tiene skills propias en `.agents/skills/`, priorizá esas.

## 2. Todo discipline (multi-step)

- Tareas con **3+ pasos distintos** → usá `todowrite` para planificar antes de empezar.
- Marcá `in_progress` al arrancar, `completed` al cerrar cada paso.
- Si un paso se bloquea, dejalo `in_progress` y agregá un follow-up específico describiendo el blocker.

## 3. Subagent delegation

- **Búsquedas de archivos / patrones / estructura** → `task` con `subagent_type: "explore"`.
- **Tareas multi-paso complejas / investigación profunda** → `task` con `subagent_type: "general"`.
- **No dupliques trabajo**: si ya hay un subagent corriendo, esperá su resultado antes de relanzar.
- **No delegues trabajo trivial** que podés resolver directo en 1-2 llamadas.
- Subagents NO heredan el contexto de la conversación principal — pasales explícitamente lo que necesitan.

## 4. Read before edit

- **Nunca edites sin leer primero.** Antes de tocar un archivo, leelo completo (no solo las líneas que pensás cambiar).
- Si vas a modificar convención (naming, imports, estilo), leé 1-2 archivos hermanos para confirmar el patrón vigente.
- Si el archivo no existe todavía, leé la convención de la carpeta (sibling más cercano).

## 5. Convention matching

Antes de crear código nuevo, buscá archivos hermanos para inferir:

- Estructura de carpetas y naming (`kebab-case` vs `snake_case` vs `PascalCase`).
- Imports (orden, grupos, absolutos vs relativos).
- Patrones de testing.
- Formas de nombrar modelos, requests, controllers, jobs, etc.
- Si hay conflicto entre una regla global del playbook y una convención local del proyecto, **prevalece la local**.

## 6. TDD donde haya tests

Si el proyecto tiene suite de tests **y** vas a cambiar comportamiento observable:

1. Escribí un test que reproduzca el bug o defina el comportamiento nuevo.
2. Confirmá que falla (red) — si pasa al primer intento, el test no está probando nada.
3. Implementá el cambio mínimo para hacerlo pasar.
4. Confirmá que pasa (green).
5. Refactorizá si hace falta, con tests en verde todo el tiempo.

Si el proyecto **no** tiene tests o son exploratorios, no inventes tests nuevos — seguí las reglas del proyecto.

## 7. Verificación antes de "done"

Antes de marcar algo como completado, corré las verificaciones que apliquen:

| Stack | Comando |
|---|---|
| **PHP / Laravel** | `vendor/bin/pint --dirty --format agent` y `php artisan test --compact` (o subset relevante con `--filter`) |
| **JS/TS** | `npm run lint` (o equivalente) y `npm test` |
| **Rust** | `cargo fmt --all && cargo clippy -- -D warnings` y `cargo test` |
| **Astro / sitios estáticos** | `npm run build` + revisar página afectada en dev server |
| **Flutter / Dart** | `dart format .` + `dart analyze` + `flutter test` |

Si una verificación falla, **NO** reportes como hecho. Si la saltabas por buena razón, documentala explícitamente.

## 8. Lo que NO se hace (cross-cutting)

- No commitear sin pedido explícito del usuario.
- No pushear a `main` (ni a `master`) sin autorización explícita en la misma sesión.
- No commitear secretos, tokens, credenciales, archivos `.env`, dumps de DB, ni datos de clientes.
- No inventar APIs, paquetes, ni funciones que no existen — verificá primero en el código real.
- No instalar ni remover dependencias sin aprobación.
- No crear archivos de documentación (`.md`, `README`) salvo pedido explícito.
- No usar emojis salvo pedido explícito.
- No declarar "listo" sin haber corrido las verificaciones que apliquen.
- No saltarte el AGENTS.md del proyecto por seguir este playbook.
<!-- END CLEVERS WORKFLOW v1 -->
