[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md) [![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)

# Cómo personalizar tu README de perfil de GitHub (con mi perfil como ejemplo)


Este tutorial te enseña a armar el README de tu perfil de GitHub: el repo especial que lo activa, los badges, las tarjetas automáticas de estadísticas, la serpiente con GitHub Actions, y los errores que dejan perfiles rotos. Todo está probado en mi propio perfil, que uso como ejemplo a lo largo del tutorial.

## Cómo crear tu README y que se muestre en tu perfil

GitHub muestra un README en tu perfil cuando cumples tres cosas:

1. El repositorio es **público**.
2. El nombre del repo es exactamente tu nombre de usuario (`Jesus-Valverde`, en mi caso).
3. El repo tiene un `README.md` con contenido, en la raíz.

Si falta cualquiera de las tres, tu perfil queda en blanco. Para crearlo: botón `+` → **New repository**, nombre igual a tu usuario, marca **Public**, activa **Add a README** y crea. GitHub detecta el repo especial y te muestra el botón **Edit README** en tu perfil.

Tres casos especiales: las cuentas administradas por una empresa (Enterprise Managed Users) no pueden tener perfil personalizado; los repos con tu nombre creados antes de julio de 2020 no se muestran solos (presiona **Share to profile** dentro del repo); y los logros (achievements) siguen existiendo a octubre de 2026 pero con documentación caída y dos insignias retiradas — trátalos como adorno, no como meta.

## Mi perfil como ejemplo

Este tutorial nació de un pendiente real: mi perfil tenía una sección "👉 Tutorials" con un GIF de "loading..." y la admisión de que estaba sin terminar. La llené escribiendo justamente este documento, y su anatomía sirve de caso de estudio.

Mi `README.md` original pesa 3,369 bytes: saludo, la sección Tutorials (el placeholder), quién soy con la bandera de México, estudios, 11 badges de tecnologías, 3 botones de práctica (freeCodeCamp, Exercism, HackerRank), 3 de contacto (LinkedIn, Linktree, correo) y una tarjeta de Steam. Son 17 badges en total, todos de shields.io con el estilo `for-the-badge`. Hacía bien sin proponérselo: `alt` en todas las imágenes y encabezados `##` correctos, justo lo que pide la guía de accesibilidad de GitHub.

Lo que le faltaba: tarjetas de estadísticas, racha y la serpiente — lo que el resto del tutorial construye. Y dos fragilidades para que no caigas en ellas: la tarjeta de Steam la sirve un servicio comunitario (`card.yuy1n.io`) sin respaldo (si cierra, se rompe el bloque más grande del perfil), y el botón de correo expone mi Gmail a los recolectores de spam. Los candados van más abajo.

## Badges con shields.io

Un badge es una imagen que shields.io genera a partir de su URL. El formato base es `img.shields.io/badge/ETIQUETA-MENSAJE-COLOR`, y el control está en los parámetros: `style` elige el estilo (`flat` por defecto; también `flat-square`, `plastic`, `for-the-badge`, `social`), `logo` toma cualquier ícono del catálogo simple-icons, y los colores aceptan hex.

Tres reglas de escape causan el 90% de los badges rotos: un guion literal es `--`, un guion bajo literal es `__`, y el `#` de los colores hex va como `%23` (un hex sin `#` también funciona). El patrón real de mi README:

```markdown
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
```

Para que sea clicleable, no uses `link=` (no funciona dentro de `<img>`): envuelve la imagen en un enlace normal.

```markdown
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/tu-usuario/)
```

Sobre límites: shields.io no publica cifras de cuota; los cuellos de botella reales suelen estar en el servicio externo que el badge consulta.

## Íconos sin texto con skill-icons

Una alternativa compacta a las filas de badges: una sola URL que dibuja la cuadrícula completa.

```markdown
[![My Skills](https://skillicons.dev/icons?i=js,html,css,react,py,flask&theme=dark)](https://skillicons.dev)
```

Los ids van en minúsculas, el tema por defecto es `dark` y `perline` controla los íconos por línea (1 a 50). La desventaja: sin texto al lado, un muro de logos comunica menos — los badges con nombre ganan en portafolios; los íconos, en listas largas. Y si te falta un ícono: skillicons.dev no tiene todos (React Router y JWT devuelven cuadros vacíos), pero `skills.syvixor.com` tiene más de 1,059 — incluidos `reactrouter` y `jwt` — y cambia de tema claro/oscuro según el visitante. Es la que uso hoy: mis 11 badges caben en una línea.

## README en dos idiomas

Pon una fila de badges de idioma arriba del README, cada uno con enlace a su versión:

```markdown
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md)
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)
```

La convención es el sufijo de idioma: `README.md` como principal y `README.es.md` en español, ambos con la misma fila de badges. Ojo: GitHub solo renderiza `README.md` en la página de perfil (no ejecuta JavaScript, no hay selector "en el sitio") — el badge lleva al repo, donde la otra versión sí se lee completa.

## El formato nativo de GitHub

Antes de instalar nada, aprovecha lo que GitHub ya soporta: secciones colapsables, llamadas de atención, notas al pie y una etiqueta para imagen según tema. Sin servicios externos, sin tokens, sin mantenimiento.

```html
<details>
<summary>Mi trayectoria en detalle</summary>

Aquí va el contenido. Debe haber una línea en blanco después de `<summary>`
para que el Markdown interno se renderice.

</details>
```

Las llamadas de atención (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`) van en un blockquote. La documentación pide máximo una o dos por documento, solo para información crucial — y solo renderizan en github.com; en otros visores quedan como blockquote plano.

El formato nativo más subestimado: la imagen que cambia según el tema del visitante.

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="banner-dark.svg">
  <img alt="Banner de bienvenida" src="banner-light.svg">
</picture>
```

## Banners y efectos animados (con moderación)

Para un encabezado con presencia: capsule-render (banners SVG animados) y readme-typing-svg (texto que se escribe y se borra).

```markdown
![header](https://capsule-render.vercel.app/api?type=wave&color=gradient&height=200&section=header&text=Tu%20Nombre&fontSize=42&animation=fadeIn)

![typing](https://readme-typing-svg.demolab.com/?font=Fira+Code&size=22&pause=1000&multiline=true&width=600&height=80&lines=Desarrollador+web;Aprendiendo+Flask+y+React)
```

`multiline=true` apila frases separadas por punto y coma. Antes de llenar tu perfil de efectos, el costo: cada uno es una dependencia externa más, los GIFs pesan megabytes, ninguno respeta la preferencia de movimiento reducido, y banner + texto + GIF + badges juntos dan el perfil saturado que la comunidad señala como mal ejemplo. Mi regla, sacada de mi propio perfil: el GIF de "loading..." funcionaba porque era uno y contaba una historia; dos más ya son ruido.

## Tarjetas de estadísticas

Servicios comunitarios que convierten tu actividad de GitHub en tarjetas de imagen:

```markdown
![Mis stats de GitHub](https://github-readme-stats.vercel.app/api?username=Jesus-Valverde&show_icons=true&theme=tokyonight)

![GitHub Streak](https://streak-stats.demolab.com?user=Jesus-Valverde&theme=tokyonight)

![Trophy](https://github-profile-trophy.vercel.app/?username=Jesus-Valverde)
```

Y una cuarta que se suele olvidar y es la única verdaderamente automática: la de lenguajes más usados. GitHub la calcula de tus repos reales — la fila de badges cuenta lo que tú dices que sabes; esta cuenta lo que tu código dice que haces:

```markdown
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Jesus-Valverde&layout=compact&theme=tokyonight&langs_count=8)
```

Parámetros útiles: `include_all_commits=true` (commits de toda la vida, no solo del año), `hide_border=true`, `layout=compact` y `langs_count` en la de lenguajes, y `cache_seconds` en stats (mínimo 6 horas, máximo 24). Si pones dos tarjetas lado a lado (`width` porcentual, se apilan solas en móvil), anclalas con `align="top"`: GitHub alinea las imágenes por su línea de texto y la más corta queda flotando abajo. Y para que midan lo mismo, compensa con el reparto del ancho — mi stats mide 467×195 píxeles y mi racha 495×195; con `width="48%"` y `width="51%"` quedan empatadas a cualquier tamaño de ventana.

Antes de instalar nada, el problema: las instancias hospedadas comparten la cuota anónima de la API de GitHub y fallan a ratos. La solución recomendada por el propio equipo es desplegar tu instancia en Vercel (~15 minutos): fork del repo, conectar a Vercel, y en sus variables de entorno agregar `PAT_1` con un Personal Access Token (la llave que GitHub usa para autorizar programas) clásico sin permisos marcados. Después cambias la URL de la tarjeta a tu instancia. La de racha documenta el mismo proceso; la de trofeos sigue arriba tal cual.

## Otros widgets

Un segundo círculo de widgets populares. Lo que decide su robustez es quién sirve la imagen:

| Widget | ¿Quién sirve la imagen? | Si el tercero falla |
|---|---|---|
| Contador de vistas (komarev) | Su servidor, en cada visita | Badge roto o desactualizado |
| Activity graph (ashutosh00710) | Su Vercel, en cada visita | Imagen rota (mismo riesgo que stats) |
| Summary cards (vn7n24fzkq) | Una Action **guarda los SVG en tu repo** | Nada: la imagen ya es tuya |
| 3D contributions (yoshi389111) | Una Action guarda el SVG en tu repo | Nada: mismo patrón |
| WakaTime (tiempo de código) | Su API + Action diaria | Sección vacía o con error |

El patrón más robusto es el "committed": la imagen vive en `raw.githubusercontent.com` — en GitHub, no en un servidor ajeno que puede fallar a las 3 a.m. Dos avisos: el contador de vistas es aproximado (su mantenedor lo llama "tracking pixel" y ha dejado de mostrarse bajo carga), y WakaTime exige activar "Display activity publicly" y se actualiza una vez al día.

## La serpiente con GitHub Actions

La serpiente que se come tu cuadrícula de contribuciones (Platane/snk) se genera en tu propio repo y se guarda en un branch llamado `output` — después no depende de nadie. Crea `.github/workflows/snake.yml`:

```yaml
name: Generate Snake
on:
  schedule:
    - cron: "0 0 * * *"   # diario a medianoche UTC
  workflow_dispatch:        # botón manual para probar
permissions:
  contents: write
jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk/svg-only@v3
        with:
          github_user_name: Jesus-Valverde
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Y la embebes desde el raw del branch `output` (con el truco `<picture>` para versión oscura):

```markdown
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/TU-USUARIO/TU-USUARIO/output/github-contribution-grid-snake-dark.svg">
  <img alt="Snake animation" src="https://raw.githubusercontent.com/TU-USUARIO/TU-USUARIO/output/github-contribution-grid-snake.svg">
</picture>
```

En repos públicos los workflows son gratis y una corrida diaria tarda un minuto. El error que rompe más perfiles de los que imaginas: **si tu repo se queda 60 días sin actividad, GitHub desactiva los workflows programados.** No hay aviso — la serpiente se congela en el último SVG y parece culpa del servicio cuando el workflow está pausado. Arreglo: pestaña Actions → Enable workflow → haz un commit para reiniciar el reloj. Usa versiones recientes de las actions: su runtime migró a Node 24 en junio de 2026 y las viejas dejaron de correr.

Dos automatizaciones más si las necesitas: lowlighter/metrics (infografías con 30+ plugins; su instancia compartida está crónicamente limitada — la ruta estable es correrlo como Action en tu repo) y gautamkrishnar/blog-post-workflow (tus posts recientes vía RSS entre dos etiquetas de comentario).

## Por qué tu tarjeta muestra datos viejos

Actualizaste tus stats y la tarjeta sigue en ayer. Casi siempre son dos cachés apiladas: la del widget (`cache_seconds` guarda la imagen 6 horas por defecto) y la de camo, el proxy de GitHub — toda imagen externa de un README pasa por `camo.githubusercontent.com`, que guarda su propia copia.

El arreglo rápido: haz que camo vea una URL nueva con un parámetro desechable (`&v=2`, luego `&v=3`...). Existe un `curl -X PURGE` contra la URL de camo, pero úsalo con moderación: obliga a todos los usuarios de GitHub a re-descargar la imagen. Dato bonus de privacidad: como quien pide la imagen es el proxy de GitHub y no el navegador del visitante, los widgets no ven las IPs de quien te lee.

## Seguridad: tokens y lo que expones

Tres reglas que no se negocian:

1. **Cada herramienta recibe el token mínimo.** Stats self-hosted usa un PAT clásico sin permisos (en variables de entorno de Vercel, no en secrets del repo); las Actions que guardan archivos en tu repo (serpiente, summary cards, 3D) usan un token fine-grained limitado a ese repo; metrics usa un PAT sin permisos para datos públicos.
2. **Un token jamás va en el README, en el YAML ni en un commit.** El secret scanning de GitHub detecta los patrones `ghp_` y `github_pat_`, pero no confíes solo en eso.
3. **Si un token se filtra, revócalo de inmediato** en Settings → Developer settings. Borrar el commit no revoca nada.

Y lo que casi nadie revisa antes de publicar: el `mailto:` con tu correo a la vista garantiza spam (la ofuscación no funciona), una tarjeta de Steam pública expone biblioteca, horas y amigos, y los contadores registran telemetría. Ninguno es incorrecto por definición; todos deben ser decisiones conscientes. Yo conservo el Gmail y la Steam porque son parte de mi identidad de perfil — y sé exactamente qué estoy exponiendo.

## Contador de visitas y botón de sponsor

El contador más usado es el de komarev, y va bien arriba del saludo:

```markdown
![Profile Views](https://komarev.com/ghpvc/?username=Jesus-Valverde&color=blueviolet&style=for-the-badge&label=PROFILE+VIEWS)
```

El número es aproximado (la caché filtra parte del tráfico). Evita `visitor-badge.laobi.icu`, que todavía circula en colecciones de tarjetas: es el servicio más frágil de su categoría. El botón de sponsor es un badge-enlace a tu página de GitHub Sponsors:

```markdown
[![Sponsor Me](https://img.shields.io/badge/Sponsor_Me-blueviolet?style=for-the-badge&logo=githubsponsors&logoColor=white)](https://github.com/sponsors/Jesus-Valverde)
```

El detalle que se olvida: el enlace solo funciona con GitHub Sponsors activado — se hace aparte en github.com/sponsors (disponible en México; pide Stripe o PayPal para cobrar). Si prefieres saltarte el alta, Buy Me a Coffee es la alternativa sin trámites y su badge se pega igual.

## Generadores automáticos

Dos generadores de formulario hacen el mismo trabajo: el de rahuldkjain (en `rahuldkjain.github.io/github-profile-readme-generator`; llenas nombre, tagline, redes y skills y genera el Markdown con preview en vivo) y GPRM (`gprm.itsvg.in`; casillas por sección, más de 300 tecnologías y temas).

Para inspiración, dos colecciones que se complementan: `awesome-github-profile-readme` (más de 31,000 estrellas; perfiles reales renderizados para copiar) y `Awesome-Profile-README-templates` (11,200★; plantillas puras por estilo — cortas, elaboradas, con código, multimedia). Como techo saludable, la propia guía lo dice: una o dos tarjetas, máximo tres.

El costo del atajo: generan perfiles clon. Un generador es un buen punto de partida; el valor está en lo que le agregas después. Sobre los generadores con IA que proliferaron en 2025-2026: existen, pero casi toda la evidencia de su calidad viene del marketing de quienes los venden.

## ¿Un README decorado ayuda a conseguir trabajo?

Busqué a propósito evidencia en contra de la premisa "un README decorado ayuda profesionalmente", y el resultado es: no existe ningún estudio que lo mida en ninguna dirección.

Lo que hay son anécdotas de practicantes, citadas como tales: los reclutadores raramente escrutan GitHub (la señal útil es el código, no los widgets); los hiring managers técnicos sí abren el perfil y valoran el pulido, pero son una minoría. Conclusión práctica: el README decorado es un adorno barato que comunica cuidado ante quien lee código — cuesta una tarde y no promete nada medible. Lo que de verdad pesa en tu portafolio está fuera del README: repos fijados con código real y bien documentado. Primero esa base; la decoración va encima.

## Problemas comunes

Cuando tu README no renderiza o algo se ve roto, revisa en este orden:

1. **El perfil está en blanco:** repo público, nombre exacto a tu username, `README.md` con contenido en la raíz (no en una subcarpeta).
2. **Una imagen se ve rota:** abre su URL en pestaña privada. 404 o página de error = URL mal formada (revisa las reglas de escape de badges).
3. **Un badge está congelado:** entra a la pestaña Actions antes de culpar al servicio. Si el workflow fue auto-desactivado por los 60 días, reactívalo y haz un commit.
4. **Se ve mal en móvil:** el culpable suele ser una imagen de ancho fijo (`<img width="850">`) o una muralla de badges. Lo esencial, arriba.
5. **Un lector de pantalla no entiende nada:** cada imagen necesita `alt` descriptivo. Es gratis y es lo primero que revisa quien llega con tecnología asistiva.

No hay límite documentado de longitud; "mantenlo corto y lo importante arriba" es consenso de la práctica, no una regla de GitHub.

## Plantilla para empezar

Base mínima y decente para empezar la tuya. Reemplaza los datos, commítala a tu repo especial y agrega piezas una a una:

```markdown
# ¡Hola! Soy TU NOMBRE 👋

Estudiante/desarrollador(a) desde México 🇲🇽, construyendo cosas en la web.

- 🔭 Ahora mismo: [proyecto actual]
- 🌱 Aprendiendo: [tecnología actual]
- 📫 Contacto: [LinkedIn o formulario]

## Tecnologías

[![My Skills](https://skillicons.dev/icons?i=js,html,css,react&theme=dark)](https://skillicons.dev)

## Stats

![Mis stats de GitHub](https://github-readme-stats.vercel.app/api?username=TU-USUARIO&show_icons=true&theme=tokyonight)

<details>
<summary>Más sobre mí</summary>

Lo que quieras contar, con una línea en blanco antes para que renderice.

</details>
```

Cada pieza que agregues después ya sabes qué cuesta, de quién depende y cómo se arregla cuando se rompe. Ese conocimiento es la diferencia entre un perfil que se ve bien el día del tutorial y uno que sigue vivo un año después.

---

## Lo esencial en 5 puntos

1. El mecanismo completo son tres condiciones: repo público, nombre exacto a tu username, y `README.md` con contenido en la raíz.
2. Las tarjetas de datos son imágenes servidas por terceros; el modo robusto es self-hostear la instancia de stats y preferir widgets que guardan el SVG en tu propio repo.
3. "Mi tarjeta está vieja" casi siempre son dos cachés apiladas: la del widget (6 h) y la de camo; el arreglo barato es `&v=2`.
4. Los workflows programados se auto-desactivan tras 60 días sin actividad del repo; tu serpiente se congela sin avisar.
5. Los tokens van con permiso mínimo, en secrets, jamás en texto; y el beneficio profesional del README decorado es anécdota, no dato: primero repos fijados con código real.

## Fuentes

- GitHub Docs — Managing your profile README; Basic writing and formatting syntax; About anonymized URLs; Disabling and enabling a workflow (verificadas 2026-10-27)
- README crudo del perfil `Jesus-Valverde/Jesus-Valverde` (2026-10-27)
- anuraghazra/github-readme-stats (README + discusión #4433); DenverCoder1/github-readme-streak-stats; ryo-ma/github-profile-trophy
- Platane/snk (repo y workflow propio); lowlighter/metrics; gautamkrishnar/blog-post-workflow
- tandpfun/skill-icons; syvixor/skills-icons; badges/shields (docs); kyechan99/capsule-render; DenverCoder1/readme-typing-svg
- antonkomarev/github-profile-views-counter; vn7n24fzkq/github-profile-summary-cards; yoshi389111/github-profile-3d-contrib
- VishwaGauravIn/github-profile-readme-maker; rahuldkjain/github-profile-readme-generator; abhisheknaiidu/awesome-github-profile-readme; kautukkundan/Awesome-Profile-README-templates; jonatasemidio/multilanguage-readme-pattern
- The Register (17-dic-2025) y changelogs de github.blog sobre pricing y runners
- Underdog.io, hilo de Glassdoor (jul-2025) y discusión #182100 (dic-2025) — evidencia anecdótica contra-premisa
