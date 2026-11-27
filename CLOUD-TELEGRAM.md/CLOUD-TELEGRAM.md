# Sesiones temporales de Free Claude Code por Telegram

Este fork puede iniciar el bot nativo de FCC bajo demanda desde GitHub Actions. **No hay sondeo programado ni servicio permanente.** Cuando quieras usarlo, inicia manualmente el workflow **Temporary Telegram coding session** en la pestaña Actions y selecciona una duración de 10 a 300 minutos. El runner temporal se apaga al terminar; no necesitas PC ni VPS.

## Configuración única

1. Crea un bot con [@BotFather](https://t.me/BotFather) y usa el chat privado del bot.
2. Averigua tu ID numérico de Telegram, por ejemplo con [@userinfobot](https://t.me/userinfobot).
3. En este repositorio abre **Settings → Secrets and variables → Actions → New repository secret** y crea:
   - `TELEGRAM_BOT_TOKEN`: token de BotFather.
   - `ALLOWED_TELEGRAM_USER_ID`: tu ID numérico de Telegram.
   - `NVIDIA_NIM_API_KEY`: clave para el proveedor que usa el modelo configurado.
   No pegues estos valores en el código, issues, inputs del workflow ni en el chat.
4. Mantén los permisos del token de Actions en solo lectura. El workflow no conserva un token de escritura en el checkout, no hace commits y no publica cambios automáticamente.
5. En Actions selecciona **Temporary Telegram coding session → Run workflow**. Abre el chat privado y envía una tarea después de iniciar la ejecución. Detén la ejecución desde Actions si terminas antes del límite.

## Qué persiste y qué no

El checkout, las dependencias, la sesión de Claude y los cambios del árbol de trabajo viven solo en ese runner y desaparecen al terminar. Si hay cambios, el workflow intenta generar `session.patch` y guardarlo como artefacto por un día para que lo revises; no lo aplica ni lo sube por sí solo. Una cancelación o fallo puede perder trabajo que aún no se haya exportado.

El agente puede ejecutar comandos y cambiar archivos del checkout. FCC limita el directorio permitido a este repositorio, pero esto no es un sandbox contra código malicioso ni una garantía de confidencialidad. El bot y el proveedor reciben los mensajes necesarios para procesar la tarea. Los logs de FCC se suprimen en Actions, pero no envíes datos sensibles. Revisa todo parche antes de aplicarlo. Los límites de GitHub y del proveedor siguen aplicando; no hay garantía de que una sesión esté siempre disponible.

Si Actions está desactivado en este fork, tendrás que habilitarlo desde **Actions** después de revisar los workflows heredados y los cambios de este PR.
