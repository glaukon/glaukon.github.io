# Publicación del blog

## Calendario propuesto: octubre de 2026

Un artículo cada martes. Las fechas ya están en los archivos y se pueden cambiar antes de subirlos.

| Fecha | Artículo | Archivo en `_posts` |
| --- | --- | --- |
| 6 de octubre | Copias de seguridad: la diferencia entre creer que estás protegido y poder recuperar tus datos | `2026-10-06-copias-seguridad-recuperar-datos.md` |
| 13 de octubre | Automatizar no es complicar: pequeñas tareas que una pyme puede dejar de hacer a mano | `2026-10-13-automatizar-tareas-pyme.md` |
| 20 de octubre | Por qué el software libre sigue teniendo sentido para profesionales y pequeñas empresas | `2026-10-20-software-libre-profesionales-pymes.md` |
| 27 de octubre | Qué debe tener una aplicación interna sencilla para que el equipo la use de verdad | `2026-10-27-aplicacion-interna-sencilla.md` |

El artículo de mayo sobre sistemas y desarrollo sigue siendo un borrador (`published: false`).

Los cuatro artículos de octubre incluyen portadas generadas con IA en `images/octubre-2026/`, con sus campos `image` e `image_alt`. Incluye también esta carpeta al crear el commit y subir los cambios.

## Activación inicial en GitHub

1. Revisa los cuatro artículos y sus fechas en tu editor.
2. En GitHub Desktop, selecciona los archivos de estos cambios, crea un commit y pulsa **Push origin** para subirlos a `master`. Incluye `_config.yml`, los cuatro artículos, esta guía, el plan editorial y `.github/workflows/publicar-blog.yml`.
3. En el repositorio de GitHub, comprueba en **Settings → General → Default branch** que la rama predeterminada sea `master`. El calendario de Actions solo se ejecuta desde la rama predeterminada. Si se cambia de rama, hay que actualizar también `branches` y la condición `if` del workflow.
4. En **Settings → Pages → Build and deployment → Source**, selecciona **GitHub Actions**. Ya tienes un workflow; no necesitas crear otro desde las sugerencias de GitHub.
5. Abre **Actions → Publicar blog → Run workflow**, elige `master` y ejecútalo. Si Actions está desactivado, actívalo primero en la configuración del repositorio.
6. Comprueba que los trabajos `build` y `deploy` terminan en verde y visita la URL del despliegue. Antes del 6 de octubre, los artículos nuevos no deben aparecer. La primera ejecución tras subir los archivos puede fallar si todavía no has cambiado el origen de Pages; vuelve a ejecutarla después del paso 4.

Estos cambios quedan preparados localmente: no activan el calendario hasta que los subas y configures Pages. No hace falta mantener encendido el ordenador ni añadir un token personal.

## Cómo funciona

Jekyll tiene `future: false` y la zona `Europe/Madrid`. Cada artículo tiene `published: true` y una fecha futura a las 09:00, con el desplazamiento horario correspondiente. Estar marcado como publicable no hace que aparezca antes de esa fecha.

El workflow reconstruye y publica el sitio todos los días a las **08:17 UTC**: 10:17 en Madrid durante el horario de verano y 09:17 durante el horario de invierno. En las fechas propuestas, las ejecuciones quedan después de las 09:00 del artículo, incluido el 27 de octubre, tras el cambio de hora. La publicación se verá cuando termine el despliegue. GitHub puede retrasar u omitir ejecuciones programadas; no es una garantía de publicación al minuto. La siguiente ejecución diaria volverá a intentarlo.

También se reconstruye al subir cambios a `master` o al ejecutar el workflow manualmente. Si haces esto después de las 09:00 del día indicado, el artículo puede aparecer antes de la ejecución diaria. Poner una fecha futura por sí solo no reconstruye una web estática: por eso está el workflow.

En repositorios públicos, GitHub puede desactivar los workflows programados tras 60 días sin actividad. Si ocurre, reactívalo en Actions y ejecuta **Run workflow**. Si no aparece un artículo, comprueba primero el estado de Actions, su fecha y `published`.

## Cambiar una fecha o añadir artículos

En el encabezado del archivo encontrarás, por ejemplo:

```yaml
date: 2026-10-06 09:00:00 +0200
published: true
```

Para cambiar el día, modifica `date` y renombra el archivo con la misma fecha: `AAAA-MM-DD-titulo.md`. En Madrid, los tres primeros artículos de octubre usan `+0200` y el del 27 usa `+0100`. Ajusta el desplazamiento si eliges otra época del año. El valor `date` del encabezado prevalece sobre el nombre del archivo.

Para aplazar un artículo sin elegir fecha todavía, cambia a `published: false`. Para recuperarlo, pon una fecha futura y vuelve a `true`. Guarda, crea un commit y sube los cambios. No hace falta modificar el cron para cambiar los días de publicación; su comprobación es diaria. Si eliges una hora posterior a la ejecución diaria, tendrás que ajustar el workflow o esperar a la ejecución del día siguiente.

Los archivos de un repositorio público se pueden leer en GitHub antes de publicarse en el blog.

## Referencias

- [Configuración de Jekyll: fechas futuras y zona horaria](https://jekyllrb.com/docs/configuration/options/).
- [Configurar el origen de GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
- [Workflows de GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).
- [Ejecuciones programadas de GitHub Actions](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule).


## Prompts de las portadas

Generadas con la herramienta integrada de generación de imágenes. Cada prompt combina el prefijo, su escena y el sufijo siguientes.

Prefijo:

```text
Use case: photorealistic-natural. Asset type: editorial cover photograph for a Spanish technology blog, one image only. Landscape 16:9 composition.
```

Escena de `images/octubre-2026/copias-seguridad.png`:

```text
A realistic small business desk with an open laptop showing simple folder icons and a successful restore check symbol without text, a connected external backup drive and a second disconnected drive neatly nearby. Visual emphasis on recoverable data and tangible backup equipment.
```

Escena de `images/octubre-2026/automatizacion.png`:

```text
A realistic small business desk with an open laptop showing an elegant minimal workflow of three connected rectangular task cards and check marks without any text, with a neatly arranged small stack of paperwork beside it. Visual emphasis on turning repeated paperwork into a simple digital process.
```

Escena de `images/octubre-2026/software-libre.png`:

```text
A realistic small business desk with two different unbranded laptops side by side showing matching abstract document and spreadsheet interfaces without any letters or numbers, and a notebook. Visual emphasis on interoperability, freedom to choose tools and practical collaboration.
```

Escena de `images/octubre-2026/aplicacion-interna.png`:

```text
A realistic small business desk with an open laptop and a smartphone next to it, both displaying the same elegant minimal task board with three columns and a few colored cards, no words or numbers. Visual emphasis on a simple usable internal application across devices.
```

Sufijo común:

```text
Consistent series art direction: authentic modest modern office, light oak tabletop, soft natural window daylight, restrained neutral tones, realistic materials, clean uncluttered composition, three-quarter view, main objects centered with generous crop-safe margins. Professional editorial photography, credible everyday technology, no people, no brand logos, no watermark, no captions, no readable text, no sci-fi holograms.
```
