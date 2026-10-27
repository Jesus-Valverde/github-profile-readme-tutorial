# Tutorial — Personaliza tu README de perfil de GitHub (caso real: el mío)


## Objetivos de aprendizaje

Al terminar este tutorial podrás:

1. Explicar cómo GitHub decide mostrar un README en tu perfil, y crear el repo especial en menos de dos minutos.
2. Construir las piezas estáticas (badges, íconos, secciones nativas de Markdown) con código que copias y pegas sin miedo.
3. Agregar tarjetas de datos automatizadas con GitHub Actions, sabiendo de antemano qué se rompe, cuándo y por qué.
4. Decidir con criterio qué agregar y qué no, considerando seguridad, privacidad y la evidencia real (escasa) sobre si esto ayuda profesionalmente.

---

## El truco de dos minutos: un repo con tu nombre

GitHub muestra un README en tu perfil cuando existe un repositorio público cuyo nombre es exactamente tu username y que contiene un archivo `README.md` con contenido en su raíz. Las tres condiciones se evalúan juntas: si privatizas el repo, vacías el archivo o cambias el nombre, el perfil vuelve a quedar en blanco. Es todo el mecanismo; no hay configuración adicional.

Para crearlo: en github.com, botón `+` → **New repository**. Nómbralo exactamente como tu usuario (en mi caso, `Jesus-Valverde`). Marca **Public**, activa la casilla **Add a README** y crea el repo. Al abrirlo, GitHub detecta que es tu repo especial y te ofrece el botón **Edit README** directo en tu perfil.

Tres excepciones que suelen sorprender:

- Si tu cuenta es de tipo *managed* (administrada por una empresa con GitHub Enterprise Managed Users), no puedes tener perfil personalizado; la documentación oficial lo excluye explícitamente.
- Si creaste un repo con tu nombre antes de julio de 2020, no aparece solo: entra al repo y presiona el botón **Share to profile**.
- Las URLs de la documentación oficial se reorganizaron en 2025, así que muchos tutoriales antiguos enlazan rutas que hoy son redirecciones. El contenido sigue ahí; el enlace es lo que envejeció.

Una nota sobre los logros (achievements): circula el rumor de que GitHub los retiró. Lo verificado a octubre de 2026 es otra cosa: la página de documentación de achievements devuelve error 404, dos badges ya no se pueden ganar, y usuarios reportan insignias congeladas desde 2025. Pero no existe anuncio oficial de retiro, y badges como Pull Shark siguen listados como obtenibles. Si te los cruzas en un tutorial, trátalos como adorno inestable, no como meta.

## Mi perfil, abierto en la mesa

Este tutorial nació de un pendiente real: mi perfil tiene una sección que dice "👉 Tutorials", con un GIF de "loading..." y una admisión de que está sin terminar. Lo que sigue es la anatomía de lo que ya construí, con lo bueno, lo frágil y lo que faltaba.

Mi `README.md` pesa 3,369 bytes y tiene esta estructura: un saludo, la sección Tutorials (el placeholder), una sección de quién soy con la bandera de México, otra de estudios, una fila de 11 badges de tecnologías, 3 botones hacia plataformas de práctica (freeCodeCamp, Exercism, HackerRank), 3 de contacto (LinkedIn, Linktree, correo) y una tarjeta de mi perfil de Steam. Son 17 badges en total, todos servidos por shields.io con el estilo `for-the-badge`.

El patrón de cada badge se ve así (este es el real, copiado del archivo):

```markdown
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
```

Lo que mi README hace bien, sin haberlo planeado: todas las imágenes tienen texto alternativo (`alt`), uso `<br>` para controlar saltos de línea, y las secciones usan encabezados `##` correctos. Eso lo hace legible para lectores de pantalla, que es exactamente lo que la guía de accesibilidad de GitHub recomienda para perfiles.

Lo que le faltaba: tarjetas de estadísticas, racha de contribuciones y la famosa serpiente. Y dos fragilidades que voy a señalar con la misma franqueza: la tarjeta de Steam la sirve un servicio comunitario (`card.yuy1n.io`) sin respaldo; si ese servicio muere, se rompe el bloque más grande de mi perfil. Y el botón de correo usa un enlace `mailto:` con mi Gmail a la vista, que los recolectores de spam leen con gusto. Más abajo veremos los candados.

## La fábrica de badges: shields.io

Un badge es una imagen generada bajo demanda a partir de su propia URL. El formato base de shields.io es `img.shields.io/badge/ETIQUETA-MENSAJE-COLOR`, y casi todo el poder está en los parámetros de la query: `style` elige entre `flat` (el default), `flat-square`, `plastic`, `for-the-badge` y `social`; `logo` toma el nombre de cualquier ícono del catálogo simple-icons; `logoColor` y el color del badge aceptan hex.

Tres reglas de escape que causan el 90% de los badges rotos: el guion `-` separa segmentos, así que un guion literal se escribe `--`; el guion bajo literal se escribe `__`; y el `#` de los colores hex va codificado como `%23` (aunque un hex sin `#` también se acepta).

Para que el badge sea clicleable, no uses el parámetro `link=` (no funciona dentro de `<img>`); envuelve la imagen Markdown en un enlace normal:

```markdown
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/tu-usuario/)
```

Sobre límites del servicio: shields.io no publica cifras de cuota por cliente. Lo que se reporta en su tracker es que los límites reales suelen venir del servicio externo que el badge consulta, no de shields mismo. Si algún blog te da un número exacto de peticiones por minuto, desconfía: no está documentado.

## Íconos sin texto: skill-icons

Una alternativa compacta a las filas de badges es skill-icons: una sola URL que dibuja una cuadrícula de íconos redondeados.

```markdown
[![My Skills](https://skillicons.dev/icons?i=js,html,css,react,py,flask&theme=dark)](https://skillicons.dev)
```

Los ids son slugs en minúsculas (`js`, `py`, `react`, `nextjs`, `kubernetes`...), el tema default es `dark` y `perline` controla cuántos íconos por línea (1 a 50). El tradeoff: sin texto al lado, un muro de logos es menos legible para quien no reconoce los íconos. Para un perfil de portafolio, los badges con nombre explícito comunican mejor; los íconos compactos ganan cuando la lista es larga.

Detalle de 2026: el proyecto original (tandpfun) sigue vivo pero lento, con más de mil issues en fila. Existe una alternativa comunitaria más activa, `skills.syvixor.com`, con más de 1,059 íconos y una ventaja real: adapta el tema claro/oscuro automáticamente según la preferencia del visitante. Ese fallback me salió necesario el mismo día que publiqué este tutorial: skillicons.dev no tiene íconos de React Router ni JWT (devuelve cuadros vacíos, con HTTP 200 de engaño), y syvixor tiene ambos con los slugs `reactrouter` y `jwt`.

## Un README, dos idiomas

Si quieres ofrecer tu perfil en más de un idioma, el patrón canónico (del repo multilanguage-readme-pattern de jonatasemidio) cabe en una línea: una fila de badges de idioma arriba del README, cada uno con enlace a su variante.

```markdown
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md)
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)
```

La convención de archivos es el sufijo de idioma en la raíz: `README.md` como principal y `README.es.md` para español. Cada versión lleva la misma fila de badges, así que el lector salta entre idiomas desde cualquiera. La limitación honesta: GitHub solo renderiza `README.md` en tu página de perfil (no ejecuta JavaScript, así que no hay cambio de idioma "en el sitio"). El selector del perfil lleva al repo, donde sí se lee la versión completa en el otro idioma.

## Lo que GitHub ya te regala

Antes de instalar nada, aprovecha el formato nativo. GitHub soporta secciones colapsables, llamadas de atención, notas al pie y una etiqueta para imagen según tema claro/oscuro. Todo sin servicios externos, sin tokens, sin mantenimiento.

Sección colapsable (útil para no aplastar al visitante con texto):

```html
<details>
<summary>Mi trayectoria en detalle</summary>

Aquí va el contenido. Ojo: debe haber una línea en blanco después de `<summary>`
para que el Markdown interno se renderice.

</details>
```

Las llamadas de atención (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`) se escriben dentro de un blockquote. La documentación oficial pide moderación: máximo una o dos por documento, y solo para información crucial. Un caveat honesto: estas llamadas solo renderizan en github.com; en otros visores quedan como blockquote plano.

Y el truco más subestimado del formato nativo, la imagen que cambia según el tema del visitante:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="banner-dark.svg">
  <img alt="Banner de bienvenida" src="banner-light.svg">
</picture>
```

## Portada con efectos (úsalos con cuenta gotas)

Si quieres un encabezado con presencia, las dos herramientas estándar son capsule-render, que genera banners SVG con formas y animaciones, y readme-typing-svg, que simula texto que se escribe y se borra.

```markdown
![header](https://capsule-render.vercel.app/api?type=wave&color=gradient&height=200&section=header&text=Tu%20Nombre&fontSize=42&animation=fadeIn)

![typing](https://readme-typing-svg.demolab.com/?font=Fira+Code&size=22&pause=1000&multiline=true&width=600&height=80&lines=Desarrollador+web;Aprendiendo+Flask+y+React)
```

El parámetro `multiline=true` (incorporado en 2025) apila varias frases separadas por punto y coma, en lugar de reescribir todo en una línea.

La letra chica: cada efecto es una dependencia externa más, los GIFs decorativos pesan megabytes, ninguno respeta la preferencia de movimiento reducido del sistema, y al apilar banner animado + texto animado + GIF + badges obtienes el antipatrón que los críticos llaman "el perfil con 40 badges animados". Regla práctica que saco de mi propio caso: mi GIF de "loading..." funciona porque es uno solo y tiene propósito narrativo. Dos más ya serían ruido.

## Las tarjetas de datos

Aquí vive el corazón del ecosistema: tres servicios comunitarios que convierten tu actividad de GitHub en tarjetas de imagen.

La tarjeta de estadísticas, de anuraghazra (github-readme-stats):

```markdown
![Mis stats de GitHub](https://github-readme-stats.vercel.app/api?username=Jesus-Valverde&show_icons=true&theme=tokyonight)
```

La de racha (streak), de DenverCoder1:

```markdown
![GitHub Streak](https://streak-stats.demolab.com?user=Jesus-Valverde&theme=tokyonight)
```

Y la de trofeos, de ryo-ma:

```markdown
![Trophy](https://github-profile-trophy.vercel.app/?username=Jesus-Valverde)
```

De la misma familia que las de stats hay una cuarta que se suele olvidar y es la única verdaderamente automática de todas: la de lenguajes más usados, que GitHub calcula de tus repos reales (la fila de badges de tecnologías cuenta lo que tú dices que sabes; esta cuenta lo que tu código dice que haces):

```markdown
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Jesus-Valverde&layout=compact&theme=tokyonight&langs_count=8)
```

`layout=compact` la vuelve lista compacta en vez de barra de porcentajes, y `langs_count` controla cuántos lenguajes muestra.

Parámetros útiles de la tarjeta de stats: `include_all_commits=true` cuenta commits de toda la vida (sin él, solo del año), `hide_border=true` la integra mejor al fondo, y `cache_seconds` controla cuánto se cachea la imagen (el mínimo actual es 21,600 segundos, o sea 6 horas, y el máximo 86,400, es decir 24 horas; si un tutorial te dice que el mínimo son 4 horas, está desactualizado).

Si pones dos tarjetas lado a lado (con `width` en porcentajes, que se apilan solas en móvil), anclalas con `align="top"`: GitHub alinea las imágenes por la línea de texto, y como las tarjetas tienen proporciones naturales distintas, la más corta queda flotando abajo. Y si quieres que además midan exactamente lo mismo, compensa la proporción con el reparto del ancho. Lo verifiqué con mi propio perfil: la tarjeta de stats mide 467×195 píxeles y la de racha 495×195; con `width="48%"` y `width="51%"` las alturas renderizadas empatan al píxel, y al ser porcentajes siguen empatadas a cualquier tamaño de ventana.

Ahora el problema que ningún tutorial silencioso te cuenta: las instancias hospedadas comparten la cuota anónima de la API de GitHub, y eso las hace intermitentes. La discusión oficial del proyecto (septiembre de 2025) terminó con una recomendación clara del propio equipo: despliega tu propia instancia en Vercel con tu token. El proceso toma unos 15 minutos: haces fork del repo, lo conectas a Vercel, y en las variables de entorno de Vercel agregas `PAT_1` con un Personal Access Token (PAT, la llave de acceso personal que GitHub usa para autorizar programas) clásico sin ningún scope marcado. Después cambias la URL de la tarjeta de `github-readme-stats.vercel.app` a la de tu instancia. La de racha tiene el mismo patrón de self-hosting documentado; la de trofeos sigue arriba tal cual, estable pero sin desarrollo desde hace tiempo.

## Más allá del trío

Hay un segundo círculo de widgets populares. Entre ellos, lo que decide su robustez es quién sirve la imagen cuando alguien visita tu perfil:

| Widget | ¿Quién sirve la imagen? | Si el tercero falla |
|---|---|---|
| Contador de vistas (komarev) | Su servidor, en cada visita | Badge roto o desactualizado |
| Activity graph (ashutosh00710) | Su Vercel, en cada visita | Imagen rota (mismo riesgo que stats) |
| Summary cards (vn7n24fzkq) | Una Action **commitea los SVG a tu repo** | Nada: la imagen ya es tuya |
| 3D contributions (yoshi389111) | Una Action commitea el SVG a tu repo | Nada: patrón committed |
| WakaTime (tiempo de código) | Su API + Action diaria | Sección vacía o con error |

Ese patrón "committed" es el más robusto del ecosistema: la Action corre en tu repo, genera el SVG y lo guarda como parte de tu propio repositorio. La imagen que el visitante carga vive en `raw.githubusercontent.com`, o sea en GitHub, no en un servidor ajeno que puede hacer cold start a las 3 a.m.

Dos avisos del círculo extra. El contador de vistas es gratis pero vive en un servidor compartido con capacidad limitada (ha dejado de mostrarse bajo carga, según su propio tracker), y su mantenedor lo describe honestamente como un "tracking pixel": cuenta visitas de forma aproximada porque la caché de GitHub filtra parte del tráfico. Y WakaTime exige activar "Display activity publicly" en tu cuenta de WakaTime y refresca aproximadamente una vez al día, porque el estándar es un cron diario.

## La serpiente: tu primera automatización

La animación más querida del ecosistema es la serpiente que se come tu cuadrícula de contribuciones (Platane/snk). A diferencia de las tarjetas, aquí la imagen se genera en tu propio repo y se guarda en un branch llamado `output`; después de eso no depende de nadie.

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

El costo: en repos públicos los minutos de Actions son gratis, y una corrida diaria de la serpiente tarda alrededor de un minuto. Pero hay una regla que rompe más perfiles de los que uno imagina: **si tu repo queda 60 días sin actividad, GitHub desactiva automáticamente los workflows programados.** La cita es literal de la documentación. Lo cruel es que no hay aviso en el README: tu serpiente simplemente se queda congelada en el último SVG generado, y uno culpa al servicio cuando el culpable es el workflow pausado. El remedio: pestaña Actions → seleccionar el workflow → Enable workflow, y hacer un commit para reiniciar el reloj de inactividad.

Sobre facturación, el panorama 2025-2026 cambió y conviene citarlo bien: GitHub propuso cobrar $0.002 por minuto a runners self-hosted, la propuesta se **pospuso** en diciembre de 2025 tras el rechazo comunitario (no está vigente ni formalmente cancelada); los precios de runners hospedados se **redujeron** hasta 39% desde enero de 2026; y los workflows en repos públicos siguen gratis. Si lees que "GitHub ahora cobra por Actions", la fuente está mal.

Otra automatización popular es lowlighter/metrics, que genera infografías con más de 30 plugins. Su instancia compartida (`metrics.lecoq.io`) existe pero está crónicamente limitada por cuota, en modo preview; la ruta actual es correrlo como Action en tu propio repo o montar tu instancia web con Docker. Ten en cuenta que varios de sus plugins están rotos por cambios de terceros (Skyline fue descontinuado por GitHub, Steam cambió su API en 2025). Y si escribes un blog, `gautamkrishnar/blog-post-workflow` inserta tus posts recientes entre dos etiquetas de comentario en tu README, vía RSS.

Un detalle técnico final: el runtime de las Actions está migrando de Node 20 a Node 24 (forzado desde junio de 2026), así que si pineas actions viejas puede que dejen de correr. Usa versiones recientes.

## ¿Por qué mi tarjeta está vieja? Las dos cachés

Este es el misterio que más confunde a los principiantes: actualizaste tus stats y la tarjeta sigue mostrando los datos de ayer. Casi siempre hay dos capas de caché apiladas, y hay que culpar a las dos.

La primera capa es la del propio widget: `cache_seconds` de github-readme-stats, que por default son 6 horas. La segunda es camo, el proxy de GitHub: toda imagen externa en un README se reescribe a una URL en `camo.githubusercontent.com`, y ese proxy guarda su propia copia de la respuesta. Tu tarjeta puede estar vieja por la capa del widget, por la de camo, o por la suma de ambas.

El remedio más simple es hacer que camo vea una URL nueva: agrega un parámetro desechable (`&v=2`, luego `&v=3`...). Es el fix clásico del proyecto (issue #632, de 2020) y sigue funcionando. Existe también un `curl -X PURGE` contra la URL de camo para invalidar una imagen puntual, pero úsalo con moderación: fuerza a todos los usuarios de GitHub a re-descargar la imagen. Y no confíes en `Cache-Control: no-cache` del origen: hay reportes documentados de que camo lo ignora por ventanas cortas.

Bonus de privacidad que sale gratis de este diseño: como quien hace la petición al servicio externo es el proxy de GitHub y no el navegador del visitante, los widgets no ven las IPs individuales de quien te lee. Volumen agregado sí; visitantes identificados, no.

## Candados: tokens y lo que expones

Tres reglas de seguridad que no se negocian. Primera: cada herramienta recibe el token mínimo. La instancia self-hosted de stats usa un PAT clásico sin scopes (en variables de entorno de Vercel, no en secrets del repo); las Actions que commitean a tu repo (serpiente, summary cards, 3D) usan un token fine-grained limitado a ese repo con permiso de lectura y escritura de contenidos, guardado como repository secret; metrics usa un PAT sin scopes para datos públicos. Segunda: un token jamás va en el README, en el YAML del workflow ni en un mensaje de commit. La protección de secretos de GitHub detecta los patrones `ghp_` y `github_pat_` al hacer push, pero no confíes solo en eso. Tercera: si un token se filtra, revócalo de inmediato en Settings → Developer settings; borrar el commit no revoca nada.

Y la parte que casi nadie revisa antes de publicar: qué dice de ti tu README a personas que no son tu público. El `mailto:` con tu correo a la vista garantiza spam (la ofuscación con JavaScript o imágenes no funciona; los harvesters la superan). Una tarjeta de Steam pública expone tu biblioteca, tus horas de juego y tu lista de amigos. Los contadores de vistas registran telemetría de tu perfil. Ninguno de estos es incorrecto por definición; todos deben ser decisiones conscientes. En mi caso: conservo el botón de Gmail y la tarjeta de Steam porque son parte de mi identidad de perfil, pero el tutorial que estás leyendo también existe para documentar que sé exactamente qué estoy exponiendo.

## Contador de visitas y botón de sponsor

Dos badges cortos que suelen pedirse a gritos. El contador de visitas más usado es el de komarev, y va bien arriba del saludo:

```markdown
![Profile Views](https://komarev.com/ghpvc/?username=Jesus-Valverde&color=blueviolet&style=for-the-badge&label=PROFILE+VIEWS)
```

Con los avisos que ya conoces del ecosistema: el número es aproximado (la caché de camo filtra parte del tráfico) y su propio mantenedor lo describe como un "tracking pixel". Evita el viejo `visitor-badge.laobi.icu` que todavía circula en colecciones de tarjetas: es el servicio frágil de la categoría. Y el botón de sponsor es un badge-enlace a `github.com/sponsors/TU-USUARIO`, con su logo oficial:

```markdown
[![Sponsor Me](https://img.shields.io/badge/Sponsor_Me-blueviolet?style=for-the-badge&logo=githubsponsors&logoColor=white)](https://github.com/sponsors/Jesus-Valverde)
```

El detalle que se olvida: el enlace solo funciona si tienes GitHub Sponsors activado, y eso se hace aparte, en github.com/sponsors (disponible en México; te pide una cuenta de Stripe o PayPal para cobrar). Puedes verificar si lo tienes activo consultando `sponsorsListing` en la API GraphQL de tu usuario. Si prefieres saltarte ese alta, Buy Me a Coffee es la alternativa sin papeleo, y su badge se pega igual.

## Generadores: el atajo y su letra chica

Si quieres saltarte el armado manual, el generador más citado es GPRM (gprm.itsvg.in): marcas casillas de secciones (redes, stack de más de 300 tecnologías, tarjetas, trofeos, contador), eliges tema, y te entrega el Markdown completo con preview en vivo. Dato curioso que corregimos durante la investigación de este tutorial: la misatribución más repetida de la blogosfera es darle el crédito a JayantGoel001; el autor real es Vishwa Gaurav, verificable en el repo y sus contribuidores. JayantGoel001 mantiene colecciones de plantillas famosas, de ahí la confusión.

La galería canónica de inspiración es `awesome-github-profile-readme`, una lista curada con más de 31,000 estrellas, activa a septiembre de 2026. Entra, elige un perfil que te guste y copia su Markdown crudo. Como catálogo de tarjetas organizadas por categoría (stats, contadores, sponsors), existe también Profile-Readme-Cards: sirve para ver el menú completo de un vistazo, pero verifica la frescura de cada recomendación — su contador sugerido (`visitor-badge.laobi.icu`) es justo el servicio frágil de su categoría. Y como techo saludable, su propia guía lo dice: una o dos tarjetas, máximo tres.

El precio del atajo: producen perfiles clon. Cuando miles de personas marcan las mismas casillas, los perfiles se parecen entre sí, y los hilos de feedback lo señalan seguido. Un generador es un buen punto de partida; el valor está en lo que le agregas después. Y sobre los generadores con IA que proliferaron en 2025-2026: existen, pero casi toda la evidencia de su calidad viene del marketing de quienes los venden.

## La pregunta incómoda: ¿esto te consigue trabajo?

Hicimos este tutorial con la regla de buscar activamente la fuente que contradiga la premisa. La premisa era "un README de perfil decorado ayuda profesionalmente". El resultado de la búsqueda: no existe evidencia cuantitativa en ninguna dirección. Ningún estudio mide el efecto de la decoración de READMEs en contrataciones.

Lo que sí hay son anécdotas de practicantes, y conviene citarlas como tales. El argumento más citado en contra viene del blog de Underdog.io, un marketplace de reclutamiento (o sea, un actor con incentivo propio en la tesis): los reclutadores raramente escrutan GitHub; la señal útil es el código, no los widgets. Un hilo de Glassdoor de julio de 2025 lo resume con matiz: no ayuda con recruiters en absoluto, pero sí ayuda con hiring managers técnicos, que son una minoría de los que miran tu perfil. Y una discusión de la comunidad de GitHub de diciembre de 2025 coincide: los revisores no técnicos no leen código, aunque pueden ojear actividad y pulido.

El frame honesto que saco de todo esto: el README decorado es un adorno barato, no una estrategia. Cuesta una tarde, no promete nada medible, y a la minoría técnica que sí abre tu perfil le comunica cuidado por los detalles. Lo que sí pesa en tu portafolio está fuera del README: repos pinned con código real y bien documentado. Primero esa base; la decoración va encima.

## Checklist: cuando algo no se ve

Cuando tu README no renderiza o algo se ve roto, revisa en este orden (cada paso resuelve una causa documentada):

1. **El perfil está en blanco:** verifica que el repo sea público, que el nombre coincida exactamente con tu username y que `README.md` no esté vacío. La variante sutil: el nombre está bien pero el archivo quedó en una subcarpeta.
2. **Una imagen se ve rota:** abre su URL en una pestaña privada. Si responde 404 o una página de error, la URL está mal formada. El proxy camo solo sirve lo que el origen devuelve; culpar a camo de una URL rota es el error clásico.
3. **Un badge está congelado:** entra a la pestaña Actions de tu repo antes de culpar al servicio. Si el workflow fue auto-desactivado por los 60 días de inactividad, reactívalo y haz un commit.
4. **Se ve mal en móvil:** GitHub reflowea el contenido correctamente; el culpable real suele ser un `<img width="850">` de ancho fijo, o una muralla de badges que empuja lo importante fuera de la primera pantalla. Pon lo esencial arriba.
5. **Un lector de pantalla no entiende nada:** cada imagen necesita `alt` descriptivo. Es gratis y es lo primero que revisa quien llega con tecnología asistiva.

No hay límite documentado de longitud para un README; "mantenlo corto y arriba del fold" es consenso de practicantes, no regla de GitHub.

## Tu plantilla de arranque

Con todo lo anterior, esta es una base mínima y decente para empezar la tuya. Reemplaza los datos, comítala a tu repo especial, y ve agregando piezas una a una:

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

Cada pieza que agregues después (streak, serpiente, contador) ya sabes qué cuesta, qué depende de quién y cómo se arregla cuando se rompe. Ese conocimiento es la diferencia entre un perfil que se ve bien el día del tutorial y uno que sigue vivo un año después.

---

## Puntos clave

Si olvidas todo lo demás, que sobreviva esto:

1. El mecanismo completo son tres condiciones: repo público con nombre exacto a tu username y `README.md` con contenido en la raíz.
2. Las tarjetas de datos son imágenes servidas por terceros; el modo robusto es self-hostear la instancia de stats y preferir widgets "committed" que guardan el SVG en tu propio repo.
3. "Mi tarjeta está vieja" casi siempre son dos cachés apiladas: la del widget y la de camo; el fix barato es `&v=2`.
4. Los workflows programados se auto-desactivan tras 60 días sin actividad del repo; tu serpiente se congela en silencio.
5. Los tokens van con scope mínimo, en secrets, jamás en texto; y el beneficio profesional del README decorado es anécdota, no dato: primero repos pinned con código real.

## Preguntas de reflexión

- Si mañana `card.yuy1n.io` (o cualquier servicio que uses) cerrara, ¿qué bloques de tu perfil morirían y cuáles sobrevivirían? Haz el inventario.
- Tu perfil tiene una audiencia que casi nunca llega (recruiters) y una que sí llega y lee código (hiring managers, otros devs). ¿Está tu README diseñado para la audiencia que realmente abre tu perfil?
- ¿Qué expone hoy tu README que no es una decisión consciente tuya?

## Glosario

- **PAT (Personal Access Token):** llave de acceso personal que autoriza a programas y Actions a actuar en tu cuenta de GitHub con los permisos (scopes) que les asignes.
- **Camo:** proxy de GitHub que reescribe toda imagen externa de un README a `camo.githubusercontent.com`; protege la privacidad del visitante y cachea las imágenes.
- **Rate limit:** límite de peticiones que una API permite en un periodo; cuando se agota, la API responde error.
- **Self-hosting:** desplegar tu propia copia de un servicio (por ejemplo, github-readme-stats en tu cuenta de Vercel) para no depender de la instancia compartida.
- **Commit:** guardar un cambio en el historial de un repositorio de Git.
- **Cron:** programador de tareas; en GitHub Actions define con qué frecuencia corre un workflow (por ejemplo, diario a medianoche UTC).
- **SVG:** formato de imagen vectorial que GitHub renderiza en los READMEs; es el formato nativo de casi todos los widgets.
- **Scope:** nivel de permiso que se le otorga a un token; el principio es asignar el mínimo necesario.

## Fuentes principales

- GitHub Docs — Managing your profile README; Basic writing and formatting syntax; About anonymized URLs; Disabling and enabling a workflow (verificadas 2026-10-27)
- README crudo del perfil `Jesus-Valverde/Jesus-Valverde` (2026-10-27)
- anuraghazra/github-readme-stats (README + discusión #4433); DenverCoder1/github-readme-streak-stats; ryo-ma/github-profile-trophy
- Platane/snk (repo y workflow propio); lowlighter/metrics; gautamkrishnar/blog-post-workflow
- tandpfun/skill-icons (issue #1491); syvixor/skills-icons; badges/shields (docs + issue #12162); kyechan99/capsule-render; DenverCoder1/readme-typing-svg
- antonkomarev/github-profile-views-counter (issues #90 y #121); vn7n24fzkq/github-profile-summary-cards; yoshi389111/github-profile-3d-contrib
- VishwaGauravIn/github-profile-readme-maker; abhisheknaiidu/awesome-github-profile-readme
- The Register (17-dic-2025) y changelogs de github.blog (ene-2026, 28-sep-2026) sobre pricing y runners
- Underdog.io, hilo de Glassdoor (jul-2025) y discusión #182100 (dic-2025) — evidencia anecdótica contra-premisa

---
