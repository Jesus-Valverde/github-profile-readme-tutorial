[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md) [![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)

# Cómo personalizar tu README de perfil de GitHub (con mi perfil como ejemplo)


Este tutorial te enseña a armar el README de tu perfil de GitHub: el repo especial que lo activa, los badges, las tarjetas automáticas de estadísticas, la serpiente con GitHub Actions, y los errores que dejan perfiles rotos. Todo está probado en mi propio perfil, que uso como ejemplo a lo largo del tutorial.

## Cómo crear tu README y que se muestre en tu perfil

GitHub muestra un README en tu perfil cuando cumples tres cosas:

1. El repositorio es **público**.
2. El nombre del repo es exactamente tu nombre de usuario (en mi caso, `Jesus-Valverde`).
3. El repo tiene un archivo `README.md` con contenido, en la raíz.

Si falta cualquiera de las tres, tu perfil queda en blanco. No hay nada más que configurar.

Para crearlo: en github.com, botón `+` → **New repository**. Nómbralo igual que tu usuario, márcalo como **Public**, activa la casilla **Add a README** y crea el repo. Al abrirlo, GitHub detecta que es tu repo especial y te muestra el botón **Edit README** directo en tu perfil.

Tres casos especiales:

- Si tu cuenta la administra una empresa con GitHub Enterprise Managed Users, no puedes tener perfil personalizado: la documentación oficial lo excluye.
- Si creaste el repo con tu nombre antes de julio de 2020, no se muestra solo: entra al repo y presiona el botón **Share to profile**.
- Los logros (achievements) siguen existiendo a octubre de 2026, pero la documentación tiene páginas caídas y dos insignias ya no se pueden ganar. Trátalos como adorno, no como meta.

## Mi perfil como ejemplo

Este tutorial nació de un pendiente real: mi perfil tenía una sección que decía "👉 Tutorials", con un GIF de "loading..." y la admisión de que estaba sin terminar. Lo que sigue es la anatomía de lo que ya construí: qué hace bien, qué le faltaba y qué es frágil.

Mi `README.md` pesa 3,369 bytes y tiene esta estructura: un saludo, la sección Tutorials (el placeholder), una sección de quién soy con la bandera de México, otra de estudios, una fila de 11 badges de tecnologías, 3 botones hacia plataformas de práctica (freeCodeCamp, Exercism, HackerRank), 3 de contacto (LinkedIn, Linktree, correo) y una tarjeta de mi perfil de Steam. Son 17 badges en total, todos servidos por shields.io con el estilo `for-the-badge`.

Cada badge se ve así (este es real, copiado de mi archivo):

```markdown
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
```

Dos cosas que mi perfil hace bien sin haberlo planeado: todas las imágenes tienen texto alternativo (`alt`) y las secciones usan encabezados `##` correctos. Eso lo hace legible para lectores de pantalla, que es justo lo que recomienda la guía de accesibilidad de GitHub.

Lo que le faltaba: tarjetas de estadísticas, racha de contribuciones y la serpiente. Y dos fragilidades que te voy a señalar porque también puedes caer en ellas: la tarjeta de Steam la sirve un servicio comunitario (`card.yuy1n.io`) sin respaldo — si ese servicio cierra, se rompe el bloque más grande de mi perfil. Y el botón de correo usa un enlace `mailto:` con mi Gmail a la vista, que los recolectores de spam leen con gusto. Más abajo van los candados.

## Badges con shields.io

Un badge es una imagen que shields.io genera a partir de su propia URL. El formato base es `img.shields.io/badge/ETIQUETA-MENSAJE-COLOR`, y casi todo el control está en los parámetros de la URL: `style` elige el estilo (`flat` es el default; también `flat-square`, `plastic`, `for-the-badge` y `social`), `logo` toma el nombre de cualquier ícono del catálogo simple-icons, y `logoColor` y el color del badge aceptan colores hex.

Tres reglas de escape causan el 90% de los badges rotos:

- El guion `-` separa segmentos, así que un guion literal se escribe `--`.
- El guion bajo literal se escribe `__`.
- El `#` de los colores hex va codificado como `%23` (aunque un hex sin `#` también funciona).

Para que el badge sea clicleable, no uses el parámetro `link=` (no funciona dentro de `<img>`): envuelve la imagen Markdown en un enlace normal:

```markdown
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/tu-usuario/)
```

Sobre límites: shields.io no publica cifras de cuota; los cuellos de botella reales suelen estar en el servicio externo que el badge consulta, no en shields mismo.

## Íconos sin texto con skill-icons

Una alternativa compacta a las filas de badges es skill-icons: una sola URL que dibuja una cuadrícula de íconos redondeados.

```markdown
[![My Skills](https://skillicons.dev/icons?i=js,html,css,react,py,flask&theme=dark)](https://skillicons.dev)
```

Los ids son nombres en minúsculas (`js`, `py`, `react`, `nextjs`, `kubernetes`...), el tema default es `dark` y `perline` controla cuántos íconos van por línea (1 a 50). La desventaja: sin texto al lado, un muro de logos es menos legible para quien no reconoce los íconos. Para un portafolio, los badges con nombre explícito comunican mejor; los íconos compactos ganan cuando la lista es larga.

Si te falta un ícono: skillicons.dev no tiene todos (React Router y JWT devuelven cuadros vacíos). La alternativa `skills.syvixor.com` tiene más de 1,059 íconos — incluyendo `reactrouter` y `jwt` — y cambia de tema claro/oscuro según la preferencia del visitante.

## README en dos idiomas

Para ofrecer tu perfil en más de un idioma, pon una fila de badges de idioma arriba del README, cada uno con enlace a su versión:

```markdown
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md)
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)
```

La convención de archivos es el sufijo de idioma: `README.md` como principal y `README.es.md` para español. Cada versión lleva la misma fila de badges, así que el lector salta entre idiomas desde cualquiera. Ten en cuenta que GitHub solo renderiza `README.md` en tu página de perfil (no ejecuta JavaScript, así que no hay selector de idioma "en el sitio"): el badge lleva al repo, donde sí se lee la versión completa.

## El formato nativo de GitHub

Antes de instalar nada, aprovecha lo que GitHub ya soporta: secciones colapsables, llamadas de atención, notas al pie y una etiqueta para imagen según tema claro/oscuro. Sin servicios externos, sin tokens, sin mantenimiento.

Sección colapsable (útil para no aplastar al visitante con texto):

```html
<details>
<summary>Mi trayectoria en detalle</summary>

Aquí va el contenido. Debe haber una línea en blanco después de `<summary>`
para que el Markdown interno se renderice.

</details>
```

Las llamadas de atención (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`) se escriben dentro de un blockquote. La documentación oficial pide moderación: máximo una o dos por documento, solo para información crucial. Ojo: solo renderizan en github.com; en otros visores quedan como blockquote plano.

Y el formato nativo más subestimado: la imagen que cambia según el tema del visitante.

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="banner-dark.svg">
  <img alt="Banner de bienvenida" src="banner-light.svg">
</picture>
```

## Banners y efectos animados (con moderación)

Si quieres un encabezado con presencia, las dos herramientas estándar son capsule-render (banners SVG con formas y animaciones) y readme-typing-svg (texto que se escribe y se borra).

```markdown
![header](https://capsule-render.vercel.app/api?type=wave&color=gradient&height=200&section=header&text=Tu%20Nombre&fontSize=42&animation=fadeIn)

![typing](https://readme-typing-svg.demolab.com/?font=Fira+Code&size=22&pause=1000&multiline=true&width=600&height=80&lines=Desarrollador+web;Aprendiendo+Flask+y+React)
```

El parámetro `multiline=true` apila varias frases separadas por punto y coma, en lugar de reescribir todo en una línea.

Antes de llenar tu perfil de efectos, considera el costo: cada efecto es una dependencia externa más, los GIFs decorativos pesan megabytes, ninguno respeta la preferencia de movimiento reducido del sistema, y banner + texto animado + GIF + badges juntos dan el perfil saturado que la comunidad señala como mal ejemplo. Mi regla, sacada de mi propio perfil: el GIF de "loading..." funciona porque es uno solo y cuenta una historia. Dos más ya serían ruido.

## Tarjetas de estadísticas

Aquí vive el corazón del ecosistema: servicios comunitarios que convierten tu actividad de GitHub en tarjetas de imagen.

La tarjeta de estadísticas, de anuraghazra (github-readme-stats):

```markdown
![Mis stats de GitHub](https://github-readme-stats.vercel.app/api?username=Jesus-Valverde&show_icons=true&theme=tokyonight)
```

La de racha de contribuciones (streak), de DenverCoder1:

```markdown
![GitHub Streak](https://streak-stats.demolab.com?user=Jesus-Valverde&theme=tokyonight)
```

La de trofeos, de ryo-ma:

```markdown
![Trophy](https://github-profile-trophy.vercel.app/?username=Jesus-Valverde)
```

Y una cuarta que se suele olvidar y es la única verdaderamente automática: la de lenguajes más usados. GitHub la calcula de tus repos reales — la fila de badges cuenta lo que tú dices que sabes; esta cuenta lo que tu código dice que haces:

```markdown
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Jesus-Valverde&layout=compact&theme=tokyonight&langs_count=8)
```

Parámetros útiles de la tarjeta de stats: `include_all_commits=true` cuenta commits de toda la vida (sin él, solo del año), `hide_border=true` la integra mejor al fondo, `layout=compact` vuelve la tarjeta de lenguajes una lista compacta en vez de barras, `langs_count` controla cuántos lenguajes muestra, y `cache_seconds` controla cuánto se cachea la imagen (mínimo 6 horas, máximo 24).

Si pones dos tarjetas lado a lado (con `width` en porcentajes, que se apilan solas en móvil), anclalas con `align="top"`: GitHub alinea las imágenes por su línea de texto y, como las tarjetas tienen alturas naturales distintas, la más corta queda flotando abajo. Si además quieres que midan lo mismo, compensa con el reparto del ancho: mi tarjeta de stats mide 467×195 píxeles y la de racha 495×195; con `width="48%"` y `width="51%"` quedan empatadas a cualquier tamaño de ventana.

El problema que debes conocer antes de instalar nada: las instancias hospedadas comparten la cuota anónima de la API de GitHub y por eso fallan a ratos. La solución recomendada por el propio equipo del proyecto es desplegar tu instancia en Vercel, y toma unos 15 minutos: haces fork del repo, lo conectas a Vercel, y en las variables de entorno de Vercel agregas `PAT_1` con un Personal Access Token (PAT: la llave que GitHub usa para autorizar programas) clásico sin ningún permiso marcado. Después cambias la URL de la tarjeta de `github-readme-stats.vercel.app` a la de tu instancia. La de racha tiene el mismo proceso documentado; la de trofeos sigue arriba tal cual.

## Otros widgets

Hay un segundo círculo de widgets populares. Lo que decide su robustez es quién sirve la imagen cuando alguien visita tu perfil:

| Widget | ¿Quién sirve la imagen? | Si el tercero falla |
|---|---|---|
| Contador de vistas (komarev) | Su servidor, en cada visita | Badge roto o desactualizado |
| Activity graph (ashutosh00710) | Su Vercel, en cada visita | Imagen rota (mismo riesgo que stats) |
| Summary cards (vn7n24fzkq) | Una Action **guarda los SVG en tu repo** | Nada: la imagen ya es tuya |
| 3D contributions (yoshi389111) | Una Action guarda el SVG en tu repo | Nada: mismo patrón |
| WakaTime (tiempo de código) | Su API + Action diaria | Sección vacía o con error |

El patrón más robusto del ecosistema es el "committed": la Action corre en tu repo, genera el SVG y lo guarda como parte de tu repositorio. La imagen que el visitante carga vive en `raw.githubusercontent.com` — en GitHub, no en un servidor ajeno que puede fallar a las 3 a.m.

Dos avisos de este círculo: el contador de vistas es aproximado (la caché de GitHub filtra parte del tráfico; su propio mantenedor lo describe como un "tracking pixel" y ha dejado de mostrarse bajo carga), y WakaTime exige activar "Display activity publicly" en tu cuenta de WakaTime y se actualiza una vez al día.

## La serpiente con GitHub Actions

La animación más querida del ecosistema es la serpiente que se come tu cuadrícula de contribuciones (Platane/snk). Aquí la imagen se genera en tu propio repo y se guarda en un branch llamado `output` — después de eso no depende de nadie.

Crea el archivo `.github/workflows/snake.yml`:

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

Y lo embebes apuntando al raw del branch `output`:

```markdown
![Snake animation](https://raw.githubusercontent.com/Jesus-Valverde/Jesus-Valverde/output/github-contribution-grid-snake.svg)
```

En repos públicos los workflows son gratis, y una corrida diaria de la serpiente tarda alrededor de un minuto. El error que rompe más perfiles de los que imaginas: **si tu repo se queda 60 días sin actividad, GitHub desactiva los workflows programados automáticamente.** No hay aviso en el README — tu serpiente simplemente se congela en el último SVG y parece culpa del servicio cuando el workflow está pausado. El arreglo: pestaña Actions → seleccionar el workflow → Enable workflow, y hacer un commit para reiniciar el reloj.

Otro detalle de mantenimiento: usa versiones recientes de las actions. Su runtime migra cada año (de Node 20 a Node 24 desde junio de 2026) y las actions viejas dejaron de correr.

Dos automatizaciones más si las necesitas: lowlighter/metrics genera infografías con más de 30 plugins (su instancia compartida está crónicamente limitada; la ruta estable es correrlo como Action en tu repo), y gautamkrishnar/blog-post-workflow inserta tus posts recientes entre dos etiquetas de comentario, vía RSS.

## Por qué tu tarjeta muestra datos viejos

Actualizaste tus stats y la tarjeta sigue mostrando los datos de ayer. Casi siempre es caché, y hay dos capas:

1. **La caché del widget:** `cache_seconds` de github-readme-stats guarda la imagen 6 horas por defecto.
2. **La caché de camo:** toda imagen externa de un README pasa por el proxy de GitHub (`camo.githubusercontent.com`), que guarda su propia copia.

El arreglo rápido es hacer que camo vea una URL nueva: agrega un parámetro desechable (`&v=2`, luego `&v=3`...). Existe también un `curl -X PURGE` contra la URL de camo para invalidar una imagen puntual, pero úsalo con moderación: obliga a todos los usuarios de GitHub a re-descargar la imagen.

Dato bonus de privacidad: como quien hace la petición al servicio externo es el proxy de GitHub y no el navegador del visitante, los widgets no ven las IPs de quien te lee.

## Seguridad: tokens y lo que expones

Tres reglas que no se negocian:

1. **Cada herramienta recibe el token mínimo.** La instancia self-hosted de stats usa un PAT clásico sin permisos (en variables de entorno de Vercel, no en secrets del repo); las Actions que guardan archivos en tu repo (serpiente, summary cards, 3D) usan un token fine-grained limitado a ese repo; metrics usa un PAT sin permisos para datos públicos.
2. **Un token jamás va en el README, en el YAML del workflow ni en un mensaje de commit.** La protección de secretos de GitHub detecta los patrones `ghp_` y `github_pat_` al hacer push, pero no confíes solo en eso.
3. **Si un token se filtra, revócalo de inmediato** en Settings → Developer settings. Borrar el commit no revoca nada.

Y la parte que casi nadie revisa antes de publicar: qué dice de ti tu README a personas que no son tu público. El `mailto:` con tu correo a la vista garantiza spam (la ofuscación con JavaScript o imágenes no funciona: los recolectores la superan). Una tarjeta de Steam pública expone tu biblioteca, tus horas de juego y tu lista de amigos. Los contadores de vistas registran telemetría de tu perfil. Ninguno es incorrecto por definición; todos deben ser decisiones conscientes. En mi caso conservo el Gmail y la tarjeta de Steam porque son parte de mi identidad de perfil — y sé exactamente qué estoy exponiendo.

## Contador de visitas y botón de sponsor

Dos badges cortos que casi todos piden. El contador de vistas más usado es el de komarev, y va bien arriba del saludo:

```markdown
![Profile Views](https://komarev.com/ghpvc/?username=Jesus-Valverde&color=blueviolet&style=for-the-badge&label=PROFILE+VIEWS)
```

Recuerda que el número es aproximado (la caché filtra parte del tráfico). Evita `visitor-badge.laobi.icu`, que todavía circula en colecciones de tarjetas: es el servicio más frágil de su categoría.

El botón de sponsor es un badge-enlace a tu página de GitHub Sponsors:

```markdown
[![Sponsor Me](https://img.shields.io/badge/Sponsor_Me-blueviolet?style=for-the-badge&logo=githubsponsors&logoColor=white)](https://github.com/sponsors/Jesus-Valverde)
```

El detalle que se olvida: el enlace solo funciona si tienes GitHub Sponsors activado, y eso se hace aparte en github.com/sponsors (disponible en México; te pide una cuenta de Stripe o PayPal para cobrar). Si prefieres saltarte ese alta, Buy Me a Coffee es la alternativa sin trámites, y su badge se pega igual.

## Generadores automáticos

Si quieres saltarte el armado manual, hay dos generadores de formulario: el de rahuldkjain (en `rahuldkjain.github.io/github-profile-readme-generator`; llenas nombre, tagline, redes y skills, y te genera el Markdown con preview en vivo) y GPRM (`gprm.itsvg.in`; casillas por sección, más de 300 tecnologías y temas).

Para inspiración, dos colecciones que se complementan: `awesome-github-profile-readme` (más de 31,000 estrellas; ves perfiles reales renderizados y copias el Markdown del que te guste) y `Awesome-Profile-README-templates` (11,200★; plantillas puras organizadas por estilo — cortas, elaboradas, con código, multimedia). Como techo saludable, la propia guía lo dice: una o dos tarjetas, máximo tres.

El costo del atajo: generan perfiles clon. Cuando miles de personas marcan las mismas casillas, los perfiles se parecen entre sí. Un generador es un buen punto de partida; el valor está en lo que le agregas después. Y sobre los generadores con IA que proliferaron en 2025-2026: existen, pero casi toda la evidencia de su calidad viene del marketing de quienes los venden.

## ¿Un README decorado ayuda a conseguir trabajo?

Busqué a propósito evidencia en contra de la premisa "un README decorado ayuda profesionalmente", y el resultado es: no existe ningún estudio que lo mida en ninguna dirección.

Lo que hay son anécdotas de practicantes, citadas como tales: los reclutadores raramente escrutan GitHub (la señal útil es el código, no los widgets); los hiring managers técnicos sí abren el perfil y valoran el pulido, pero son una minoría de los que lo miran. La conclusión práctica: el README decorado es un adorno barato que comunica cuidado ante quien lee código — cuesta una tarde y no promete nada medible. Lo que de verdad pesa en tu portafolio está fuera del README: repos fijados con código real y bien documentado. Primero esa base; la decoración va encima.

## Problemas comunes

Cuando tu README no renderiza o algo se ve roto, revisa en este orden:

1. **El perfil está en blanco:** verifica que el repo sea público, que el nombre coincida exactamente con tu username y que `README.md` no esté vacío ni en una subcarpeta.
2. **Una imagen se ve rota:** abre su URL en una pestaña privada. Si responde 404 o una página de error, la URL está mal formada (revisa las reglas de escape de badges).
3. **Un badge está congelado:** entra a la pestaña Actions de tu repo antes de culpar al servicio. Si el workflow fue auto-desactivado por los 60 días de inactividad, reactívalo y haz un commit.
4. **Se ve mal en móvil:** el culpable suele ser una imagen de ancho fijo (`<img width="850">`) o una muralla de badges que empuja lo importante fuera de la primera pantalla. Pon lo esencial arriba.
5. **Un lector de pantalla no entiende nada:** cada imagen necesita `alt` descriptivo. Es gratis y es lo primero que revisa quien llega con tecnología asistiva.

No hay límite documentado de longitud para un README; "mantenlo corto y lo importante arriba" es el consenso de la práctica, no una regla de GitHub.

## Plantilla para empezar

Con todo lo anterior, esta es una base mínima y decente para empezar la tuya. Reemplaza los datos, commítala a tu repo especial, y ve agregando piezas una a una:

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

Cada pieza que agregues después (streak, serpiente, contador) ya sabes qué cuesta, de quién depende y cómo se arregla cuando se rompe. Ese conocimiento es la diferencia entre un perfil que se ve bien el día del tutorial y uno que sigue vivo un año después.

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
- VishwaGauravIn/github-profile-readme-maker; abhisheknaiidu/awesome-github-profile-readme
- The Register (17-dic-2025) y changelogs de github.blog sobre pricing y runners
- Underdog.io, hilo de Glassdoor (jul-2025) y discusión #182100 (dic-2025) — evidencia anecdótica contra-premisa
