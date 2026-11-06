# Encuesta de disponibilidad del claustro (23–27 de noviembre)

Página estática para GitHub Pages. Cada docente escribe su nombre y apellidos, marca las medias horas en las que puede y pulsa **Enviar**. No ve las respuestas de los demás. Las respuestas llegan a una hoja de Google tuya, con una pestaña **Resumen** que cuenta cuántos pueden en cada franja (mapa de calor) y lista las mejores franjas con los nombres.

Archivos:

- `index.html` — la encuesta (se sube a GitHub).
- `Code.gs` — el script que recibe las respuestas (se pega en Google Apps Script, dentro de la hoja).

## 1. Crear la hoja de respuestas (5 minutos)

1. Entra en [sheets.google.com](https://sheets.google.com) con tu cuenta de thePower y crea una hoja nueva. Ponle nombre, por ejemplo «Disponibilidad claustro nov 2026».
2. Menú **Extensiones → Apps Script**. Se abre el editor con un archivo `Código.gs`.
3. Borra lo que haya y pega el contenido completo de `Code.gs`. Guarda (icono del disquete o Ctrl+S).
4. En el desplegable de funciones (arriba, junto a «Depurar») elige **setup** y pulsa **▶ Ejecutar**. La primera vez pide permisos: «Revisar permisos» → tu cuenta → «Avanzado» → «Ir a … (no seguro)» → «Permitir». Es tu propio script leyendo tu propia hoja; el aviso es el estándar de Google para scripts no publicados.
5. Vuelve a la hoja: ya tiene las pestañas **Resumen** y **Respuestas**.

## 2. Publicar el script como aplicación web

1. En el editor de Apps Script: **Implementar → Nueva implementación**.
2. Pulsa el engranaje junto a «Seleccionar tipo» y elige **Aplicación web**.
3. Rellena:
   - Descripción: `encuesta claustro`
   - Ejecutar como: **Yo** (tu cuenta)
   - Quién tiene acceso: **Cualquier usuario**
4. **Implementar**. Copia la **URL de la aplicación web** (acaba en `/exec`).
5. Comprueba que funciona: pega esa URL en el navegador. Debe mostrar `{"ok":true,"respuestas":0}`.

«Cualquier usuario» significa que la página puede enviar respuestas sin que el docente inicie sesión. Nadie puede leer la hoja con esa URL: solo escribir una respuesta.

## 3. Conectar la página y subirla a GitHub

1. Abre `index.html` con un editor de texto y busca la línea:

   ```js
   const ENDPOINT = "";
   ```

   Pega la URL entre las comillas y guarda.

2. En [github.com](https://github.com) crea un repositorio nuevo (por ejemplo `encuesta-claustro`), público. Sube `index.html` (botón **Add file → Upload files**).
3. En el repositorio: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. Al cabo de un minuto aparece la dirección, del tipo `https://TU-USUARIO.github.io/encuesta-claustro/`. Ese es el enlace que envías al claustro.

## 4. Ver los resultados

Abre la hoja de Google. En **Resumen**:

- la cuadrícula muestra cuántos docentes pueden en cada media hora, con color más intenso cuanta más gente;
- a la derecha, **Mejores franjas** lista las 15 franjas con más gente y quiénes son;
- arriba, el número de respuestas recibidas y la hora de la última.

En **Respuestas** está cada persona en una fila. Si alguien vuelve a enviar con el mismo nombre y apellidos, se sustituye su fila (no se duplica).

## Si quieres cambiar algo

- **Horario** (ahora de 8:00 a 21:00): cambia `START` y `END` en los dos archivos (`index.html` y `Code.gs`) y vuelve a ejecutar `setup()`. Ojo: `setup()` vacía la pestaña Resumen pero no borra Respuestas; si cambias el horario con respuestas ya recibidas, las columnas dejarán de coincidir, así que hazlo antes de enviar el enlace.
- **Días**: igual, en la lista `DAYS` de ambos archivos.
- Si editas `Code.gs` después de publicarlo, hay que hacer **Implementar → Gestionar implementaciones → ✎ → Versión: Nueva → Implementar** para que el cambio llegue a la URL.
