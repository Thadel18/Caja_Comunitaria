# App de la Caja de Ahorro y Crédito Omaguas "San Francisco"

Aplicación web instalable (PWA) para llevar el control de socios, aportes de
capital, ahorros, créditos, mora e interés — y generar los documentos
oficiales de la caja. **Funciona sin internet**: una vez abierta la primera
vez, sigue funcionando aunque no haya señal, y guarda todo en el propio
dispositivo (celular, tablet o computadora).

## Contenido de esta carpeta
- `index.html` – la aplicación completa (no necesita instalación de programas).
- `manifest.json` y `sw.js` – archivos que permiten "instalar" la app como un
  ícono en el celular/computadora y que funcione sin internet.
- `icon-192.png` / `icon-512.png` – ícono de la app.

## Uso más simple: abrir directamente
Puede simplemente abrir `index.html` haciendo doble clic. Funcionará, pero
para que se pueda "instalar" como app (ícono en pantalla de inicio) y
funcione offline de forma confiable, es mejor publicarla en internet una vez
(gratis) con una de las opciones de abajo. Luego de la primera visita, ya no
hace falta internet.

## ⚠️ Importante: por qué no se instalaba antes en Android
Android/Chrome **solo permite instalar una app si se abre desde una dirección
web segura (https://)**. Si usted abrió `index.html` haciendo doble clic
desde el explorador de archivos del celular (dirección que empieza con
`file://`), el botón de instalar nunca aparecerá — eso es una regla de
seguridad de Google, no un error de la app. La solución es publicar la
carpeta una vez en internet (gratis) con Netlify o GitHub Pages (ver abajo)
y abrir esa dirección `https://...` desde el celular. Ahora además, cuando
la app detecta que sí se puede instalar, muestra un aviso amarillo arriba
que dice **"Toca aquí para instalarla"**.

## Publicar gratis en internet (para instalar como app)

### Opción A — Netlify (más sencilla)
1. Entre a https://app.netlify.com/drop
2. Arrastre esta carpeta completa (o el .zip descomprimido) a la página.
3. Netlify le da un enlace tipo `https://algo-al-azar.netlify.app`.
4. Abra ese enlace desde el celular. Debería aparecer el aviso amarillo de
   instalación; si no aparece, use el menú del navegador (⋮) → **"Instalar
   app"** o **"Agregar a pantalla de inicio"**.

### Opción B — GitHub Pages
1. Cree una cuenta gratis en https://github.com si no tiene.
2. Cree un repositorio nuevo (por ejemplo `caja-osf`).
3. Suba todos los archivos de esta carpeta al repositorio.
4. Vaya a **Settings → Pages**, elija la rama `main` y guarde.
5. GitHub le da un enlace tipo `https://usuario.github.io/caja-osf/`.

Con cualquiera de las dos opciones, la conexión HTTPS es automática y
gratuita, lo que requieren los navegadores para instalar la app.

## Instalar la app en el celular
- **Android (Chrome):** abra el enlace `https://...` → toque el aviso
  amarillo "Toca aquí para instalarla", o use el menú (⋮) → "Instalar app" /
  "Agregar a pantalla de inicio".
- **iPhone (Safari):** abra el enlace → botón compartir (□↑) → "Agregar a
  pantalla de inicio" (iOS no tiene el aviso automático, siempre se instala
  por este menú).

Si después de publicarla en Netlify o GitHub Pages el aviso sigue sin
aparecer: cierre por completo el navegador y vuelva a abrir el enlace, o
pruebe primero en modo incógnito para descartar una copia vieja guardada en
caché.

## Ver los mismos datos en el celular y en la web (sincronización real)
Como la app guarda los datos dentro de cada navegador/celular, por defecto
**cada dispositivo tiene su propia copia** — por eso lo que ingresa en un
celular no aparecía en la web. La pestaña **"Google Sheets"** de la app
resuelve esto usando una hoja de cálculo de Google como "nube" compartida
entre sus 3 terminales (los celulares y la computadora). En resumen:
1. Cree una hoja de cálculo en Google Sheets.
2. Extensiones → Apps Script → pegue el código que la pestaña "Google
   Sheets" de la app le muestra (botón "Copiar código").
3. Implementar → Nueva implementación → tipo "Aplicación web" → acceso
   "Cualquier usuario" → Implementar.
4. Copie la URL que termina en `/exec`.
5. Péguela en la pestaña "Google Sheets" de **cada uno de los 3
   dispositivos** (misma URL en los tres) y presione "Guardar
   configuración".

Desde ahí, cada dispositivo tiene dos botones: **"📤 Subir"** (envía lo que
tiene ese dispositivo a la nube) y **"📥 Traer"** (descarga lo más reciente
de la nube a ese dispositivo). La app también revisa sola, cada vez que la
abre con internet, si hay algo más reciente en la nube, y se lo pregunta
antes de reemplazar sus datos locales. Sugerencia práctica: use un
dispositivo como "principal" para ingresar los datos del día, suba desde
ahí, y en los otros dos use "Traer" para ponerse al día — si dos personas
editan al mismo tiempo sin sincronizar entre medio, el que suba de último
sobrescribe al otro. Todo esto requiere internet solo en el momento de
sincronizar; el resto del tiempo la app sigue funcionando sin conexión con
normalidad.

Si ya había configurado una versión anterior de esta conexión, debe
reemplazar el código en Apps Script por el nuevo (la pestaña se lo indica)
y volver a implementarlo desde "Administrar implementaciones" para que la
misma URL empiece a funcionar en los dos sentidos.

## Cómo se guardan los datos
Todos los datos (socios, créditos, ahorros, etc.) se guardan **dentro del
navegador de cada dispositivo**, no en un servidor. Esto quiere decir:
- No necesita internet para trabajar día a día.
- Si varias personas usan la app en distintos celulares, cada uno tendrá su
  propia copia de los datos, salvo que se sincronicen manualmente (por
  respaldo .json) o mediante Google Sheets como se explicó arriba.

### Cómo compartir los datos entre dispositivos (Tesorero, Gerente, etc.)
Use la pestaña **"Respaldo de datos"** dentro de la app:
1. En el dispositivo con la información más reciente, presione
   **"Descargar respaldo (.json)"**.
2. Envíe ese archivo por WhatsApp, correo o USB al otro dispositivo.
3. En el otro dispositivo, entre a "Respaldo de datos" → "Restaurar desde
   archivo" y seleccione el archivo recibido.

Se recomienda hacer un respaldo después de cada Asamblea o jornada de
cobros, y guardarlo también en un correo electrónico o Drive como copia de
seguridad adicional.

## Sobre el diseño
La interfaz usa un lenguaje visual sencillo (íconos, colores de la selva y
el río, textos claros en español) pensado para ser intercultural y fácil de
usar por personas con distinto nivel de experiencia con la tecnología. El
modo de una sola página liviana (sin video ni imágenes pesadas) reduce el
consumo de datos y de batería, cuidando el uso responsable de los recursos.

## Parámetros ya cargados según el Reglamento
La configuración inicial de la app ya trae los valores aprobados el 1 de
marzo del 2026: aporte inicial US$60, aporte mensual US$1 hasta completar
US$100, tasa de interés 12% (socios) / 15% (no socios), mora de US$0,25
diarios, fondo de desgravamen de US$0,25 por mes de plazo, ahorro con tasa
del 3% anual, entre otros. Todos estos valores se pueden ajustar en la
pestaña **Configuración** si la Asamblea decide modificarlos.
