# Capítulo V: Product Implementation, Validation & Deployment

## 5.1. Software Configuration Management

En esta sección se describen las decisiones, convenciones y herramientas utilizadas por el equipo Inges Company para gestionar el ciclo de vida, la implementación, la validación y el despliegue de **DoofPlus**. Estas decisiones permiten mantener la consistencia y la trazabilidad de los cambios realizados en cada sprint sobre el Website, la Frontend Web Application y los RESTful Web Services.

### 5.1.1. Software Development Environment Configuration

A continuación se detallan los productos de software que los miembros del equipo utilizan para colaborar en el ciclo de vida de DoofPlus, indicando su propósito y su ruta de referencia (productos SaaS) o de descarga (productos que se ejecutan en el computador de cada integrante).

* **Project Management**
    * **Jira Software:** Gestión del Product Backlog, planificación de sprints y seguimiento de tareas en el board del proyecto. (Referencia: https://www.atlassian.com/software/jira)
    * **Discord:** Canal de comunicación del equipo para las reuniones de Sprint Planning, Sprint Review y coordinación diaria. (Referencia: https://discord.com)
* **Requirements Management**
    * **Jira Software:** Registro de User Stories y Technical Stories con sus Story Points y criterios de aceptación. (Referencia: https://www.atlassian.com/software/jira)
    * **Gherkin:** Redacción de criterios de aceptación con la estructura Given-When-Then. (Referencia: https://cucumber.io/docs/gherkin/reference)
    * **Miro:** Elaboración del Big Picture Event Storming y del Design-Level Event Storming. (Referencia: https://miro.com)
* **Product UX/UI Design**
    * **Figma:** Elaboración de Wireframes, Mock-ups y Prototypes del Website y la Web Application. (Referencia: https://www.figma.com)
    * **FigJam:** Elaboración de los Wireflows y User Flows de la Web Application. (Referencia: https://www.figma.com/figjam)
    * **UXPressia:** Elaboración de User Personas, Empathy Maps, Journey Maps e Impact Maps. (Referencia: https://uxpressia.com)
    * **Structurizr DSL:** Elaboración de los diagramas C4 de contexto, contenedores y componentes bajo el enfoque Diagram-as-Code. (Referencia: https://structurizr.com)
    * **Mermaid:** Elaboración de los diagramas de clases y de base de datos bajo el enfoque Diagram-as-Code. (Referencia: https://mermaid.js.org)
* **Software Development**
    * **Git:** Sistema de control de versiones distribuido utilizado en todos los repositorios. (Descarga: https://git-scm.com/downloads)
    * **GitHub:** Plataforma de alojamiento de los repositorios de la organización y de colaboración mediante ramas y Pull Requests. (Referencia: https://github.com/IngesCompany)
    * **WebStorm:** IDE para el desarrollo del Website (HTML5, CSS3 y JavaScript) y de la Frontend Web Application en Angular. (Descarga: https://www.jetbrains.com/webstorm/download)
    * **IntelliJ IDEA:** IDE para el desarrollo de los RESTful Web Services en Java con Spring Boot. (Descarga: https://www.jetbrains.com/idea/download)
    * **Node.js y npm:** Entorno de ejecución y gestor de paquetes requeridos por Angular CLI. (Descarga: https://nodejs.org/en/download)
    * **Angular CLI:** Herramienta para generar, ejecutar y compilar la Frontend Web Application, integrando **Angular Material** como biblioteca de componentes y **ngx-translate** para la internacionalización. (Referencia: https://angular.dev/tools/cli)
    * **Spring Boot y Spring Data JPA:** Frameworks de Java para el desarrollo de los RESTful Web Services. (Referencia: https://spring.io/projects/spring-boot)
    * **MySQL:** Sistema gestor de base de datos relacional (MySQL 8). (Descarga: https://dev.mysql.com/downloads)
* **Software Testing**
    * **Chrome DevTools:** Inspección del diseño responsive y depuración del Website y la Web Application. (Referencia: https://developer.chrome.com/docs/devtools)
    * **json-server:** Fake API para simular los endpoints REST desde la Web Application mientras se implementan los Web Services. (Referencia: https://github.com/typicode/json-server)
    * **Swagger UI:** Ejecución de pruebas sobre los endpoints documentados de los RESTful Web Services. (Referencia: https://swagger.io/tools/swagger-ui)
* **Software Documentation**
    * **Markdown en GitHub:** Redacción del informe del proyecto bajo el enfoque Docs-as-Code en el repositorio del informe. (Referencia: https://www.markdownguide.org)
    * **OpenAPI (Swagger):** Documentación de los RESTful Web Services. (Referencia: https://swagger.io/specification)
* **Software Deployment**
    * **GitHub Pages:** Publicación del Website. (Referencia: https://pages.github.com)
    * **Firebase Hosting:** Publicación de la Frontend Web Application. (Referencia: https://firebase.google.com/docs/hosting)
    * **Render:** Publicación de los RESTful Web Services. (Referencia: https://render.com)
    * **Railway:** Base de datos MySQL gestionada en la nube. (Referencia: https://railway.com)

### 5.1.2. Source Code Management

El equipo utiliza **GitHub** como plataforma y **Git** como sistema de control de versiones. Todos los repositorios pertenecen a la organización IngesCompany: https://github.com/IngesCompany:

| Producto | Repositorio |
|----------|-------------|
| Website | https://github.com/IngesCompany/doofplus-website |
| Frontend Web Application | https://github.com/IngesCompany/doofplus-web-application |
| RESTful Web Services | https://github.com/IngesCompany/doofplus-platform |
| Informe del proyecto | https://github.com/IngesCompany/doofplus-report |

**GitFlow Workflow**

El equipo aplica el modelo GitFlow propuesto por Vincent Driessen en *A successful Git branching model*:

* **`main`:** Contiene únicamente versiones estables listas para producción. Solo recibe merges desde ramas `release/*` y `hotfix/*`, y cada merge se etiqueta con su versión (por ejemplo, `v1.0.0`).
* **`develop`:** Rama de integración. Consolida las funcionalidades terminadas antes de preparar una nueva versión.
* **Feature branches:** Nacen de `develop` y regresan a `develop` mediante Pull Request. Convención: `feature/<nombre-en-kebab-case>`, nombrando el bounded context o la funcionalidad (por ejemplo, `feature/shared`, `feature/manufacturing`, `feature/project-configuration`). En el repositorio del informe se usa `feature/chapter<n>`.
* **Release branches:** Nacen de `develop` cuando un incremento está listo para entregarse y se fusionan con `main` y `develop`. Convención: `release/v<MAJOR>.<MINOR>.<PATCH>`, admitiendo el sufijo de pre-release `-rc.<n>` (por ejemplo, `release/v1.0.0-rc.1`, usada en el Website).
* **Hotfix branches:** Nacen de `main` para corregir errores críticos en producción y se fusionan con `main` y `develop`. Convención: `hotfix/v<MAJOR>.<MINOR>.<PATCH>` (por ejemplo, `hotfix/v1.0.1`).

**Semantic Versioning**

Las releases se nombran según **Semantic Versioning 2.0.0** con el formato `MAJOR.MINOR.PATCH`:

* **MAJOR:** Cambios incompatibles con versiones anteriores (por ejemplo, `v2.0.0`).
* **MINOR:** Nuevas funcionalidades compatibles con la versión anterior (por ejemplo, `v1.1.0`).
* **PATCH:** Correcciones de errores compatibles (por ejemplo, `v1.0.1`).

**Conventional Commits**

Los mensajes de commit siguen la especificación **Conventional Commits 1.0.0**:

```
<type>(<optional scope>): <description>

<optional body>

<optional footer(s)>
```

* **type:** `feat` (nueva funcionalidad), `fix` (corrección de errores), `docs` (documentación), `style` (formato sin cambios de lógica), `refactor` (reestructuración sin cambio de comportamiento), `test` (pruebas), `build` (sistema de build o dependencias), `ci` (integración continua), `chore` (tareas de mantenimiento).
* **scope:** Módulo o bounded context afectado, por ejemplo `feat(lots): ...` o `docs(chapter5): ...`.
* **description:** Resumen breve en inglés, en modo imperativo y en minúsculas.
* **body y footer:** Detalle del cambio y referencias a tareas; los cambios incompatibles se marcan con `BREAKING CHANGE:` o con `!` después del type.

### 5.1.3. Source Code Style Guide & Coding Conventions

Toda la nomenclatura del código fuente (archivos, clases, variables, métodos y comentarios) se escribe en **inglés**, respetando el Ubiquitous Language del dominio de calidad farmacéutica (por ejemplo, `ProductionBatch`, `Deviation`, `CapaAction`). Las convenciones adoptadas por lenguaje son las siguientes:

* **HTML:** HTML Style Guide and Coding Conventions (W3Schools): https://www.w3schools.com/html/html5_syntax.asp y Google HTML/CSS Style Guide: https://google.github.io/styleguide/htmlcssguide.html. Etiquetas y atributos en minúsculas, valores de atributos entre comillas dobles, uso de etiquetas semánticas (`header`, `main`, `section`, `footer`) y atributo `alt` en todas las imágenes.
* **CSS:** Google HTML/CSS Style Guide: https://google.github.io/styleguide/htmlcssguide.html. Indentación de 2 espacios, nombres de clases en kebab-case y selectores cortos; los ids no se usan para estilos.
* **JavaScript:** Google JavaScript Style Guide: https://google.github.io/styleguide/jsguide.html. Uso de `const`/`let`, lowerCamelCase para variables y funciones y punto y coma al final de cada sentencia.
* **TypeScript:** Google TypeScript Style Guide: https://google.github.io/styleguide/tsguide.html. UpperCamelCase para clases e interfaces, lowerCamelCase para propiedades y métodos, tipado explícito y sin uso de `any`.
* **Angular:** Angular coding style guide: https://angular.dev/style-guide. Nombres de archivos en kebab-case, un componente por archivo, selectores con el prefijo `app-`, inyección de dependencias en servicios y organización del código por bounded context (`domain`, `infrastructure`, `application`, `presentation`).
* **Java:** Google Java Style Guide: https://google.github.io/styleguide/javaguide.html. UpperCamelCase para clases, lowerCamelCase para métodos y variables, CONSTANT_CASE para constantes y llaves obligatorias en todas las estructuras de control.
* **Spring Boot:** Spring Boot Features: https://docs.spring.io/spring-boot/reference/features/index.html. Clase principal en el paquete raíz, configuración externalizada en `application.properties` y variables de entorno, y controladores RESTful con rutas en plural y kebab-case (por ejemplo, `/api/v1/production-batches`).
* **Gherkin:** Gherkin Conventions for Readable Specifications: https://specflow.org/gherkin/gherkin-conventions-for-readable-specifications. Palabras clave `Feature`, `Scenario`, `Given`, `When`, `Then` en inglés, un comportamiento por escenario y uso de `Scenario Outline` con `Examples` para casos basados en datos.

### 5.1.4. Software Deployment Configuration

A continuación se describen los pasos para desplegar cada producto de la solución a partir de su repositorio de código fuente:

1. **Website (GitHub Pages)**
    1. Fusionar la rama en `main` y etiquetar la versión.
    2. En el repositorio `doofplus-website`, ingresar a *Settings > Pages* y seleccionar *GitHub Actions* como origen. El workflow `.github/workflows/deploy.yml` publica la carpeta `public`, que contiene el sitio estático, y el archivo `.nojekyll` indica a GitHub Pages que publique los archivos sin procesarlos con Jekyll.
    3. GitHub Pages publica el sitio en https://ingescompany.github.io/doofplus-website/ y el workflow lo vuelve a publicar con cada push a `main`.
2. **Frontend Web Application (Firebase Hosting)**
    1. Instalar Firebase CLI (`npm install -g firebase-tools`) e iniciar sesión con `firebase login`.
    2. Seleccionar el proyecto de Firebase con `firebase use --add`. El repositorio ya incluye `firebase.json`, que publica la carpeta `dist/IngesCompany-Frontend/browser` como Single Page Application.
    3. Registrar en `src/environments/environment.ts` la URL base de los RESTful Web Services publicados (`platformProviderApiBaseUrl`, https://doofplus-platform.onrender.com/api/v1). Desde la versión `v1.4.0`, todos los bounded contexts usan ese API y la Web Application ya no necesita la Fake API.
    4. Compilar la versión de producción con `ng build --configuration production`.
    5. Publicar con `firebase deploy`.
3. **RESTful Web Services (Render y Railway)**
    1. Crear la base de datos MySQL en Railway y obtener la URL de conexión y las credenciales.
    2. Crear un Web Service en Render vinculado a la rama `main` del repositorio de Web Services, con el Dockerfile del proyecto Spring Boot.
    3. Registrar en Render las variables de entorno de producción (URL y credenciales de la base de datos, secreto JWT, credenciales de la pasarela de pagos Niubiz, API key de SendGrid y API key de los dispositivos de ThingsBoard).
    4. Render compila y publica el servicio con cada push a `main`; la documentación OpenAPI queda disponible en la ruta `/swagger-ui/index.html` del servicio.

## 5.2. Landing Page, Services & Applications Implementation

En esta sección se explica y evidencia el proceso de implementación, pruebas, documentación y despliegue de **DoofPlus**, incluyendo el Website, la Frontend Web Application y los RESTful Web Services. El avance se presenta organizado por Sprints a partir del Product Backlog.

### 5.2.1. Sprint 1

En esta sección se registra y explica el avance en términos de producto y trabajo colaborativo para el **Sprint 1**, cuyo enfoque principal fue la construcción y el despliegue de la primera versión del Website de DoofPlus, así como la configuración inicial de los repositorios.

#### 5.2.1.1. Sprint Planning 1

El Sprint Planning Meeting sirvió para definir los objetivos iniciales, asignar responsabilidades y seleccionar las User Stories prioritarias orientadas a la presentación comercial de DoofPlus. A continuación, se presenta el resumen de la reunión de planificación:

| Sprint # | Sprint 1 |
|----------|----------|
| **Sprint Planning Background** | |
| **Date** | 2026-09-20 |
| **Time** | 10:00 AM |
| **Location** | Reunión virtual vía Discord |
| **Prepared By** | Cobades Zamora, Yhoshua Hebert |
| **Attendees (to planning meeting)** | Angulo Ramírez, Marcelo Martín / Cobades Zamora, Yhoshua Hebert / Flores Martinez, Ricardo Andres / Rojas Ambicho, Nestor Daniel / Zavaleta Gutierrez, Rodolfo Martin |
| **Sprint 0 Review Summary** | No aplica por ser el primer Sprint del proyecto. |
| **Sprint 0 Retrospective Summary** | No aplica por ser el primer Sprint del proyecto. |
| **Sprint Goal & User Stories** | |
| **Sprint 1 Goal** | **Our focus is on** QA/QC specialists and production supervisors of small and medium-sized pharmaceutical laboratories being able to learn, from a bilingual website, how DoofPlus centralizes their quality records and batch traceability, compare its subscription plans and contact the team.<br>**We believe it delivers** a clear understanding of how DoofPlus replaces paper forms and spreadsheets and shortens audit preparation, so they can decide to evaluate the platform, **to** QA/QC specialists and production supervisors.<br>**This will be confirmed when** a visitor from each segment, on desktop or mobile and in English or Spanish, identifies the features for their role, compares the two plans and sends an inquiry through the contact form. |
| **Sprint 1 Velocity** | 16 Story Points |
| **Sum of Story Points** | 13 Story Points (US44: 3, US03: 2, US45: 1, US04: 1, US46: 5, US47: 1) |

#### 5.2.1.2. Aspect Leaders and Collaborators

En el Sprint 1 se consideraron cuatro aspectos: el diseño del Website, su implementación, la configuración de repositorios y despliegue, y la documentación del sprint. A continuación se presenta el Leadership-and-Collaboration Matrix (LACX), que indica quién es el líder (L) y quiénes son los colaboradores (C) en cada aspecto:

| Team Member (Last Name, First Name) | GitHub Username | Website UI/UX | Website Implementation | Repositories & Deployment | Documentation |
|-------------------------------------|-----------------|:------------------:|:---------------------------:|:-------------------------:|:-------------:|
| Angulo Ramírez, Marcelo Martín | Zock2005 | L | C | | C |
| Cobades Zamora, Yhoshua Hebert | YhoshuaCZ | C | C | L | C |
| Flores Martinez, Ricardo Andres | Nitoryu28 / Nitoryu2801 | C | C | | C |
| Rojas Ambicho, Nestor Daniel | danRO-20 | C | C | | |
| Zavaleta Gutierrez, Rodolfo Martin | gutierrezrodolfo360-bit | C | L | C | L |

#### 5.2.1.3. Sprint Backlog 1

El objetivo principal de este Sprint fue implementar y publicar el Website de DoofPlus para dar a conocer a Inges Company y su propuesta de valor. La siguiente imagen muestra las User Stories del Sprint 1 en Jira, ya cerrado:

![Sprint Backlog 1 en Jira](assets/img/chapter5/evidencia/jira-pb.png)

*Figura: User Stories del Sprint 1 en Jira Software.*

**Enlace al board en Jira:** https://doofplus.atlassian.net/jira/software/projects/UPC/boards/3

| Sprint # | Sprint 1 | | | | | | |
|----------|----------|---|---|---|---|---|---|
| **User Story** | | **Work-Item / Task** | | | | | |
| **Id** | **Title** | **Id** | **Title** | **Description** | **Estimation (Hours)** | **Assigned To** | **Status (To-do / In-Process / To-Review / Done)** |
| US44 | Navegación por secciones | T001 | Implementar navbar responsivo | Estructurar el menú de navegación con los enlaces a Home, Features, Benefits, Plans y Contact. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US44 | Navegación por secciones | T002 | Estilos y menú hamburguesa | Aplicar estilos CSS al menú y añadir el comportamiento responsive con menú hamburguesa para móvil. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US03 | Visualización de planes y precios | T003 | Diseñar tarjetas de planes | Crear las tarjetas de los planes Standard Lab (US$199/mes) y Enterprise (US$599/mes) con sus características. | 3 | Flores Martinez, Ricardo Andres | Done |
| US03 | Visualización de planes y precios | T004 | Toggle mensual/anual | Implementar el cambio entre precios mensuales y anuales con un ahorro equivalente a dos meses (≈17%). | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US45 | Visualización del equipo y de la startup | T005 | Maquetar sección Our Team | Implementar las tarjetas de los 5 integrantes del equipo Inges Company con foto, nombre y descripción. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US45 | Visualización del equipo y de la startup | T006 | Correcciones sección Our Team | Corregir la estructura y el contenido de la sección del equipo tras la revisión de pares. | 1 | Angulo Ramírez, Marcelo Martín | Done |
| US04 | Formulario de contacto | T007 | Footer con datos de contacto | Desarrollar el footer con los datos de contacto y los enlaces legales. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US04 | Formulario de contacto | T008 | Formulario de suscripción por email | Implementar el formulario de suscripción por email con la validación del correo. | 1 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US44 | Navegación por secciones | T009 | Estructura semántica de index | Corregir la estructura general de `index.html` con etiquetas semánticas (header, main, section y footer). | 1 | Flores Martinez, Ricardo Andres | Done |
| US44 | Navegación por secciones | T010 | Revisión de accesibilidad | Revisar los textos alternativos, los atributos aria y el contraste de colores del Website. | 1 | Flores Martinez, Ricardo Andres | Done |
| US46 | Cambio de idioma | T011 | Archivos de traducción ES/EN | Crear los archivos de traducción en.json y es.json con los textos de cada sección. | 1 | Cobades Zamora, Yhoshua Hebert | Done |
| US46 | Cambio de idioma | T012 | Selector de idioma e i18n | Implementar el selector de idioma ES/EN y la lógica JavaScript que aplica las traducciones. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US47 | Consulta de términos y política de privacidad | T013 | Agregar Terms of Service | Redactar e implementar la página de Términos de Servicio de DoofPlus. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US47 | Consulta de términos y política de privacidad | T014 | Agregar Privacy Policy | Redactar e implementar la Política de Privacidad conforme a la Ley N.° 29733. | 2 | Angulo Ramírez, Marcelo Martín | Done |

#### 5.2.1.4. Development Evidence for Sprint Review

Durante el Sprint 1 se implementó el Website con HTML5, CSS3 y JavaScript: estructura semántica de las secciones, hoja de estilos responsive, recursos gráficos, footer con formulario de contacto y cambio de idioma ES/EN mediante archivos de traducción. La versión estable se integró a `main` a través de la rama `release/v1.0.0-rc.1`. La siguiente tabla presenta los commits del repositorio:

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/doofplus-website | main | `b93c547` | fix: refactor index.html | Refactorización de la estructura de `index.html`. | 20/09/2026 |
| IngesCompany/doofplus-website | main | `1f1a22f` | Merge branch 'release/v1.0.0-rc.1' into main | Integración de la rama de release a producción. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `e530153` | fix: change the defect language | Corrección del idioma predeterminado. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `7eded14` | build: add the option to change the language in main.js | Lógica para alternar idiomas en el script principal. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `432fb64` | fix: update links of the images in index.html | Actualización de las rutas de las imágenes. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `46b51b6` | build: add styles | Incorporación de la hoja de estilos CSS. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `86d4578` | chore: add images | Inclusión de los recursos gráficos del sitio. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `06bd5ef` | build: Add footer | Creación de la sección del pie de página. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `be8e428` | build: add body | Estructura y contenido del cuerpo principal. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `9b082a5` | feat: add language switching functionality in main.js | Funcionalidad de cambio de idioma. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `b9ff9e6` | ci: add translations | Archivos de traducción ES/EN. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `6a1377f` | docs: update README.md | Actualización de la documentación del repositorio. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `0de92b6` | fix: refactor README.md | Corrección del formato del README. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `6e6efc0` | docs: add README.md | Creación del README del repositorio. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `8dca66b` | Merge remote-tracking branch 'origin/develop' into develop | Sincronización de la rama `develop`. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `a8c7448` | chore: Create template | Creación de la plantilla base del proyecto. | 20/09/2026 |
| IngesCompany/doofplus-website | develop | `e68b54e` | feat: init commit | Commit inicial del repositorio. | 20/09/2026 |

#### 5.2.1.5. Execution Evidence for Sprint Review

En este Sprint se logró un Website funcional, responsive y bilingüe (español e inglés), con navegación por secciones, propuesta de valor, características, planes y precios con toggle mensual/anual, sección del equipo, formulario de contacto y páginas de Términos de Servicio y Política de Privacidad. A continuación se presentan las capturas de las principales secciones implementadas:

![Website - Parte 1](assets/img/chapter5/screenshots/1.png)

![Website - Parte 2](assets/img/chapter5/screenshots/2.png)

![Website - Parte 3](assets/img/chapter5/screenshots/3.png)

![Website - Parte 4](assets/img/chapter5/screenshots/4.png)

![Website - Parte 5](assets/img/chapter5/screenshots/5.png)

![Website - Parte 6](assets/img/chapter5/screenshots/6.png)

![Website - Parte 7](assets/img/chapter5/screenshots/7.png)

![Website - Parte 8](assets/img/chapter5/screenshots/8.png)

![Website - Parte 9](assets/img/chapter5/screenshots/9.png)

![Website - Parte 10](assets/img/chapter5/screenshots/10.png)

![Website - Parte 11](assets/img/chapter5/screenshots/11.png)

**Website desplegado:** https://ingescompany.github.io/doofplus-website/

Video de navegación del producto: upc-pre-202620-1asi0729-7742-IngesCompany-productnavigation-sprint-1 (duración: 3:03), ver en Microsoft Stream: https://shorturl.at/ezIzk. Muestra la navegación del Website, el único producto del Sprint 1.

#### 5.2.1.6. Services Documentation Evidence for Sprint Review

El alcance del Sprint 1 se limitó al Website, por lo que no se implementaron ni documentaron endpoints. La documentación de los RESTful Web Services con OpenAPI se elaborará en el sprint en que se implementen dichos servicios.

#### 5.2.1.7. Software Deployment Evidence for Sprint Review

Durante este Sprint, el equipo publicó el Website en **GitHub Pages**. Para ello se configuró, en *Settings > Pages* del repositorio `doofplus-website`, la publicación desde la rama `main` y la carpeta raíz, de modo que cada cambio integrado en `main` se publica automáticamente.

![Configuración de GitHub Pages](assets/img/chapter5/evidencia/github-pages.png)

*Figura: Configuración de GitHub Pages en el repositorio del Website.*

![Website publicado](assets/img/chapter5/evidencia/pages.png)

*Figura: Website publicado en GitHub Pages.*

#### 5.2.1.8. Team Collaboration Insights during Sprint

Todos los miembros del equipo participaron en la implementación del Website. Los cambios se integraron en la rama `develop` y, desde ella, se preparó la rama `release/v1.0.0-rc.1`, que se fusionó con `main` para su publicación. La siguiente imagen muestra los analíticos de commits del repositorio en GitHub:

![Insights del repositorio del Website](assets/img/chapter5/evidencia/evidencia.png)

*Figura: Analíticos de colaboración del repositorio del Website en GitHub.*

### 5.2.2. Sprint 2

En esta sección se registra y explica el avance en términos de producto y trabajo colaborativo para el **Sprint 2**, cuyo enfoque fue completar el Website de DoofPlus y construir la primera versión de la Frontend Web Application con sus seis bounded contexts, consumiendo una Fake API mientras se implementan los RESTful Web Services.

#### 5.2.2.1. Sprint Planning 2

El Sprint Planning Meeting sirvió para definir los objetivos del Sprint, asignar responsabilidades por bounded context y seleccionar las User Stories pendientes del Website y las de la Web Application. A continuación, se presenta el resumen de la reunión de planificación:

| Sprint # | Sprint 2 |
|----------|----------|
| **Sprint Planning Background** | |
| **Date** | 2026-10-02 |
| **Time** | 09:00 AM |
| **Location** | Reunión virtual vía Discord |
| **Prepared By** | Cobades Zamora, Yhoshua Hebert |
| **Attendees (to planning meeting)** | Angulo Ramírez, Marcelo Martín / Cobades Zamora, Yhoshua Hebert / Flores Martinez, Ricardo Andres / Rojas Ambicho, Nestor Daniel / Zavaleta Gutierrez, Rodolfo Martin |
| **Sprint 1 Review Summary** | Se entregó la primera versión del Website de DoofPlus publicada en GitHub Pages, con navegación por secciones, planes y precios, sección del equipo, formulario de contacto, cambio de idioma ES/EN y páginas legales. Como feedback, se pidió que el formulario de contacto sirva para enviar consultas sobre la plataforma y sus planes, y alinear el Website con los mock-ups del capítulo 4. |
| **Sprint 1 Retrospective Summary** | Como acierto, el equipo integró la versión estable mediante una rama de release siguiendo GitFlow. Como oportunidades de mejora, se acordó trabajar en feature branches que nazcan de `develop`, una por sección o bounded context, distribuir los commits a lo largo del sprint y usar los types de Conventional Commits según su significado. |
| **Sprint Goal & User Stories** | |
| **Sprint 2 Goal** | **Our focus is on** QA/QC specialists and production supervisors being able to manage, in a single web platform, the life cycle of a batch: register production orders and batches, receive raw materials, monitor equipment readings, record deviations and CAPA, and release batches with an electronic signature.<br>**We believe it delivers** complete batch traceability and audit-ready records without paper forms or spreadsheets, together with a website that guides new laboratories to the platform, **to** QA/QC specialists and production supervisors of small and medium-sized pharmaceutical laboratories.<br>**This will be confirmed when** a QA/QC specialist and a production supervisor sign in to their own environment, follow a batch from its creation to its release with an electronic signature and retrieve its complete history in a single view. |
| **Sprint 2 Velocity** | 177 Story Points |
| **Sum of Story Points** | 177 Story Points (US01: 2, US02: 2, US48: 2, US49: 2, US05: 1, US06: 2, US07: 3, US08: 5, US55: 3, US50: 3, US51: 3, US52: 5, US53: 3, US35: 3, US36: 5, US57: 3, US14: 3, US15: 5, US16: 2, US58: 3, US17: 3, US32: 3, US23: 3, US24: 3, US25: 5, US26: 3, US37: 3, US38: 3, US39: 3, US56: 3, US22: 2, US09: 5, US10: 3, US12: 5, US13: 3, US18: 3, US19: 5, US20: 5, US21: 3, US11: 5, US54: 5, US31: 3, US27: 5, US28: 5, US29: 5, US30: 3, US59: 3, US33: 3, US34: 3, US40: 3, US41: 3, US42: 2, US43: 3) |

#### 5.2.2.2. Aspect Leaders and Collaborators

En el Sprint 2 se consideraron ocho aspectos: el Website y, en la Web Application, los bounded contexts (Shared e IAM; Organizations y Subscriptions; Manufacturing; IoT Monitoring; Quality & Compliance), las releases y el despliegue, y la documentación. El líder (L) de cada aspecto es el integrante con más commits en él, según el historial de los repositorios.

| Team Member (Last Name, First Name) | GitHub Username | Website | Shared & IAM | Organizations & Subscriptions | Manufacturing | IoT Monitoring | Quality & Compliance | Releases & Deployment | Documentation |
|-------------------------------------|-----------------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Angulo Ramírez, Marcelo Martín | Zock2005 | C | C | | | L | | | C |
| Cobades Zamora, Yhoshua Hebert | YhoshuaCZ | C | L | | L | | L | C | C |
| Flores Martinez, Ricardo Andres | Nitoryu28 | C | | | C | | C | | |
| Rojas Ambicho, Nestor Daniel | danRO-20 | L | | L | | C | | L | C |
| Zavaleta Gutierrez, Rodolfo Martin | gutierrezrodolfo360-bit | C | C | | C | | C | C | L |

#### 5.2.2.3. Sprint Backlog 2

El objetivo del Sprint fue completar el Website y entregar la primera versión de la Web Application. Las tareas se organizaron por User Story; las del Website incluyen la reimplementación de las secciones del Sprint 1 sobre el diseño del capítulo 4. La siguiente imagen muestra el board del Sprint 2 en Jira:

![Sprint Backlog 2 en Jira](assets/img/chapter5/evidencia/jira-pb2.png)

*Figura: Board del Sprint 2 en Jira Software.*

**Enlace al board en Jira:** https://doofplus.atlassian.net/jira/software/projects/UPC/boards/3

| Sprint # | Sprint 2 | | | | | | |
|----------|----------|---|---|---|---|---|---|
| **User Story** | | **Work-Item / Task** | | | | | |
| **Id** | **Title** | **Id** | **Title** | **Description** | **Estimation (Hours)** | **Assigned To** | **Status (To-do / In-Process / To-Review / Done)** |
| US01 | Visualización de la propuesta de valor | T015 | Hero con propuesta de valor | Implementar el hero con el título, el subtítulo, los indicadores de confianza y los botones Get Started y View plans. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US01 | Visualización de la propuesta de valor | T016 | Hero con propuesta de valor: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US02 | Visualización de servicios y características | T017 | Sección Services | Implementar las tarjetas de servicios con sus estilos y sus textos en en.json y es.json. | 2 | Flores Martinez, Ricardo Andres | Done |
| US02 | Visualización de servicios y características | T018 | Sección Features | Implementar el acordeón de características con su panel de vista previa, sus estilos y sus textos en en.json y es.json. | 1 | Cobades Zamora, Yhoshua Hebert | Done |
| US48 | Acceso por segmento a la Web Application | T019 | Acceso por segmento | Implementar la sección Choose your workspace y los enlaces con data-app-segment hacia el inicio de sesión de cada entorno. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US48 | Acceso por segmento a la Web Application | T020 | Acceso por segmento: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US49 | Visualización del video promocional | T021 | Sección About the Product con video | Implementar la sección del video del producto con su reproductor, sus estilos y sus textos en en.json y es.json. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US49 | Visualización del video promocional | T022 | Carga del video y video About the Team | Cargar el video de YouTube al pulsar play y agregar el video About the Team debajo de las tarjetas del equipo. | 1 | Rojas Ambicho, Nestor Daniel | Done |
| US05 | Preguntas frecuentes | T023 | Sección FAQ | Implementar las preguntas frecuentes con acordeón accesible y el enlace al formulario de contacto. | 1 | Rojas Ambicho, Nestor Daniel | Done |
| US05 | Preguntas frecuentes | T024 | Sección FAQ: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Rojas Ambicho, Nestor Daniel | Done |
| US44 | Navegación por secciones | T025 | Navbar con menú móvil | Reimplementar la barra de navegación con anclas reales, Sign in y Get Started con destino propio y el menú overlay en mobile. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US44 | Navegación por secciones | T026 | Navbar con menú móvil: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US03 | Visualización de planes y precios | T027 | Planes con toggle mensual/anual | Reimplementar las tarjetas de planes con el cambio de precio mensual/anual y su nota de precios. | 2 | Flores Martinez, Ricardo Andres | Done |
| US03 | Visualización de planes y precios | T028 | Planes con toggle mensual/anual: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Flores Martinez, Ricardo Andres | Done |
| US45 | Visualización del equipo y de la startup | T029 | Secciones About us y Our Team | Implementar la misión, la visión y las tarjetas de los integrantes con su foto y rol. | 1 | Rojas Ambicho, Nestor Daniel | Done |
| US45 | Visualización del equipo y de la startup | T030 | Secciones About us y Our Team: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Rojas Ambicho, Nestor Daniel | Done |
| US04 | Formulario de contacto | T031 | Formulario Contact us | Implementar el formulario de consulta con validación de campos y el estado de mensaje enviado. | 1 | Cobades Zamora, Yhoshua Hebert | Done |
| US04 | Formulario de contacto | T032 | Formulario Contact us: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Cobades Zamora, Yhoshua Hebert | Done |
| US47 | Consulta de términos y política de privacidad | T033 | Términos y política de privacidad | Implementar las páginas terms.html y privacy.html con sus estilos y traducciones. | 1 | Angulo Ramírez, Marcelo Martín | Done |
| US47 | Consulta de términos y política de privacidad | T034 | Términos y política de privacidad: estilos y traducciones | Aplicar los estilos responsive de la sección y agregar sus textos en en.json y es.json. | 1 | Angulo Ramírez, Marcelo Martín | Done |
| US06 | Inicio de sesión con segundo factor | T035 | Inicio de sesión con 2FA: vista | Implementar la elección de entorno, el inicio de sesión por entorno y la verificación con código de seis dígitos. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US06 | Inicio de sesión con segundo factor | T036 | Inicio de sesión con 2FA: store y Fake API | Agregar al store de IAM las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 1 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US07 | Gestión de roles | T037 | Acceso por rol: vista | Implementar el guard de IAM y el estado Access not authorized cuando el rol no corresponde al entorno. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US07 | Gestión de roles | T038 | Acceso por rol: store y Fake API | Agregar al store de IAM las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US08 | Firmas electrónicas | T039 | Firma electrónica: vista | Implementar la confirmación con contraseña en las aprobaciones, liberaciones y cierres críticos. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US08 | Firmas electrónicas | T040 | Firma electrónica: store y Fake API | Agregar al store de IAM las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US55 | Alta de usuarios del equipo | T041 | Usuarios e invitaciones: vista | Implementar el directorio de usuarios y perfiles y el formulario para invitar usuarios. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US55 | Alta de usuarios del equipo | T042 | Usuarios e invitaciones: store y Fake API | Agregar al store de IAM las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US50 | Registro de organización | T043 | Registro de organización: vista | Implementar el registro con razón social, RUC, planta, plan y primer administrador, y el resumen de administración. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US50 | Registro de organización | T044 | Registro de organización: store y Fake API | Agregar al store de Organizations las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US51 | Selección de plan | T045 | Selección de plan: vista | Implementar la revisión del cambio de plan en la página de suscripción. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US51 | Selección de plan | T046 | Selección de plan: store y Fake API | Agregar al store de Subscriptions las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US52 | Pago de suscripción | T047 | Pago de suscripción: vista | Implementar el historial de facturación y el reintento de un pago rechazado. | 3 | Rojas Ambicho, Nestor Daniel | Done |
| US52 | Pago de suscripción | T048 | Pago de suscripción: store y Fake API | Agregar al store de Subscriptions las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Rojas Ambicho, Nestor Daniel | Done |
| US53 | Renovación y cancelación | T049 | Renovación de la suscripción: vista | Mostrar la fecha de renovación y el estado de la suscripción en la página de suscripción y pagos. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US53 | Renovación y cancelación | T050 | Renovación de la suscripción: store y Fake API | Agregar al store de Subscriptions las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US35 | Catálogo de productos | T051 | Catálogo de productos: vista | Implementar el catálogo de productos con su fórmula maestra vigente. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US35 | Catálogo de productos | T052 | Catálogo de productos: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US36 | Gestión de fórmulas maestras | T053 | Fórmulas maestras: vista | Mostrar los componentes y la versión aprobada de la fórmula maestra de cada producto. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US36 | Gestión de fórmulas maestras | T054 | Fórmulas maestras: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US57 | Gestión de órdenes de producción | T055 | Órdenes de producción: vista | Implementar la lista y la ejecución de órdenes de producción contra la fórmula maestra. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US57 | Gestión de órdenes de producción | T056 | Órdenes de producción: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US14 | Registro de lotes | T057 | Registro de lotes: vista | Implementar el diálogo Create batch con el estado de lote rechazado por fórmula no aprobada. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US14 | Registro de lotes | T058 | Registro de lotes: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US15 | Consulta del historial de lotes | T059 | Historial de lotes: vista | Implementar la lista de lotes con filtros y la genealogía y el historial de estados de cada lote. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US15 | Consulta del historial de lotes | T060 | Historial de lotes: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US16 | Gestión de estados de lote | T061 | Estados de lote: vista | Implementar el cambio de estado de los lotes y sus conteos por estado. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US16 | Gestión de estados de lote | T062 | Estados de lote: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 1 | Cobades Zamora, Yhoshua Hebert | Done |
| US58 | Recepción de materias primas | T063 | Recepción de materias primas: vista | Implementar la recepción de materias primas con cuarentena e inspección. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US58 | Recepción de materias primas | T064 | Recepción de materias primas: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US17 | Asociación de materias primas | T065 | Asociación de materias primas: vista | Asignar lotes de materia prima aprobados a un lote de producción. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US17 | Asociación de materias primas | T066 | Asociación de materias primas: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US32 | Panel de producción | T067 | Resumen de producción: vista | Implementar el resumen de producción con el programa del día, la disponibilidad de equipos y las incidencias. | 2 | Flores Martinez, Ricardo Andres | Done |
| US32 | Panel de producción | T068 | Resumen de producción: store y Fake API | Agregar al store de Manufacturing las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Flores Martinez, Ricardo Andres | Done |
| US23 | Registro de dispositivos IoT | T069 | Inventario de equipos y sensores: vista | Implementar el inventario de equipos con sus sensores IoT y el registro de un sensor. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US23 | Registro de dispositivos IoT | T070 | Inventario de equipos y sensores: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US24 | Asociación de sensores a un lote | T071 | Asociación de sensores a lotes: vista | Implementar la evidencia IoT del lote con la asociación de equipos y sensores. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US24 | Asociación de sensores a un lote | T072 | Asociación de sensores a lotes: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US25 | Captura automática de evidencias | T073 | Telemetría: vista | Implementar el gráfico de telemetría con límites y lectura pico. | 3 | Angulo Ramírez, Marcelo Martín | Done |
| US25 | Captura automática de evidencias | T074 | Telemetría: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Angulo Ramírez, Marcelo Martín | Done |
| US26 | Consulta de registros IoT | T075 | Consulta de registros IoT: vista | Implementar el resumen IoT con la salud de los equipos y la cola de alertas. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US26 | Consulta de registros IoT | T076 | Consulta de registros IoT: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US37 | Gestión de equipos | T077 | Gestión de equipos: vista | Mostrar el estado operativo de cada equipo en el inventario. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US37 | Gestión de equipos | T078 | Gestión de equipos: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US38 | Gestión de calibraciones | T079 | Calibraciones: vista | Mostrar el estado de calibración (apto, por vencer, no apto) de equipos y sensores. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US38 | Gestión de calibraciones | T080 | Calibraciones: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US39 | Mantenimiento preventivo | T081 | Mantenimiento preventivo: vista | Mostrar el próximo mantenimiento y su responsable en el detalle del equipo. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US39 | Mantenimiento preventivo | T082 | Mantenimiento preventivo: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US56 | Registro y escalamiento de incidencias | T083 | Incidentes: vista | Implementar la lista de incidentes con su severidad y el reconocimiento de alertas. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US56 | Registro y escalamiento de incidencias | T084 | Incidentes: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US22 | Notificaciones de desviación crítica | T085 | Alertas críticas: vista | Implementar el detalle del sensor con la alerta activa y la regla de reconocimiento. | 2 | Angulo Ramírez, Marcelo Martín | Done |
| US22 | Notificaciones de desviación crítica | T086 | Alertas críticas: store y Fake API | Agregar al store de IoT Monitoring las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 1 | Angulo Ramírez, Marcelo Martín | Done |
| US09 | Gestión de protocolos de calidad | T087 | Documentos de calidad: vista | Implementar el repositorio de documentos controlados con su flujo de aprobación. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US09 | Gestión de protocolos de calidad | T088 | Documentos de calidad: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US10 | Repositorio de SOP | T089 | Repositorio de SOP: vista | Filtrar los documentos por tipo y estado para consultar la versión vigente. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US10 | Repositorio de SOP | T090 | Repositorio de SOP: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US12 | Control de versiones documentales | T091 | Versiones de documentos: vista | Implementar el historial de versiones de cada documento. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US12 | Control de versiones documentales | T092 | Versiones de documentos: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US13 | Aprobación documental | T093 | Aprobación documental: vista | Implementar la aprobación con firma y el bloqueo de autoaprobación (segregación de funciones). | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US13 | Aprobación documental | T094 | Aprobación documental: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US18 | Registro de desviaciones | T095 | Registro de desviaciones: vista | Implementar el reporte de desviación con su evaluación de riesgo. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US18 | Registro de desviaciones | T096 | Registro de desviaciones: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US19 | Análisis de causa raíz | T097 | Análisis de causa raíz: vista | Implementar el registro de la causa raíz como requisito del plan CAPA. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US19 | Análisis de causa raíz | T098 | Análisis de causa raíz: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US20 | Gestión CAPA | T099 | Plan CAPA: vista | Implementar el plan CAPA con sus acciones, responsables y fechas. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US20 | Gestión CAPA | T100 | Plan CAPA: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US21 | Seguimiento de acciones CAPA | T101 | Seguimiento de CAPA: vista | Mostrar el avance de las acciones CAPA y bloquear el cierre sin evidencia de eficacia. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US21 | Seguimiento de acciones CAPA | T102 | Seguimiento de CAPA: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US11 | Automatización de cálculos de calidad | T103 | Resultados analíticos: vista | Implementar los resultados analíticos con su conformidad respecto de la especificación. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US11 | Automatización de cálculos de calidad | T104 | Resultados analíticos: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US54 | Revisión y liberación de lotes | T105 | Liberación de lotes: vista | Implementar la liberación de lotes con requisitos previos, firma electrónica y estado bloqueado. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US54 | Revisión y liberación de lotes | T106 | Liberación de lotes: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US31 | Panel de indicadores de calidad | T107 | Resumen de calidad: vista | Implementar el resumen de calidad con la cola de prioridades y las próximas decisiones. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US31 | Panel de indicadores de calidad | T108 | Resumen de calidad: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US27 | Audit trail | T109 | Audit trail: vista | Implementar el registro de eventos con filtros por registro y actor, compartido por los tres entornos. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US27 | Audit trail | T110 | Audit trail: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US28 | Generación automática de reportes | T111 | Reportes regulatorios: vista | Implementar la lista y generación de reportes regulatorios. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US28 | Generación automática de reportes | T112 | Reportes regulatorios: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US29 | Preparación de auditorías | T113 | Preparación de auditorías: vista | Implementar el registro de auditorías y su estado de preparación. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US29 | Preparación de auditorías | T114 | Preparación de auditorías: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| US30 | Acceso de auditor a evidencias | T115 | Evidencias para auditor: vista | Mostrar las evidencias vinculadas a cada hallazgo de auditoría. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US30 | Acceso de auditor a evidencias | T116 | Evidencias para auditor: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US59 | Registro de auditorías y hallazgos | T117 | Hallazgos de auditoría: vista | Implementar el registro de hallazgos con su severidad y acción asignada. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US59 | Registro de auditorías y hallazgos | T118 | Hallazgos de auditoría: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US33 | Indicadores de trazabilidad | T119 | Indicadores de trazabilidad: vista | Implementar los indicadores de brechas de trazabilidad. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US33 | Indicadores de trazabilidad | T120 | Indicadores de trazabilidad: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US34 | Indicadores de desviaciones | T121 | Indicadores de desviaciones: vista | Implementar la tendencia de desviaciones por periodo. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US34 | Indicadores de desviaciones | T122 | Indicadores de desviaciones: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US40 | Bandeja de tareas | T123 | Bandeja de tareas: vista | Implementar la lista de tareas pendientes vinculadas a registros. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US40 | Bandeja de tareas | T124 | Bandeja de tareas: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US41 | Notificaciones entre áreas | T125 | Comunicación entre áreas: vista | Implementar los comentarios de cada tarea para la coordinación entre Producción y Calidad. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US41 | Notificaciones entre áreas | T126 | Comunicación entre áreas: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US42 | Solicitudes de aprobación | T127 | Solicitudes de aprobación: vista | Crear tareas de aprobación dirigidas a Calidad desde un registro. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US42 | Solicitudes de aprobación | T128 | Solicitudes de aprobación: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 1 | Cobades Zamora, Yhoshua Hebert | Done |
| US43 | Seguimiento de tareas | T129 | Seguimiento de tareas: vista | Mostrar el estado de las tareas asignadas por el usuario. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| US43 | Seguimiento de tareas | T130 | Seguimiento de tareas: store y Fake API | Agregar al store de Quality las operaciones de la vista, sus datos en la Fake API (db.json) y las traducciones en inglés y español. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| — | Tareas técnicas | T131 | Configuración del proyecto Angular | Configurar Angular Material, ngx-translate, environments y json-server con las rutas /api/v1. | 4 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| — | Tareas técnicas | T132 | Capa shared | Implementar las clases base de la API, el layout público, el workspace shell, el page header y el selector de idioma. | 6 | Cobades Zamora, Yhoshua Hebert | Done |
| — | Tareas técnicas | T133 | Traducciones de IoT Monitoring | Agregar las 121 claves de la sección monitoring en inglés y español. | 3 | Rojas Ambicho, Nestor Daniel | Done |
| — | Tareas técnicas | T134 | Documentación del repositorio | Redactar el README, el CHANGELOG, la guía de contribución, las ADRs y el diagrama de clases. | 4 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| — | Tareas técnicas | T135 | Releases v1.0.0 | Preparar release/v1.0.0 en el Website y en la Web Application, con merge a main y tag SemVer. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| — | Tareas técnicas | T136 | Configuración de despliegue | Agregar firebase.json para Firebase Hosting y el script server:prod para publicar la Fake API. | 2 | Rojas Ambicho, Nestor Daniel | Done |

#### 5.2.2.4. Development Evidence for Sprint Review

En el Sprint 2 se trabajó en dos repositorios siguiendo GitFlow: una feature branch por sección del Website o por bounded context de la Web Application, integradas en `develop` con merges `--no-ff`, y una rama `release/v1.0.0` fusionada en `main` con el tag `v1.0.0` en ambos repositorios. El Website recibió además el hotfix `v1.0.1` y el enlace de sus botones de acceso a la Web Application publicada; en la Web Application, después de `v1.0.0` se registraron en `main` los ajustes del despliegue en Firebase Hosting y Render y la versión 1.0.1. Las tablas siguientes presentan todos los commits de `main`; la columna *Branch* indica la rama en que se realizó cada commit.

**Website** (97 commits)

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/doofplus-website | main | `5a5fb40` | chore: initial commit | — | 07/10/2026 |
| IngesCompany/doofplus-website | main | `80e064f` | chore: add gitignore | — | 07/10/2026 |
| IngesCompany/doofplus-website | feature/project-configuration | `afb534f` | feat(translations): add initial language files for English and Spanish | — | 07/10/2026 |
| IngesCompany/doofplus-website | feature/project-configuration | `dc827a9` | feat(translations): implement language switching functionality file | — | 07/10/2026 |
| IngesCompany/doofplus-website | develop | `0a72a3f` | Merge branch 'feature/project-configuration' into develop | — | 07/10/2026 |
| IngesCompany/doofplus-website | feature/navbar-hero | `c569c20` | feat(translations): add language switching functionality and update HTML structure | — | 07/10/2026 |
| IngesCompany/doofplus-website | feature/navbar-hero | `ab9e295` | feat(nav): add navbar with language support in English and Spanish and styles | — | 07/10/2026 |
| IngesCompany/doofplus-website | feature/navbar-hero | `996e8cd` | feat(hero): add hero section with dynamic content placeholders and styles | — | 07/10/2026 |
| IngesCompany/doofplus-website | feature/navbar-hero | `2ca1c4b` | feat(translations): add hero content translations for English and Spanish | — | 07/10/2026 |
| IngesCompany/doofplus-website | develop | `2acc88b` | Merge branch 'feature/navbar-hero' into develop | — | 07/10/2026 |
| IngesCompany/doofplus-website | develop | `0d68dcf` | feat(styles): add modular styles with the 12-column fluid grid | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `a79fefb` | feat(i18n): load English and Spanish texts from JSON files | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `b31ee03` | feat(layout): add navbar with mobile menu, footer and segment access | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `85932c9` | feat(cursor): add custom cursors in the DoofPlus colors | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/plans-section | `cc97535` | feat(i18n): add translation of plans | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/plans-section | `690e9a9` | feat(components): add billing-toggle | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/plans-section | `f3838e1` | feat(styles): add section of plan styles | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/plans-section | `b527590` | feat(scripts): add import of sections | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/plans-section | `8bfd189` | feat(index):  add monthly and yearly plans | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `cdd7304` | Merge branch 'feature/plans-section' into develop | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/restore-hero | `59d793c` | feat(home): restore hero section | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `f886259` | Merge branch 'feature/restore-hero' into develop | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/workspace-section | `c10ba0b` | feat(i18n): add workspace content translations for English and Spanish | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/workspace-section | `3cc963b` | feat(workspace): add process flow bar and section workspace | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/workspace-section | `b8b9428` | feat(workspace): add workspace cards with dynamic content and translation | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `06b0bfe` | Merge branch 'feature/workspace-section' into develop | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/services | `504205f` | feat(services) : add services cards | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/services | `ca857c3` | feat(i18n) : add services content translations for english and spanish | — | 08/10/2026 |
| IngesCompany/doofplus-website | feature/services | `78ab06b` | feat(services) : add services styles | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `0b48370` | Merge branch 'feature/services' into develop | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `0d2bd78` | fix(navbar): skip placeholder links when highlighting sections | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `666d9cd` | feat(i18n): add features content translations for english and spanish | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `c8ffc51` | feat(features): add features section with accordion and preview panels | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `70c9db1` | feat(features): add features styles | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `fbf3b79` | fix(plans): load billing toggle script so the annual option works | — | 08/10/2026 |
| IngesCompany/doofplus-website | develop | `beb359f` | style(form): add textarea and confirmation styles and remove unused demo styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `72c978b` | feat(i18n): add contact inquiry translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/contact-section | `3a58827` | feat(contact): add contact inquiry form section | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `d296d28` | Merge remote-tracking branch 'origin/feature/contact-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/benefits-section | `103c355` | feat(i18n): add benefits content translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/benefits-section | `6e38531` | feat(benefits): add benefits section with key result cards | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/benefits-section | `f043190` | feat(benefits): add benefits styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `9b49664` | Merge branch 'feature/benefits-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/testimonials-section | `e8b7970` | feat(i18n): add testimonials content translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/about-product-section | `f14e0b9` | feat(i18n): add product section content translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/about-product-section | `7fd893b` | feat(video): add styles for product video section | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/about-product-section | `145acdf` | feat(video): add product video section with player and details | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `989262c` | Merge branch 'feature/about-product-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/testimonials-section | `cbfe7b1` | feat(testimonials): add testimonials section with client quotes and ratings | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/testimonials-section | `26f6288` | feat(testimonials): add testimonials styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `f3a3a1e` | Merge branch 'feature/testimonials-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/faq-section | `7833057` | feat(i18n): add faq content translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/faq-section | `9599b92` | feat(faq): add faq section with accordion and contact link | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/faq-section | `ff8e68a` | feat(faq): add faq styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `20a0012` | Merge branch 'feature/faq-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/about-section | `f43c313` | feat(i18n): add about content translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/about-section | `58d8b38` | feat(about): add about section with mission, vision and principles | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/about-section | `ed983a7` | feat(about): add about styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `e0235c1` | Merge branch 'feature/about-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/team-section | `bdeab66` | feat(i18n): add team content translations for english and spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/team-section | `65de15e` | feat(team): add team member photos | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/team-section | `25f6c2b` | feat(team): add team section with member cards | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/team-section | `e40431d` | feat(team): add team styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `217aa55` | Merge branch 'feature/team-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/landing-links | `5e7e811` | fix(landing): replace demo links, fix hero buttons and wrap sections in main | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/navbar | `f5754c1` | feat(navbar): add section links, segment access and mobile menu | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `8236269` | Merge branch 'fix/landing-links' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `b9e41f1` | Merge branch 'feature/navbar' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/hero-section | `ab053c9` | fix(i18n): update hero content translations | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/hero-section | `ab59881` | fix(hero): update hero call to action buttons | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `2b51732` | Merge branch 'fix/hero-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/workspace-section | `25c1931` | fix(i18n): update workspace content translations | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/workspace-section | `486687f` | style(workspace): replace workspace styles with card and banner styles | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/workspace-section | `4e471af` | fix(workspace): simplify segment cards and add new customer banner | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `0af9d9e` | Merge branch 'fix/workspace-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/footer-privacy-section | `483ab70` | fix(i18n): update Spanish translations for product video section producing error | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/footer-privacy-section | `f0d25a0` | feat(terms): add Terms of Service page with legal content and multilingual support | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/footer-privacy-section | `cf1c8a3` | feat(privacy): add Privacy Policy page with legal content and multilingual support | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/footer-privacy-section | `670ebff` | feat(styles): add styles for secondary pages including terms of service and privacy policy | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/footer-privacy-section | `7d42d1c` | feat(legal): add Terms of Service and Privacy Policy sections in English and Spanish | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `6f34ece` | Merge branch 'feature/footer-privacy-section' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/legal-pages | `acda06d` | fix(styles): import the secondary page styles used by the terms and privacy pages | — | 09/10/2026 |
| IngesCompany/doofplus-website | fix/legal-pages | `6f465cd` | fix(i18n): add the page titles and back link translations of the terms and privacy pages | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `f8a1b3d` | Merge branch 'fix/legal-pages' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/videos | `2bd55e5` | feat(video): add the video player that loads the YouTube embed on play | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/videos | `d742662` | feat(team): add the about the team video below the member cards | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `1163cea` | Merge branch 'feature/videos' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | release/v1.0.0 | `42a44c0` | chore(release): set the landing page version to 1.0.0 | — | 09/10/2026 |
| IngesCompany/doofplus-website | main | `1acb96b` | Merge branch 'release/v1.0.0' | — | 09/10/2026 |
| IngesCompany/doofplus-website | hotfix/v1.0.1 | `7a2de04` | fix(deploy): publish the static site on GitHub Pages without the Jekyll build | — | 09/10/2026 |
| IngesCompany/doofplus-website | hotfix/v1.0.1 | `d4efb41` | chore(release): set the landing page version to 1.0.1 | — | 09/10/2026 |
| IngesCompany/doofplus-website | main | `61326ed` | Merge branch 'hotfix/v1.0.1' | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `385a2f9` | Merge branch 'release/v1.0.0' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `97a9e4b` | Merge branch 'hotfix/v1.0.1' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | feature/web-app-links | `467b222` | feat(config): link the segment access buttons to the published web application | — | 09/10/2026 |
| IngesCompany/doofplus-website | develop | `bb1946e` | Merge branch 'feature/web-app-links' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-website | main | `4e2299e` | Merge branch 'develop' | — | 09/10/2026 |

**Frontend Web Application** (178 commits)

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/doofplus-web-application | main | `16247a9` | chore: initial commit | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | main | `58f3404` | chore: add git ignore | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | feature/project-configuration | `89336d3` | feat(i18n): add i18n support for English and Spanish translation | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | feature/project-configuration | `84282bf` | feat(ui): add Material Design UI Library | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | feature/project-configuration | `cb6376e` | feat(environment): add Environment configuration for development and production modes | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | develop | `3ea5890` | Merge branch 'feature/project-configuration' into develop | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `b066a80` | feat(home): add Home view with title and content, including route definition and style | — | 28/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `6d386d5` | feat(home): add DateTime and URL value objects for handing dates and URLs | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `574db0d` | feat(base-entity): add BaseEntity interface for domain entities with UUID identifier | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `b1906c4` | feat(toolbar): add responsive toolbar component | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `c701062` | feat(layout): add layout component | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `f5ed375` | feat(language-switcher): add language switcher component for UI language selection | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `c0bcedc` | feat(about): add About page with layout, styles, and content for product overview | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `78a850c` | feat(page-not-found): add Page Not Found component with template and navigation | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `9df65b3` | chore(index): update index.html structure for semantic consistency | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `8ebbec3` | style(layout): add tittle | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `067727c` | feat(about): add the route definition of the view About | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `9840b0b` | feat(routes): add the route definition of the view About and PageNotFound | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `f4f9185` | Merge remote-tracking branch 'origin/feature/shared' into feature/shared | # Conflicts: # src/app/app.routes.ts | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `a270b2f` | feat(footer): add footer component and translation | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `485f392` | feat(footer): add footer component and translation | — | 29/09/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `46a135e` | fix(layout): render toolbar globally across public views and add translations | — | 30/09/2026 |
| IngesCompany/doofplus-web-application | develop | `e7ec1ba` | Merge branch 'feature/shared' into develop | — | 05/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `c5951a6` | feat(database): add initial db.json with vaccine batch data | — | 05/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `dd30869` | feat(batch): add Batch entity to represent product batches | — | 05/10/2026 |
| IngesCompany/doofplus-web-application | feature/share-fixes | `a09dd57` | fix(shared): add missing DoofPlus logo asset | — | 06/10/2026 |
| IngesCompany/doofplus-web-application | feature/share-fixes | `6f4ce9c` | fix(i18n): add missing translations for home, about and page not found views | — | 06/10/2026 |
| IngesCompany/doofplus-web-application | develop | `23e6e5a` | Merge branch 'feature/share-fixes' into develop | — | 06/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `5f53fd7` | feat(server): add JSON server setup to run the locale database | — | 07/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `43b4302` | feat(manufacturing): add infrastructure layer in manufacturing for batch operations | — | 07/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `98bd8a3` | feat(database): add db.json with initial posts and comments data | — | 07/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `ae368f6` | feat(manufacturing): implement ManufacturingStore for batch state management in application layer | — | 07/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `353c95b` | feat(batch): add BatchList component with support in English and Spanish and routing for batch management | — | 07/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `07e9dc2` | feat(batch): add BatchForm component with support in English and Spanish and routing | — | 07/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `2092428` | Merge branch 'develop' into feature/manufacturing | — | 08/10/2026 |
| IngesCompany/doofplus-web-application | develop | `f8184a4` | Merge branch 'feature/manufacturing' into develop | — | 08/10/2026 |
| IngesCompany/doofplus-web-application | develop | `9ab2fae` | fix(routes): integrate manufacturing routes into main app routing | — | 08/10/2026 |
| IngesCompany/doofplus-web-application | develop | `0e9ba1a` | fix(manufacturing): add ChangeDetectorRef to batch list to trigger zoneless rendering | — | 08/10/2026 |
| IngesCompany/doofplus-web-application | develop | `767e6a2` | test(mock): update mock database with testing records | — | 08/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `00c63c2` | feat(iam): add domain models for user authentication and authorization | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `96c30c7` | feat(iam): add data transfer objects and assembler for sign-in flow | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `3aa4550` | feat(iam): add data transfer objects and assembler for sign-up flow | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `f6b50bc` | feat(iam): implement IamApi for user sign-up and sign-in functionality | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `f28cca2` | feat(store): add application store to manage authentication state | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `68ed25a` | feat(guard): add route guard to protect authenticated views | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `41b15e9` | feat(interceptor): add interceptor to attach bearer tokens | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `bf9e497` | feat(sign-in-view): add user interface component for sign in | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `1da2e62` | feat(sign-up-view): add user interface component for sign up | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `0d905de` | feat(routing): integrate iam views and configure loading for authentication | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `c59594f` | Merge branch 'feature/iam' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `8aab2ab` | chore(server): add documents, deviations, CAPA, results, audits, reports and tasks to the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `493c0ec` | feat(environment): add the fake API base URL and the quality endpoint paths | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `863f2c8` | feat(quality): model documents, deviations, CAPA, analytical results, audits, reports and tasks | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `de4c4f6` | feat(quality): read and write the quality collections through the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `141ea68` | feat(quality): enforce release, signature, segregation of duties and CAPA closure rules in the store | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `a26fb2d` | feat(quality-view): add the quality overview and the traceability and deviation indicators | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `f0ec8e2` | feat(document-view): add controlled documents with approval workflow and version history | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `83b92e7` | feat(release-view): add batch release with electronic signature and the analytical results | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `46ea7c9` | feat(task-view): add tasks and discussions linked to records | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `d0bd0c5` | feat(i18n): add the quality and compliance translations in English and Spanish | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `e91dbb4` | feat(routing): add the routes of the quality bounded context | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `ee75ac9` | fix(config): complete the index.html head with viewport, fonts, icons and SEO meta tags | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `28b167d` | feat(environment): add the landing page URL and the fake API base URL | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `fca883b` | style(theme): apply DoofPlus colors and shapes to the Material theme | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `5c6559e` | style(shared): add layout, status and accessibility helpers for the Figma views | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `0ac965e` | feat(shared): add base API, endpoint, assembler and form classes from the course base project | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `7657404` | feat(language-switcher): show the EN/ES pill of the mock-ups and remember the chosen language | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `939f04d` | feat(alert): add Alert entity to represent system alerts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `3798e78` | feat(layout): turn the toolbar, footer and layout into the public frame of the mock-ups | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `9f900a0` | feat(equipment): add Equipment entity to represent equipment details and maintenance | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `33cd8ca` | feat(page-header): add breadcrumb, title and actions header for workspace pages | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `1d274fd` | feat(reading): add Reading entity to represent telemetry readings | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `1286b97` | feat(config): use outlined Material icons, bind route parameters to inputs and announce the page language | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `28f0f89` | feat(sensor): add Sensor entity to represent IoT sensors and their properties | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `8b345e2` | refactor(shared): replace home and about with the sign-in entry point | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/shared | `9ca0dea` | test(app): check that the root component hosts the routed views | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `7aa3999` | Merge branch 'feature/shared' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `30ebe27` | chore(server): add users, role profiles and invitations to the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `5c45a1a` | feat(environment): add the endpoint paths of the IAM collections | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `bf84897` | feat(monitoring-api): add monitoring api service for iot endpoints management | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `fbe4243` | feat(iam): model users with environment and organization, role profiles and invitations | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `a66ff4c` | feat(alert): add alert API endpoint and assembler for CRUD operations | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `e3c2e89` | feat(iam): read users, role profiles and invitations from the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `cb30ca9` | feat(equipment): add API endpoint, assembler, and response models for equipment CRUD operations | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `271285c` | feat(iam): sign in by environment with a two-factor code and role-based access | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `b2c9c9d` | feat(reading): add Reading API endpoint, assembler, and response models for CRUD operations | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `496cd7a` | feat(layout): add the workspace shell with sidebar, top bar and user menu | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `e60fbcd` | feat(sensor): add Sensor API endpoint, assembler, and response models for CRUD operations | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `31c5208` | feat(sign-in-view): add environment selection, sign-in, two-factor and not-authorized views | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `042b8fe` | feat(users-view): add users and profiles directory and the invite user form | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `73b7b53` | feat(monitoring-store): add monitoringstore for managing equipment, sensors, readings, and alerts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `d304131` | feat(i18n): add the IAM and workspace translations in English and Spanish | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `4a3f0b6` | feat(routing): route the sign-in and the three environments protected by the IAM guard | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/iam | `9a91e9d` | refactor(iam): remove the token sign-in, sign-up and interceptor that the fake API cannot serve | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `9ca9813` | Merge remote-tracking branch 'origin/feature/iam' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `5aa36c1` | chore(server): add json-server as a development dependency | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `bae6ffe` | chore(config): raise the component style budget for the Figma layouts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `092339a` | feat(telemetry-chart): add telemetry chart component for visualizing sensor readings | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `e457c8a` | chore(server): replace the sample production batches with the manufacturing collections | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `dd7b09f` | feat(environment): add the endpoint paths of the manufacturing collections | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `fe885b3` | feat(manufacturing): model products, master formulas, orders, operations, batches and material lots | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `1b415ea` | feat(manufacturing): read and write the manufacturing collections through the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `33eebd2` | feat(manufacturing): validate batches, record operations and receive materials in the store with signals | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `67542b0` | feat(alert-list): add alert list component for displaying IoT incidents with severity and status | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `ded2019` | feat(batch-view): turn the batch form into the create batch dialog with the rejection state | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `519b1cd` | feat(batch-iot-evidence): add component for displaying IoT evidence with equipment association and readings | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `8a49239` | feat(equipment-inventory): add equipment inventory component for managing sensors and maintenance | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `b4190b2` | feat(iot-overview): add IoT overview component for monitoring sensor and equipment health, telemetry, and alerts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `d85d8bf` | feat(sensor-detail): add sensor detail component for displaying telemetry, alerts, and equipment calibration | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `448e9de` | feat(routes): add monitoring routes for IoT overview, equipment inventory, sensor detail, alert list, and batch IoT evidence | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `037a753` | feat(batch-view): show batches with status counts, filters, lookup and the selected batch | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `4ca6f73` | chore(server): add plans, the organization subscription and invoices to the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `58d11c5` | feat(batch-view): add batch genealogy and status history | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `7903c15` | feat(environment): add the endpoint paths of the subscription collections | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `1d252d1` | feat(order-view): add production orders and the order execution against the master formula | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `ba60036` | feat(product-view): add the product catalog and the effective master formula | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `ea09f17` | feat(receipt-view): add the raw-material receipt with quarantine inspection | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `af07149` | feat(subscriptions): model plans, subscriptions and invoices | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `7646e4c` | feat(i18n): replace the batch translations with the manufacturing translations and add shared labels | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `223e7ca` | feat(routing): route the manufacturing views in the production environment | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `5d3118b` | feat(subscriptions): read plans, subscriptions and invoices from the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `c6a4fda` | feat(subscriptions): manage the plan change and the payment retry in the subscriptions store | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `01e3922` | feat(subscription-view): add the subscriptions and payments page with billing history and plan change review | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `3f183b2` | Merge branch 'develop' into feature/monitoring | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `b9a862a` | feat(db): add equipment and sensor data with calibration and maintenance details | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `9dc488c` | feat(i18n): add the subscriptions translations in English and Spanish | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `9383633` | chore(db): remove unnecessary whitespace and trailing braces from db.json | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `b104c03` | feat(environment): add new endpoint paths for equipment, sensors, readings, and alerts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions | `23c8b4e` | feat(routing): route the subscriptions page in the administration environment | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `1481052` | Merge branch 'feature/subscriptions' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `d05ab97` | Merge branch 'develop' into feature/monitoring | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `e78965d` | chore(server): add the organization, facilities, user profiles and administrative activity to the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `0737256` | feat(environment): add the endpoint paths of the organization collections | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `63f97ed` | feat(organizations): model organizations, facilities, user profiles and administrative activity | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `6a75732` | feat(routes): add monitoring routes to production environment | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `eace210` | feat(organizations): read and register organizations through the fake API | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `f3e103f` | chore(routes): clean up import statements in app.routes.ts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `378c1a7` | feat(organizations): register organizations and update user profiles in the organizations store | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `14b745a` | Merge branch 'feature/monitoring' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `028ab75` | feat(registration-view): add the organization registration with plan and first administrator | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `9646143` | feat(overview-view): add the administration overview with users, facilities and account health | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `0c0d6bd` | feat(profile-view): add profile and notification preferences for every environment | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `d03f0bc` | Merge branch 'develop' into feature/organizations | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `222adee` | feat(i18n): add the organizations translations in English and Spanish | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/organizations | `3bb4348` | feat(routing): route the registration, the administration overview and the profile | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `0d4cdb9` | feat(overview): add the production overview with schedule readiness and incident priorities | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing | `6f3053b` | feat(routing): route the production overview as the production home | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `be5d92b` | Merge branch 'feature/organizations' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `6e3273e` | fix(i18n): use shared cancel and status labels instead of keys from other bounded context | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `a5ffaaa` | fix(routing): route the quality view and share the audit trail and task with every environment | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `0446f56` | Merge branch 'feature/manufacturing' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `05fae7c` | Merge branch 'develop' into feature/quality | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `f53fbe1` | fix(i18n): use the shared status label in the remaining quality views | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/quality | `7de536e` | fix(routing): add the quality routes to the qa, production and administration environments | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `4132182` | Merge branch 'feature/quality' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | docs/repository-setup | `1864b3b` | docs(readme): add project documentation, run instructions and bounded contexts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | docs/repository-setup | `f791346` | chore(license): add MIT license | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | docs/repository-setup | `abb5afc` | docs(repository): add changelog and contributing guidelines | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | docs/repository-setup | `60145ed` | docs(architecture): create docs directory with user stories and diagrams placeholders | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `158f838` | Merge branch 'docs/repository-setup' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | docs/expanded-readme | `0b2a174` | docs(readme): expand documentation with badges, architecture and tech stack details | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `8c47f21` | Merge branch 'docs/expanded-readme' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `3a87aa1` | docs(architecture): fix readme markdown, add ADRs and mermaid diagrams | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `1298689` | docs(architecture): add domain model class diagram | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `39b250c` | docs(architecture): align docs structure with learning-center (PlantUML and single adrs file) | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/monitoring | `785fda4` | feat(i18n): add the IoT monitoring translations in English and Spanish | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `efa7877` | Merge branch 'feature/monitoring' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/project-configuration | `c96bd29` | docs(readme): rename the demo accounts section to test accounts | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/project-configuration | `317784a` | chore(server): add a start script to publish the fake API on a hosting service | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | feature/project-configuration | `a258f40` | chore(deploy): add the Firebase Hosting configuration for the single page application | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | develop | `eab64e9` | Merge branch 'feature/project-configuration' into develop | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | release/v1.0.0 | `700dcb1` | chore(release): set the web application version to 1.0.0 and update the changelog | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | main | `d63b938` | Merge branch 'release/v1.0.0' | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | main | `b0097e9` | fix(environment): read the fake API published on Render in production | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | main | `9a7d14b` | chore(deploy): link the Firebase project and ignore the deploy cache | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | main | `c9dbe4e` | fix(server): restore the seed state of material lot RM-26104 | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | main | `079465a` | fix(a11y): name tables and alerts of the views copied before the accessibility work | — | 09/10/2026 |
| IngesCompany/doofplus-web-application | main | `946151e` | chore(release): set the web application version to 1.0.1 and update the changelog | — | 09/10/2026 |

#### 5.2.2.5. Execution Evidence for Sprint Review

En este Sprint se completó el Website, publicada en GitHub Pages, y se implementó la Web Application con sus tres entornos. En el Website se agregaron el hero, el acceso por segmento, los servicios y características, el video About the Product, los beneficios, About us, el equipo con su video, los testimonios y las preguntas frecuentes, y se reimplementaron la navegación con menú mobile, los planes, el formulario de consulta y las páginas legales. La Web Application permite elegir el entorno, iniciar sesión con segundo factor y recorrer todos los módulos de QA/QC (documentos, desviaciones y CAPA, resultados analíticos, liberación de lotes, auditorías, audit trail, reportes y tareas), Production (órdenes, productos y fórmulas, lotes, materias primas, equipos e IoT, incidentes) y Administration (usuarios, organización y suscripción), en inglés y español, con datos servidos por una Fake API.

**Website:** https://ingescompany.github.io/doofplus-website/

![Hero con la propuesta de valor (US01)](assets/img/chapter5/sprint2/landing/01-home.png)

*Figura: Hero con la propuesta de valor (US01).*

![Acceso por segmento: Choose your workspace (US48)](assets/img/chapter5/sprint2/landing/02-workspace.png)

*Figura: Acceso por segmento: Choose your workspace (US48).*

![Servicios (US02)](assets/img/chapter5/sprint2/landing/03-services.png)

*Figura: Servicios (US02).*

![Características con acordeón y vista previa (US02)](assets/img/chapter5/sprint2/landing/04-features.png)

*Figura: Características con acordeón y vista previa (US02).*

![Video About the Product (US49)](assets/img/chapter5/sprint2/landing/05-product.png)

*Figura: Video About the Product (US49).*

![Beneficios](assets/img/chapter5/sprint2/landing/06-benefits.png)

*Figura: Beneficios.*

![Planes con toggle mensual/anual (US03)](assets/img/chapter5/sprint2/landing/07-plans.png)

*Figura: Planes con toggle mensual/anual (US03).*

![About us: misión y visión (US45)](assets/img/chapter5/sprint2/landing/08-about.png)

*Figura: About us: misión y visión (US45).*

![Our Team y video About the Team (US45, US49)](assets/img/chapter5/sprint2/landing/09-team.png)

*Figura: Our Team y video About the Team (US45, US49).*

![Testimonios](assets/img/chapter5/sprint2/landing/10-testimonials.png)

*Figura: Testimonios.*

![Preguntas frecuentes (US05)](assets/img/chapter5/sprint2/landing/11-faq.png)

*Figura: Preguntas frecuentes (US05).*

![Formulario Contact us y footer (US04)](assets/img/chapter5/sprint2/landing/12-contact.png)

*Figura: Formulario Contact us y footer (US04).*

![Website en español (US46)](assets/img/chapter5/sprint2/landing/13-home-es.png)

*Figura: Website en español (US46).*

![Términos de Servicio (US47)](assets/img/chapter5/sprint2/landing/14-terms.png)

*Figura: Términos de Servicio (US47).*

La sección 5 de los Términos de Servicio, «Compromiso profesional y ético», declara que IngesCompany desarrolla DoofPlus siguiendo el Código de Ética de Ingeniería de Software de ACM/IEEE (ACM/IEEE-CS Joint Task Force on Software Engineering Ethics and Professional Practices, 1999) y el Código de Ética del Colegio de Ingenieros del Perú (Colegio de Ingenieros del Perú, s. f.): actuar en interés público, ser transparente sobre los límites del producto y reportar cualquier incidente que afecte los datos de los clientes. La página está enlazada desde el footer del Website, en español e inglés.

![Vista mobile](assets/img/chapter5/sprint2/landing/15-mobile-home.png)

*Figura: Vista mobile.*

![Menú de navegación en mobile (US44)](assets/img/chapter5/sprint2/landing/16-mobile-menu.png)

*Figura: Menú de navegación en mobile (US44).*

**Web Application:** https://doofplus-webapp.web.app (cuentas de prueba en el README del repositorio; contraseña `DoofPlus2026!` y código 2FA `482106`).

![Elección de entorno (US06)](assets/img/chapter5/sprint2/web-app/01-sign-in.png)

*Figura: Elección de entorno (US06).*

![Verificación con código 2FA (US06)](assets/img/chapter5/sprint2/web-app/02-two-factor.png)

*Figura: Verificación con código 2FA (US06).*

![QA/QC · Quality overview (US31)](assets/img/chapter5/sprint2/web-app/03-qa-overview.png)

*Figura: QA/QC · Quality overview (US31).*

![QA/QC · Quality documents con versiones y aprobación (US09, US12, US13)](assets/img/chapter5/sprint2/web-app/04-qa-documents.png)

*Figura: QA/QC · Quality documents con versiones y aprobación (US09, US12, US13).*

![QA/QC · Deviation report y evaluación de riesgo (US18)](assets/img/chapter5/sprint2/web-app/05-qa-deviations.png)

*Figura: QA/QC · Deviation report y evaluación de riesgo (US18).*

![QA/QC · Plan CAPA (US19, US20, US21)](assets/img/chapter5/sprint2/web-app/06-qa-capa.png)

*Figura: QA/QC · Plan CAPA (US19, US20, US21).*

![QA/QC · Liberación de lotes con firma electrónica (US54, US08)](assets/img/chapter5/sprint2/web-app/07-qa-batch-release.png)

*Figura: QA/QC · Liberación de lotes con firma electrónica (US54, US08).*

![QA/QC · Audit trail (US27)](assets/img/chapter5/sprint2/web-app/08-qa-audit-trail.png)

*Figura: QA/QC · Audit trail (US27).*

![Production · Production overview (US32)](assets/img/chapter5/sprint2/web-app/09-production-overview.png)

*Figura: Production · Production overview (US32).*

![Production · Órdenes de producción (US57)](assets/img/chapter5/sprint2/web-app/10-production-orders.png)

*Figura: Production · Órdenes de producción (US57).*

![Production · Lotes con filtros y lote seleccionado (US14, US15, US16)](assets/img/chapter5/sprint2/web-app/11-production-batches.png)

*Figura: Production · Lotes con filtros y lote seleccionado (US14, US15, US16).*

![Production · IoT overview con telemetría (US25, US26)](assets/img/chapter5/sprint2/web-app/12-iot-overview.png)

*Figura: Production · IoT overview con telemetría (US25, US26).*

![Production · Equipos y sensores IoT (US23, US37, US38)](assets/img/chapter5/sprint2/web-app/13-equipment.png)

*Figura: Production · Equipos y sensores IoT (US23, US37, US38).*

![Production · Incidentes (US56, US22)](assets/img/chapter5/sprint2/web-app/14-incidents.png)

*Figura: Production · Incidentes (US56, US22).*

![Administration · Resumen de administración (US50)](assets/img/chapter5/sprint2/web-app/15-admin-overview.png)

*Figura: Administration · Resumen de administración (US50).*

![Administration · Usuarios y perfiles (US55, US07)](assets/img/chapter5/sprint2/web-app/16-admin-users.png)

*Figura: Administration · Usuarios y perfiles (US55, US07).*

![Administration · Suscripción y pagos (US51, US52, US53)](assets/img/chapter5/sprint2/web-app/17-admin-subscription.png)

*Figura: Administration · Suscripción y pagos (US51, US52, US53).*

![Administration · Suscripción y pagos en español](assets/img/chapter5/sprint2/web-app/18-admin-subscription-es.png)

*Figura: Administration · Suscripción y pagos en español.*

![Registro de la organización (US50)](assets/img/chapter5/sprint2/web-app/19-register.png)

*Figura: Registro de la organización (US50).*

![Inicio de sesión en mobile](assets/img/chapter5/sprint2/web-app/20-mobile-sign-in.png)

*Figura: Inicio de sesión en mobile.*

Video de navegación del producto: upc-pre-202620-1asi0729-7742-IngesCompany-productnavigation-sprint-2 (duración: 11:20), ver en Microsoft Stream: https://shorturl.at/6lL4u. Muestra la navegación del Website y de la Web Application implementados en el Sprint 2.

[![Video de navegación del producto del Sprint 2](assets/img/chapter5/sprint2/product-navigation-video.png)](https://shorturl.at/6lL4u)

*Figura: Cuadro del video de navegación del producto del Sprint 2 (minuto 3:50, sección del equipo en el Website).*

#### 5.2.2.6. Services Documentation Evidence for Sprint Review

En el Sprint 2 todavía no se implementaron los RESTful Web Services, por lo que no hay documentación OpenAPI. Mientras tanto, la Web Application consume una Fake API con json-server (`server/db.json`), cuyas rutas se exponen bajo el prefijo `/api/v1` mediante `server/routes.json`, el mismo que tendrán los Web Services. La siguiente tabla documenta los endpoints que usa la Web Application; la URL base local es `http://localhost:3000/api/v1` y la publicada en Render es `https://ingescompany-frontend.onrender.com/api/v1` (por ejemplo, `/plans`: https://ingescompany-frontend.onrender.com/api/v1/plans).

| Endpoint | Verbo HTTP | Sintaxis | Parámetros | Response | URL documentación |
|---|---|---|---|---|---|
| `/invitations` | GET | `/api/v1/invitations` | — | 200 OK con la lista de `invitations` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/invitations` | POST | `/api/v1/invitations` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/role-profiles` | GET | `/api/v1/role-profiles` | — | 200 OK con la lista de `role-profiles` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/users` | GET | `/api/v1/users` | — | 200 OK con la lista de `users` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/users` | GET | `/api/v1/users?email={email}&password={password}` | `email`, `password` (query) | 200 OK con el usuario cuyas credenciales coinciden (inicio de sesión) | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/users` | GET | `/api/v1/users?id={id}&twoFactorCode={code}` | `id`, `twoFactorCode` (query) | 200 OK con el usuario si el código 2FA es válido | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/users` | POST | `/api/v1/users` | Usuario en el body (JSON) | 201 Created con el usuario invitado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/batch-events` | GET | `/api/v1/batch-events` | — | 200 OK con la lista de `batch-events` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/batch-events` | POST | `/api/v1/batch-events` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/batches` | GET | `/api/v1/batches` | — | 200 OK con la lista de `batches` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/batches` | POST | `/api/v1/batches` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/batches` | PUT | `/api/v1/batches/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/formula-items` | GET | `/api/v1/formula-items` | — | 200 OK con la lista de `formula-items` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/master-formulas` | GET | `/api/v1/master-formulas` | — | 200 OK con la lista de `master-formulas` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/material-lots` | GET | `/api/v1/material-lots` | — | 200 OK con la lista de `material-lots` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/material-lots` | POST | `/api/v1/material-lots` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/material-lots` | PUT | `/api/v1/material-lots/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/operations` | GET | `/api/v1/operations` | — | 200 OK con la lista de `operations` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/operations` | PUT | `/api/v1/operations/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/production-orders` | GET | `/api/v1/production-orders` | — | 200 OK con la lista de `production-orders` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/production-orders` | POST | `/api/v1/production-orders` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/products` | GET | `/api/v1/products` | — | 200 OK con la lista de `products` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/products` | POST | `/api/v1/products` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/alerts` | GET | `/api/v1/alerts` | — | 200 OK con la lista de `alerts` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/alerts` | PUT | `/api/v1/alerts/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/equipment` | GET | `/api/v1/equipment` | — | 200 OK con la lista de `equipment` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/equipment` | PUT | `/api/v1/equipment/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/readings` | GET | `/api/v1/readings` | — | 200 OK con la lista de `readings` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/sensors` | GET | `/api/v1/sensors` | — | 200 OK con la lista de `sensors` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/sensors` | POST | `/api/v1/sensors` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/sensors` | PUT | `/api/v1/sensors/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/administrative-activities` | GET | `/api/v1/administrative-activities` | — | 200 OK con la lista de `administrative-activities` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/facilities` | GET | `/api/v1/facilities` | — | 200 OK con la lista de `facilities` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/facilities` | POST | `/api/v1/facilities` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/organizations` | GET | `/api/v1/organizations/{id}` | `id` (path) | 200 OK con el recurso de `organizations` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/organizations` | POST | `/api/v1/organizations` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/organizations` | GET | `/api/v1/organizations?ruc={ruc}` | `ruc` (query) | 200 OK con la organización que ya usa ese RUC | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/user-profiles` | GET | `/api/v1/user-profiles` | — | 200 OK con la lista de `user-profiles` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/user-profiles` | PUT | `/api/v1/user-profiles/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/analytical-results` | GET | `/api/v1/analytical-results` | — | 200 OK con la lista de `analytical-results` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/analytical-results` | POST | `/api/v1/analytical-results` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/analytical-results` | PUT | `/api/v1/analytical-results/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audit-events` | GET | `/api/v1/audit-events` | — | 200 OK con la lista de `audit-events` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audit-events` | POST | `/api/v1/audit-events` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audit-events` | PUT | `/api/v1/audit-events/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audit-findings` | GET | `/api/v1/audit-findings` | — | 200 OK con la lista de `audit-findings` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audit-findings` | POST | `/api/v1/audit-findings` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audit-findings` | PUT | `/api/v1/audit-findings/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audits` | GET | `/api/v1/audits` | — | 200 OK con la lista de `audits` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audits` | POST | `/api/v1/audits` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/audits` | PUT | `/api/v1/audits/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/capa-actions` | GET | `/api/v1/capa-actions` | — | 200 OK con la lista de `capa-actions` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/capa-actions` | POST | `/api/v1/capa-actions` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/capa-actions` | PUT | `/api/v1/capa-actions/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/capa-plans` | GET | `/api/v1/capa-plans` | — | 200 OK con la lista de `capa-plans` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/capa-plans` | POST | `/api/v1/capa-plans` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/capa-plans` | PUT | `/api/v1/capa-plans/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/collaboration-tasks` | GET | `/api/v1/collaboration-tasks` | — | 200 OK con la lista de `collaboration-tasks` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/collaboration-tasks` | POST | `/api/v1/collaboration-tasks` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/collaboration-tasks` | PUT | `/api/v1/collaboration-tasks/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/deviation-trends` | GET | `/api/v1/deviation-trends` | — | 200 OK con la lista de `deviation-trends` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/deviation-trends` | POST | `/api/v1/deviation-trends` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/deviation-trends` | PUT | `/api/v1/deviation-trends/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/deviations` | GET | `/api/v1/deviations` | — | 200 OK con la lista de `deviations` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/deviations` | POST | `/api/v1/deviations` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/deviations` | PUT | `/api/v1/deviations/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/evidence` | GET | `/api/v1/evidence` | — | 200 OK con la lista de `evidence` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/evidence` | POST | `/api/v1/evidence` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/evidence` | PUT | `/api/v1/evidence/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/quality-documents` | GET | `/api/v1/quality-documents` | — | 200 OK con la lista de `quality-documents` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/quality-documents` | POST | `/api/v1/quality-documents` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/quality-documents` | PUT | `/api/v1/quality-documents/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/regulatory-reports` | GET | `/api/v1/regulatory-reports` | — | 200 OK con la lista de `regulatory-reports` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/regulatory-reports` | POST | `/api/v1/regulatory-reports` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/regulatory-reports` | PUT | `/api/v1/regulatory-reports/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/task-comments` | GET | `/api/v1/task-comments` | — | 200 OK con la lista de `task-comments` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/task-comments` | POST | `/api/v1/task-comments` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/task-comments` | PUT | `/api/v1/task-comments/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/traceability-gaps` | GET | `/api/v1/traceability-gaps` | — | 200 OK con la lista de `traceability-gaps` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/traceability-gaps` | POST | `/api/v1/traceability-gaps` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/traceability-gaps` | PUT | `/api/v1/traceability-gaps/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/invoices` | GET | `/api/v1/invoices` | — | 200 OK con la lista de `invoices` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/invoices` | POST | `/api/v1/invoices` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/plans` | GET | `/api/v1/plans` | — | 200 OK con la lista de `plans` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/subscriptions` | GET | `/api/v1/subscriptions` | — | 200 OK con la lista de `subscriptions` | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/subscriptions` | POST | `/api/v1/subscriptions` | Recurso en el body (JSON) | 201 Created con el recurso creado | https://github.com/IngesCompany/doofplus-web-application#readme |
| `/subscriptions` | PUT | `/api/v1/subscriptions/{id}` | `id` (path) y recurso en el body (JSON) | 200 OK con el recurso actualizado | https://github.com/IngesCompany/doofplus-web-application#readme |

#### 5.2.2.7. Software Deployment Evidence for Sprint Review

En este Sprint se prepararon las versiones estables de ambos productos siguiendo GitFlow:

- **Website:** la rama `release/v1.0.0` se fusionó en `main` con el tag `v1.0.0`, y luego se publicó el hotfix `v1.0.1`, que agrega el archivo `.nojekyll` para que GitHub Pages publique los archivos estáticos sin procesarlos con Jekyll. El Website se publica en GitHub Pages desde `main` en https://ingescompany.github.io/doofplus-website/.
- **Web Application:** la rama `release/v1.0.0` se fusionó en `main` con el tag `v1.0.0` y su CHANGELOG. El repositorio incluye `firebase.json`, que configura Firebase Hosting como Single Page Application, y el script `npm run server:prod`, que publica la Fake API en un Web Service de Render. Después del release se agregaron en `main` la lectura de la Fake API publicada en Render, la vinculación del proyecto de Firebase y correcciones de accesibilidad, y la versión se actualizó a 1.0.1 en el CHANGELOG. La Web Application está publicada en Firebase Hosting en https://doofplus-webapp.web.app y la Fake API en Render en https://ingescompany-frontend.onrender.com/api/v1.

![Tag v1.0.0 del Website](assets/img/chapter5/sprint2/github/release-landing-v1.0.0.png)

*Figura: Tag v1.0.0 del repositorio del Website.*

![Tag v1.0.0 de la Web Application](assets/img/chapter5/sprint2/github/release-frontend-v1.0.0.png)

*Figura: Tag v1.0.0 del repositorio de la Web Application.*

![Website publicado](assets/img/chapter5/sprint2/landing/01-home.png)

*Figura: Website publicado en GitHub Pages.*

#### 5.2.2.8. Team Collaboration Insights during Sprint

Los cinco integrantes participaron en ambos repositorios. La siguiente tabla resume los commits de cada integrante en `main` (sin contar los commits de merge), seguida de los analíticos de GitHub: *Contributors*, que muestra los commits por integrante, y *Network*, que muestra las ramas de GitFlow y sus merges.

| Team Member | GitHub Username | Website | Web Application | Total |
|---|---|:---:|:---:|:---:|
| Rojas Ambicho, Nestor Daniel | danRO-20 | 25 | 23 | 48 |
| Zavaleta Gutierrez, Rodolfo Martin | gutierrezrodolfo360-bit | 17 | 44 | 61 |
| Cobades Zamora, Yhoshua Hebert | YhoshuaCZ | 13 | 56 | 69 |
| Angulo Ramírez, Marcelo Martín | Zock2005 | 8 | 28 | 36 |
| Flores Martinez, Ricardo Andres | Nitoryu28 | 8 | 4 | 12 |

![Contributors del Website](assets/img/chapter5/sprint2/github/insights-landing-contributors.png)

*Figura: Contributors del repositorio del Website.*

![Contributors de la Web Application](assets/img/chapter5/sprint2/github/insights-frontend-contributors.png)

*Figura: Contributors del repositorio de la Web Application.*

![Network del Website](assets/img/chapter5/sprint2/github/insights-landing-network.png)

*Figura: Network graph del repositorio del Website.*

![Network de la Web Application](assets/img/chapter5/sprint2/github/insights-frontend-network.png)

*Figura: Network graph del repositorio de la Web Application.*

### 5.2.3. Sprint 3

En esta sección se registra y explica el avance en términos de producto y trabajo colaborativo para el **Sprint 3** (del 18/10/2026 al 14/11/2026), cuyo enfoque fue entregar la primera versión desplegada de los RESTful Web Services, mejorar el Website y la Web Application a partir del feedback del Sprint 2 y preparar la primera versión del curso de Responsabilidad Social.

#### 5.2.3.1. Sprint Planning 3

El Sprint Planning Meeting sirvió para definir los objetivos del Sprint, asignar responsabilidades por bounded context y seleccionar las Technical Stories de los RESTful Web Services. A continuación, se presenta el resumen de la reunión de planificación:

| Sprint # | Sprint 3 |
|----------|----------|
| **Sprint Planning Background** | |
| **Date** | 2026-10-18 |
| **Time** | 10:00 AM |
| **Location** | Reunión virtual vía Discord |
| **Prepared By** | Zavaleta Gutierrez, Rodolfo Martin |
| **Attendees (to planning meeting)** | Angulo Ramírez, Marcelo Martín / Cobades Zamora, Yhoshua Hebert / Flores Martinez, Ricardo Andres / Torres Juárez, Alisee Muriel / Rojas Ambicho, Nestor Daniel / Zavaleta Gutierrez, Rodolfo Martin |
| **Sprint 2 Review Summary** | Se entregó el Website completo en GitHub Pages y la primera versión de la Web Application (`v1.0.0`) en Firebase Hosting, con sus tres entornos y una Fake API en Render. Como feedback, se pidió llevar el formulario de contacto a la Web Application, unir el Website con el entorno de cada segmento y empezar los RESTful Web Services que reemplacen a la Fake API. |
| **Sprint 2 Retrospective Summary** | Como acierto, el equipo publicó cada versión con ramas `release/` y `hotfix/` y tags SemVer. Como oportunidades de mejora, se acordó unir las feature branches a `develop` con más frecuencia (varias ramas de los Web Services acumularon más de cien commits sin unir) y mantener Jira al día con el estado real de cada tarea. |
| **Sprint Goal & User Stories** | |
| **Sprint 3 Goal** | **Our focus is on** delivering the first deployed version of the DoofPlus RESTful Web Services for organizations, subscriptions, manufacturing, IoT monitoring and quality, documented with OpenAPI.<br>**We believe it delivers** a real backend that the Web Application can use instead of the Fake API, together with a website that takes each segment to its own environment, **to** QA/QC specialists and production supervisors of small and medium-sized pharmaceutical laboratories.<br>**This will be confirmed when** the API is published on Render with its database on Railway, its Swagger documentation lists the endpoints of each bounded context and a contact inquiry sent through the API is stored. |
| **Sprint 3 Velocity** | 34 Story Points |
| **Sum of Story Points** | 34 Story Points (TS12: 3, TS09: 5, TS07: 5, TS03: 5, TS10: 5, TS11: 5, TS02: 3, US48: 2, US04: 1) |

#### 5.2.3.2. Aspect Leaders and Collaborators

En el Sprint 3 se consideraron el Website y la Web Application y, en los RESTful Web Services, los bounded contexts (Shared & IAM, Organizations, Subscriptions, Manufacturing, IoT Monitoring y Quality & Compliance), las releases y el despliegue, y la documentación. El líder (L) de cada aspecto es el integrante con más commits en él, según el historial de los repositorios.

| Team Member (Last Name, First Name) | GitHub Username | Website | Web Application | Shared & IAM | Organizations | Subscriptions | Manufacturing | IoT Monitoring | Quality & Compliance | Releases & Deployment | Documentation |
|-------------------------------------|-----------------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Angulo Ramírez, Marcelo Martín | Zock2005 | | | | | | | L | | | C |
| Cobades Zamora, Yhoshua Hebert | YhoshuaCZ | C | L | C | L | | | | C | L | C |
| Flores Martinez, Ricardo Andres | Nitoryu28 | | | | | | | | L | | |
| Rojas Ambicho, Nestor Daniel | danRO-20 | L | C | L | | L | | | | C | L |
| Torres Juárez, Alisee Muriel | lLisee1 | | | | C | | | | | | C |
| Zavaleta Gutierrez, Rodolfo Martin | gutierrezrodolfo360-bit | C | C | C | | | L | | | C | C |

#### 5.2.3.3. Sprint Backlog 3

El objetivo del Sprint fue entregar la primera versión desplegada de los RESTful Web Services. El Sprint Backlog 3 junta tres bloques: las mejoras del Website y de la Web Application hechas desde el 18/10 (T184 a T198), las tareas de los Web Services por Technical Story (T137 a T165) y la autenticación con JWT (TS02, T199 a T201). Una tarea está en *Done* solo cuando su rama se unió a `develop`; lo que no se termine pasa al Sprint 4. Al cierre del Sprint hay 42 tareas en *Done*, 2 en *In-Process* y 3 en *To-do*, con 177 horas estimadas en total.

![Sprint Backlog 3 en Jira](assets/img/chapter5/evidencia/jira-sprint3.png)

**Enlace al board en Jira:** https://doofplus.atlassian.net/jira/software/projects/UPC/boards/3

| Sprint # | Sprint 3 | | | | | | |
|----------|----------|---|---|---|---|---|---|
| **User Story** | | **Work-Item / Task** | | | | | |
| **Id** | **Title** | **Id** | **Title** | **Description** | **Estimation (Hours)** | **Assigned To** | **Status (To-do / In-Process / To-Review / Done)** |
| TS12 | API de organizaciones y consultas de contacto | T137 | Organizations: dominio y persistencia | Completar los aggregates Organization, UserProfile y ContactInquiry con sus value objects y repositorios Spring Data JPA (rama feature/organizations). | 4 | Cobades Zamora, Yhoshua Hebert | Done |
| TS12 | API de organizaciones y consultas de contacto | T138 | Organizations: servicios de aplicación | Implementar los command services y query services de registro de la organización, perfiles y consultas de contacto. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| TS12 | API de organizaciones y consultas de contacto | T139 | Organizations: endpoints REST | Exponer /api/v1/organizations, /api/v1/user-profiles y POST /api/v1/contact-inquiries con resources, assemblers y documentación OpenAPI. | 4 | Cobades Zamora, Yhoshua Hebert | Done |
| TS12 | API de organizaciones y consultas de contacto | T140 | Organizations: fachada ACL | Implementar OrganizationsContextFacade para que Subscriptions consulte la organización sin acceder a su modelo. | 2 | Cobades Zamora, Yhoshua Hebert | To-do |
| TS12 | API de organizaciones y consultas de contacto | T141 | Web App: registro de organización y contacto contra el API | Reemplazar la Fake API en el módulo organizations de la Web Application (US50, US04). | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| TS09 | API de suscripciones y pagos | T142 | Subscriptions: revisión e integración en develop | Revisar feature/subscriptions, corregir observaciones y fusionarla en develop. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| TS09 | API de suscripciones y pagos | T143 | Subscriptions: pago con Niubiz | Agregar el pago de la suscripción: POST /api/v1/subscriptions/{id}/payments con el sandbox de Niubiz; responde 503 si la pasarela no está disponible y no registra el pago. | 5 | Rojas Ambicho, Nestor Daniel | Done |
| TS09 | API de suscripciones y pagos | T144 | Subscriptions: renovación | Agregar la renovación de la suscripción (US53) junto a la activación y cancelación existentes. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| TS09 | API de suscripciones y pagos | T145 | Web App: planes, suscripción y pago contra el API | Usar el API en el módulo subscriptions de la Web Application: planes, suscripción, pago con Niubiz, cambio de plan y facturas desde los pagos (US51, US52, US53). | 3 | Rojas Ambicho, Nestor Daniel | Done |
| TS09 | API de suscripciones y pagos | T146 | Subscriptions: pruebas | Pruebas unitarias del dominio y pruebas de integración de los endpoints de planes, suscripciones y pagos. | 3 | Rojas Ambicho, Nestor Daniel | Done |
| TS07 | API de operaciones de laboratorio | T147 | Manufacturing: productos y fórmulas maestras (dominio) | Implementar los aggregates Product y MasterFormula con sus value objects y repositorios JPA. | 4 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| TS07 | API de operaciones de laboratorio | T148 | Manufacturing: endpoints de productos y fórmulas | Servicios y endpoints /api/v1/products y /api/v1/master-formulas con documentación OpenAPI (US35, US36). | 4 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| TS07 | API de operaciones de laboratorio | T149 | IoT Monitoring: equipos, calibraciones y mantenimientos | Servicios y endpoints /api/v1/equipment con calibraciones y mantenimientos; DELETE responde 409 si el equipo está asociado a un lote en curso (US37, US38, US39). | 5 | Angulo Ramírez, Marcelo Martín | In-Process |
| TS07 | API de operaciones de laboratorio | T150 | IoT Monitoring: sensores y telemetría | Servicios y endpoints /api/v1/sensors para el inventario de sensores (US23) y POST /api/v1/telemetry para recibir las lecturas de ThingsBoard con X-Api-Key; una lectura fuera de rango abre una alerta. | 3 | Angulo Ramírez, Marcelo Martín | Done |
| TS07 | API de operaciones de laboratorio | T151 | Web App: productos, fórmulas y equipos contra el API | Reemplazar la Fake API en los módulos manufacturing (productos y fórmulas) e iot-monitoring (equipos y dispositivos). | 3 | Angulo Ramírez, Marcelo Martín | Done |
| TS03 | API de trazabilidad de lotes | T152 | Manufacturing: órdenes, lotes y materias primas (dominio) | Implementar los aggregates ProductionOrder, ProductionBatch y RawMaterialLot con sus estados y repositorios JPA. | 5 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| TS03 | API de trazabilidad de lotes | T153 | Manufacturing: endpoints de órdenes y lotes | Endpoints /api/v1/production-orders y /api/v1/production-batches: registro (409 si el número de lote ya existe), cambio de estado con los estados de la Web Application (start, resume, release y progreso), GET /{batchId} con su línea de tiempo, y registro de las incidencias, eventos y consumos de cada lote (US57, US14, US15, US16). | 5 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| TS03 | API de trazabilidad de lotes | T154 | Manufacturing: recepción y asociación de materias primas | Endpoints de recepción de materias primas, que dejan el lote en SAMPLING/PENDING, y su asociación a un lote de producción (US58, US17). | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| TS03 | API de trazabilidad de lotes | T155 | Manufacturing: incidencias y escalamiento a Calidad | Registrar incidencias de un lote y publicar el domain event que Quality usa para abrir una desviación (US56). | 3 | Angulo Ramírez, Marcelo Martín | In-Process |
| TS03 | API de trazabilidad de lotes | T156 | Manufacturing: fachada ACL | Implementar ManufacturingContextFacade para que Quality e IoT Monitoring consulten lotes y equipos. | 2 | Cobades Zamora, Yhoshua Hebert | To-do |
| TS03 | API de trazabilidad de lotes | T157 | Web App: trazabilidad de lotes contra el API | Reemplazar la Fake API en el módulo manufacturing (órdenes, lotes, materias primas e incidencias). | 4 | Cobades Zamora, Yhoshua Hebert | Done |
| TS10 | API de documentación de calidad | T158 | Quality: servicios de documentación | Implementar los command y query services de QualityDocument: registro, nuevas versiones y aprobación (US09, US10, US12, US13). | 4 | Flores Martinez, Ricardo Andres | Done |
| TS10 | API de documentación de calidad | T159 | Quality: endpoints de documentación | Implementar QualityDocumentController: POST /api/v1/quality-documents responde 201 con la versión 1.0 y GET /{id} inexistente responde 404; documentación OpenAPI. | 3 | Flores Martinez, Ricardo Andres | Done |
| TS10 | API de documentación de calidad | T160 | Web App: documentación de calidad contra el API | Reemplazar la Fake API en las vistas de protocolos, SOP y versiones del módulo quality. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| TS11 | API de desviaciones y CAPA | T161 | Quality: servicios de desviaciones y CAPA | Implementar los servicios de Deviation, CapaPlan y CapaAction: registro, causa raíz, acciones y cierre (US18, US19, US20, US21). | 5 | Flores Martinez, Ricardo Andres | Done |
| TS11 | API de desviaciones y CAPA | T162 | Quality: endpoints de desviaciones y CAPA | Implementar DeviationController, CapaPlanController y CapaActionController; PATCH /api/v1/deviations/{id}/close sin causa raíz responde 422. | 4 | Flores Martinez, Ricardo Andres | Done |
| TS11 | API de desviaciones y CAPA | T163 | Quality: desviación desde incidencia de Producción | Policy que abre una desviación cuando Manufacturing escala una incidencia (US56). | 2 | Flores Martinez, Ricardo Andres | To-do |
| TS11 | API de desviaciones y CAPA | T164 | Web App: desviaciones y CAPA contra el API | Reemplazar la Fake API en las vistas de desviaciones y CAPA del módulo quality. | 3 | Cobades Zamora, Yhoshua Hebert | Done |
| — | Tareas técnicas | T165 | Despliegue del RESTful API | Publicar el RESTful API en Render con la base de datos MySQL en Railway y la documentación Swagger accesible; configurar la URL del API en la Web Application. | 4 | Rojas Ambicho, Nestor Daniel | Done |
| US48 | Acceso por segmento a la Web Application | T184 | Website: sección Call to action | Implementar la sección Call to action con sus estilos y sus textos en en.json y es.json. | 3 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US48 | Acceso por segmento a la Web Application | T185 | Website: CTA por segmento y enlaces a la Web App | Mostrar un CTA por segmento y enlazar los botones de acceso y registro con el entorno correspondiente de la Web Application. | 3 | Rojas Ambicho, Nestor Daniel | Done |
| — | Tareas técnicas | T186 | Website: redes sociales en el footer | Agregar los enlaces a las redes sociales de DoofPlus en el footer. | 2 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| — | Tareas técnicas | T187 | Website: release v2.1.0 y publicación con GitHub Actions | Preparar release/v2.1.0 y publicar el Website en GitHub Pages con un workflow de GitHub Actions. | 3 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| — | Tareas técnicas | T188 | Website: hotfix v2.1.1 | Corregir los enlaces del Website publicado y etiquetar v2.1.1. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US04 | Formulario de contacto | T189 | Website: estilos de contacto, footer y release v2.2.0 | Ajustar los estilos de la sección de contacto y el footer con la organización de GitHub, y publicar v2.2.0. | 4 | Cobades Zamora, Yhoshua Hebert | Done |
| — | Tareas técnicas | T190 | Web App: correcciones de las pruebas de QA | Aplicar las observaciones de las pruebas de QA de la Web Application. | 4 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| US48 | Acceso por segmento a la Web Application | T191 | Web App: enlaces de la Web App al Website | Enlazar el sign-in y la zona pública de la Web Application con el Website. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| — | Tareas técnicas | T192 | Web App: traducción de los permisos por rol | Traducir los permisos de cada rol en inglés y español. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| — | Tareas técnicas | T193 | Web App: búsqueda global por código | Buscar lotes, órdenes, documentos y desviaciones por su código desde la barra superior. | 4 | Rojas Ambicho, Nestor Daniel | Done |
| — | Tareas técnicas | T194 | Web App: hotfix v1.0.2 | Corregir la Web Application publicada y etiquetar v1.0.2. | 2 | Rojas Ambicho, Nestor Daniel | Done |
| US04 | Formulario de contacto | T195 | Web App: Contact us en la zona pública | Implementar Contact us en la zona pública del sign-in con validación y envío de la consulta. | 6 | Cobades Zamora, Yhoshua Hebert | Done |
| — | Tareas técnicas | T196 | Web App: release v1.1.0 y despliegue en Firebase | Preparar release/v1.1.0 y publicar la Web Application en Firebase Hosting. | 2 | Cobades Zamora, Yhoshua Hebert | Done |
| — | Tareas técnicas | T197 | Platform: configuración del proyecto y capa shared | Crear el proyecto Spring Boot con su configuración, OpenAPI y la capa shared. | 6 | Zavaleta Gutierrez, Rodolfo Martin | Done |
| — | Tareas técnicas | T198 | Platform: shared con Result y ApplicationError | Agregar Result, ApplicationError y los assemblers de errores a la capa shared. | 6 | Rojas Ambicho, Nestor Daniel | Done |
| TS02 | Autenticación JWT en el RESTful API | T199 | IAM: dominio y persistencia de User y Role | Implementar los aggregates User y Role con sus repositorios JPA y la carga inicial de roles. | 10 | Cobades Zamora, Yhoshua Hebert | Done |
| TS02 | Autenticación JWT en el RESTful API | T200 | IAM: sign-up y sign-in con JWT | Exponer sign-up y sign-in que devuelven un JWT y filtrar las rutas por rol. | 10 | Cobades Zamora, Yhoshua Hebert | Done |
| TS02 | Autenticación JWT en el RESTful API | T201 | Web App: sign-in contra el API | Iniciar sesión en la Web Application contra el API y enviar el token en cada petición. | 6 | Cobades Zamora, Yhoshua Hebert | Done |

#### 5.2.3.4. Development Evidence for Sprint Review

En el Sprint 3 se trabajó en cuatro repositorios siguiendo GitFlow: una feature branch por sección del Website, por mejora de la Web Application o por bounded context de los Web Services, integradas en `develop` con merges `--no-ff`, y ramas `release/` y `hotfix/` fusionadas en `main` con su tag. El Website pasó por `v2.1.0`, `v2.1.1` y `v2.2.0`; la Web Application, por `v1.0.2` y `v1.1.0`, y los RESTful Web Services tuvieron su primera versión, `v1.0.0`. Las tablas siguientes presentan los commits de `main` del Sprint (desde el 18/10/2026); la columna *Branch* indica la rama en que se realizó cada commit. El curso de Responsabilidad Social se trabaja en `develop` de su repositorio, que todavía no tiene release.

**Website** (55 commits)

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/doofplus-website | feature/call-to-action-section | `ac5f52e` | feat(cta): add final call to action section with quick access links | — | 26/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `bf072bf` | feat(cta): add styles for final call to action section with quick access links | — | 26/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `96d7eb0` | feat(i18n): add call to action section translations for English and Spanish | — | 26/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `37251bf` | fix(cta): update launch button segment to sign-in for better user flow | — | 26/10/2026 |
| IngesCompany/doofplus-website | develop | `37586cf` | Merge branch 'feature/call-to-action-section' into develop | — | 26/10/2026 |
| IngesCompany/doofplus-website | feature/footer-social-media | `5f54282` | feat(footer): add social media links and direct contact channels | — | 26/10/2026 |
| IngesCompany/doofplus-website | develop | `f60293c` | Merge branch 'feature/footer-social-media' into develop | — | 26/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `c55beec` | feat(workspace): show the segment cards as information only | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `288dc56` | feat(plans): show the plans as information only | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `a8b1e5a` | feat(cta): add a call to action for each segment | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `6898ccf` | feat(navbar): lead get started to the call to action | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `4f4e65f` | refactor(contact): remove the contact section | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/call-to-action-section | `57d880a` | fix(footer): center the social media icons | — | 30/10/2026 |
| IngesCompany/doofplus-website | develop | `b5f87eb` | Merge branch 'feature/call-to-action-section' into develop | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/web-app-links | `ecb1fb9` | feat(config): open the local web application from localhost | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/web-app-links | `63490ab` | chore: remove unused boilerplate files | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/web-app-links | `a4159bb` | docs: add readme and project license | — | 30/10/2026 |
| IngesCompany/doofplus-website | feature/web-app-links | `8e1c5c8` | style: use the doofplus shield as favicon | — | 30/10/2026 |
| IngesCompany/doofplus-website | develop | `326c6ac` | Merge branch 'feature/web-app-links' into develop | — | 30/10/2026 |
| IngesCompany/doofplus-website | release/v2.1.0 | `a03bafb` | chore: remove npm, the site is served as static files | — | 31/10/2026 |
| IngesCompany/doofplus-website | release/v2.1.0 | `8d15baa` | refactor: move the pages into public and keep the assets in scripts, styles, images and i18n | — | 31/10/2026 |
| IngesCompany/doofplus-website | release/v2.1.0 | `096c806` | ci(deploy): publish the public folder on GitHub Pages | — | 31/10/2026 |
| IngesCompany/doofplus-website | release/v2.1.0 | `a92b371` | docs(readme): describe the public folder structure and how to run the site without npm | — | 31/10/2026 |
| IngesCompany/doofplus-website | release/v2.1.0 | `9dd1eed` | docs: add CHANGELOG.md and CONTRIBUTING.md files | — | 31/10/2026 |
| IngesCompany/doofplus-website | release/v2.1.0 | `f0d572e` | docs: update CHANGELOG.md | — | 31/10/2026 |
| IngesCompany/doofplus-website | main | `be9ea4e` | Merge branch 'release/v2.1.0' into main | — | 31/10/2026 |
| IngesCompany/doofplus-website | main | `567cd5d` | Merge branch 'release/v2.1.0' into main | — | 31/10/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `b90947c` | style: remove the styles of the deleted contact section | — | 31/10/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `bd6b827` | chore: remove robots.txt, .nojekyll and the boilerplate 404 page | — | 31/10/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `6e52a4d` | refactor: share the header and footer of every page through partials | — | 31/10/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `09e7da3` | fix(team): update team member images to use consistent naming convention | — | 01/11/2026 |
| IngesCompany/doofplus-website | hotfix/v2.1.1 | `bf0c154` | fix: point the links to the new organization | — | 01/11/2026 |
| IngesCompany/doofplus-website | hotfix/v2.1.1 | `5c4470f` | docs: update the changelog for version 2.1.1 | — | 01/11/2026 |
| IngesCompany/doofplus-website | main | `6fbd40a` | Merge branch 'hotfix/v2.1.1' | — | 01/11/2026 |
| IngesCompany/doofplus-website | develop | `dbd2469` | Merge branch 'hotfix/v2.1.1' into develop | — | 01/11/2026 |
| IngesCompany/doofplus-website | fix/contact-styles | `c7d43c9` | fix(styles): remove the unused contact form styles | — | 02/11/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `3e26329` | refactor(scripts): rename component files and update import paths for consistency | — | 02/11/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `ad5530f` | refactor(cursor): update cursor file paths for consistency and remove unnecessary directory | — | 02/11/2026 |
| IngesCompany/doofplus-website | fix/public-static-site | `19ac275` | feat(team): add Alisee Torres member to the team section and update role descriptions for consistency | — | 02/11/2026 |
| IngesCompany/doofplus-website | develop | `e926cba` | Merge branch 'fix/contact-styles' into develop | — | 02/11/2026 |
| IngesCompany/doofplus-website | develop | `5903961` | Merge branch 'fix/public-static-site' into develop | — | 02/11/2026 |
| IngesCompany/doofplus-website | fix/contributing-title | `6a60629` | docs(contributing): use the doofplus-website repository name in the title (W-026) | — | 07/11/2026 |
| IngesCompany/doofplus-website | develop | `4dc7925` | Merge branch 'fix/contributing-title' into develop | — | 07/11/2026 |
| IngesCompany/doofplus-website | fix/footer-github-org | `5417ba7` | fix(footer): point the github link to the ingescompany organization | — | 07/11/2026 |
| IngesCompany/doofplus-website | develop | `adb3505` | Merge branch 'fix/footer-github-org' into develop | — | 07/11/2026 |
| IngesCompany/doofplus-website | release/v2.2.0 | `8edef98` | docs: update the changelog for version 2.2.0 | — | 09/11/2026 |
| IngesCompany/doofplus-website | main | `a228dc5` | Merge branch 'release/v2.2.0' into main | — | 09/11/2026 |
| IngesCompany/doofplus-website | feature/legal-pages-back-link | `a93d3cb` | feat(legal): add a link back to the website on the terms and privacy pages | — | 14/11/2026 |
| IngesCompany/doofplus-website | develop | `c1cca2c` | Merge branch 'feature/legal-pages-back-link' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-website | feature/team-role-and-404 | `dc66a40` | fix(team): use the same role labels as the published team and add a 404 page | — | 14/11/2026 |
| IngesCompany/doofplus-website | develop | `34bd8e0` | Merge branch 'feature/team-role-and-404' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-website | feature/about-videos | `bdb23a4` | feat(videos): add the about the product and about the team videos | — | 15/11/2026 |
| IngesCompany/doofplus-website | release/v2.3.0 | `df898c2` | docs: update the changelog for version 2.3.0 | — | 15/11/2026 |
| IngesCompany/doofplus-website | develop | `b409505` | Merge branch 'feature/about-videos' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-website | develop | `02cc5c5` | Merge branch 'release/v2.3.0' into develop | — | 15/11/2026 |

**Web Application** (61 commits)

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `253858d` | refactor(overview): remove redundant invite user button | — | 28/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `92632ee` | fix(footer): open terms and privacy links in a new tab | — | 28/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `69881d3` | fix(i18n): translate dosage forms in product catalog and form | — | 28/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `3166ae6` | fix(iam): translate role permission previews in invitation form | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `b758dee` | fix(quality): populate change details for all audit trail events | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `ddefd88` | fix(quality): add snackbar feedback and lock state when saving capa root cause | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `cf7f00f` | fix(manufacturing): add validation feedback and success notification to material receipt | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `05f7787` | fix(quality): add removeEvidence method to avoid mistakes while uploading evidence | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | feature/qa-test-feedback | `d92cfc1` | fix(quality): translate evidence package metadata in audits | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | develop | `4f05e1c` | Merge branch 'feature/qa-test-feedback' into develop | — | 29/10/2026 |
| IngesCompany/doofplus-web-application | feature/landing-links | `7e5fdfe` | feat(navigation): link the public pages one level up and to the local landing page | — | 30/10/2026 |
| IngesCompany/doofplus-web-application | feature/landing-links | `106891d` | feat(registration): ask before leaving with unsaved data | — | 30/10/2026 |
| IngesCompany/doofplus-web-application | feature/landing-links | `35abc44` | style: use the doofplus shield as favicon | — | 30/10/2026 |
| IngesCompany/doofplus-web-application | develop | `b50ba5e` | Merge branch 'feature/landing-links' into develop | — | 30/10/2026 |
| IngesCompany/doofplus-web-application | fix/role-permission-translations | `976aece` | fix(i18n): translate the role permissions in the profile matrix | — | 31/10/2026 |
| IngesCompany/doofplus-web-application | develop | `2849511` | Merge branch 'fix/role-permission-translations' into develop | — | 31/10/2026 |
| IngesCompany/doofplus-web-application | feature/global-search | `f1d1e13` | feat(shell): search a record by its exact code from the top bar | — | 31/10/2026 |
| IngesCompany/doofplus-web-application | feature/global-search | `ad9d91c` | feat(quality): open the document and the batch given in the url | — | 31/10/2026 |
| IngesCompany/doofplus-web-application | develop | `06deb35` | Merge branch 'feature/global-search' into develop | — | 31/10/2026 |
| IngesCompany/doofplus-web-application | hotfix/v1.0.2 | `8f36f0c` | fix(environment): link the website published by the new organization | — | 01/11/2026 |
| IngesCompany/doofplus-web-application | hotfix/v1.0.2 | `5f0c52a` | chore(release): set the web application version to 1.0.2 and update the changelog | — | 01/11/2026 |
| IngesCompany/doofplus-web-application | main | `bf120b7` | Merge branch 'hotfix/v1.0.2' | — | 01/11/2026 |
| IngesCompany/doofplus-web-application | develop | `d34183f` | Merge branch 'hotfix/v1.0.2' into develop | — | 01/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `dfe1043` | feat(organizations): add contact inquiries to the fake api | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `aa50d8c` | feat(organizations): add contact inquiry entity, assembler and api endpoint | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `ec7a0a7` | feat(organizations): send contact inquiries from the organizations store | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `00db3b8` | feat(i18n): add contact us translations | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `152096b` | feat(organizations): add the public contact us view and route | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `a4aa4bd` | feat(shell): link contact us from the public header and the sign-in page | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `366c034` | fix(organizations): show the office city without a country in the contact panel | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | develop | `30c0946` | Merge branch 'feature/contact-inquiry' into develop | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-inquiry | `41a3518` | style(organizations): match the contact us look of the aw frontend | Teal panel with the forum icon and label, check_circle topics, form inside a card with a full-width button, 64 px check on the confirmation and a 1100 px bre… | 02/11/2026 |
| IngesCompany/doofplus-web-application | develop | `17465b8` | Merge branch 'feature/contact-inquiry' into develop | — | 02/11/2026 |
| IngesCompany/doofplus-web-application | feature/contact-us-estilo-aw | `cea8525` | style(organizations): match the aw contact us look in fields, card shadow and footer | — | 04/11/2026 |
| IngesCompany/doofplus-web-application | develop | `5195e7a` | Merge branch 'feature/contact-us-estilo-aw' into develop | — | 04/11/2026 |
| IngesCompany/doofplus-web-application | fix/contact-us-title-line-height | `4a22393` | fix(organizations): give the contact us titles their own line height so they do not overlap on mobile | — | 07/11/2026 |
| IngesCompany/doofplus-web-application | develop | `68a5477` | Merge branch 'fix/contact-us-title-line-height' into develop | — | 07/11/2026 |
| IngesCompany/doofplus-web-application | fix/contributing-title | `c40dbef` | docs(contributing): use the doofplus-web-application repository name in the title (W-026) | — | 07/11/2026 |
| IngesCompany/doofplus-web-application | develop | `99fcc80` | Merge branch 'fix/contributing-title' into develop | — | 07/11/2026 |
| IngesCompany/doofplus-web-application | release/v1.1.0 | `f13d1a1` | chore(release): prepare version 1.1.0 | — | 09/11/2026 |
| IngesCompany/doofplus-web-application | main | `59dde7a` | Merge branch 'release/v1.1.0' into main | — | 09/11/2026 |
| IngesCompany/doofplus-web-application | feature/connect-platform-api | `fb0dfc6` | feat(platform): connect organizations and iot monitoring to the doofplus platform api | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | develop | `d43c34f` | Merge branch 'feature/connect-platform-api' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | release/v1.2.0 | `7eb7960` | chore(release): prepare version 1.2.0 | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | develop | `27ccc98` | Merge branch 'release/v1.2.0' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | feature/subscriptions-platform-api | `27dc6cc` | feat(subscriptions): use the platform api for plans, subscriptions, payments and plan changes | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | develop | `100b2c6` | Merge branch 'feature/subscriptions-platform-api' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | feature/iam-real-api | `750b36b` | feat(iam): sign in with the iam of the doofplus platform | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | develop | `3fca89f` | Merge branch 'feature/iam-real-api' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | feature/translated-workspace-texts | `7af696f` | feat(i18n): translate the toasts, labels and not found page of the workspace | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | develop | `34e6a4f` | Merge branch 'feature/translated-workspace-texts' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-web-application | feature/manufacturing-platform-api | `eeeec92` | feat(manufacturing): use the platform API for products, formulas, orders, batches and lots | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | develop | `d0d1065` | Merge branch 'feature/manufacturing-platform-api' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | feature/quality-platform-api | `74b3fb8` | feat(quality): use the platform API for the Quality and Compliance records | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | develop | `3fba861` | Merge branch 'feature/quality-platform-api' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | release/v1.3.0 | `b9537bc` | chore(release): prepare version 1.3.0 | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | develop | `a9537cd` | Merge branch 'release/v1.3.0' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | feature/invitations-and-roles-api | `4ba4037` | feat(iam): load the invitations and role profiles from the platform | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | develop | `841c481` | Merge branch 'feature/invitations-and-roles-api' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | release/v1.4.0 | `674f818` | chore(release): prepare version 1.4.0 | — | 15/11/2026 |
| IngesCompany/doofplus-web-application | develop | `37af48f` | Merge branch 'release/v1.4.0' into develop | — | 15/11/2026 |

**RESTful Web Services** (394 commits)

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/doofplus-platform | main | `f878fc4` | chore: initial commit | — | 20/10/2026 |
| IngesCompany/doofplus-platform | feature/project-configuration | `55b128f` | docs: add project-level documentation files | — | 20/10/2026 |
| IngesCompany/doofplus-platform | feature/project-configuration | `af308fd` | docs: add initial reference documentation to README | — | 20/10/2026 |
| IngesCompany/doofplus-platform | develop | `75bb286` | Merge branch 'feature/project-configuration' into develop | — | 20/10/2026 |
| IngesCompany/doofplus-platform | feature/shared | `ca6fe28` | feat(conventions): add Snake Case Naming strategy | — | 25/10/2026 |
| IngesCompany/doofplus-platform | feature/shared | `9663ba2` | feat(result): add base implementation of Result pattern | — | 25/10/2026 |
| IngesCompany/doofplus-platform | feature/shared | `2ae3b5f` | feat(orm): configure ORM parameters | — | 25/10/2026 |
| IngesCompany/doofplus-platform | develop | `61e3f0d` | Merge branch 'feature/shared' into develop | — | 25/10/2026 |
| IngesCompany/doofplus-platform | release/v1.0.0 | `a31af48` | chore: update README.md | — | 25/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `5085fe6` | feat(subscriptions): add aggregate Subscription | — | 26/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `e0654cc` | feat(facility): add initial Facility value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `405df6f` | feat(subscriptions): add PlanKey value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | release/v1.0.0 | `ba1f579` | chore: update README.md | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `45c8186` | fix(subscriptions): use plan message keys in PlanKey value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `6f952f4` | feat(subscriptions): add OrganizationId value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `f6c9aad` | feat(subscriptions): add BillingEmail value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `c4fafa5` | feat(subscriptions): add Money embeddable value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `80eb72c` | feat(subscriptions): add PaymentCard embeddable value object | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `836489d` | feat(subscriptions): add BillingCycle and SubscriptionStatus enums | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `d79f43d` | feat(subscriptions): add PlanKey, OrganizationId and BillingEmail attribute converters | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `46b9408` | feat(subscriptions): add plan and subscription commands | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `b1fc863` | feat(subscriptions): add Plan aggregate | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `0f7e6d1` | feat(subscriptions): implement Subscription aggregate | — | 27/10/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `deee12a` | feat(production-batch): add BatchNumber value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `5535222` | feat(production-batch): add Quantity value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `7015d20` | feat(subscriptions): add plan and subscription queries | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `ee08cf6` | feat(subscriptions): add PlanRepository and SubscriptionRepository | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `8d3db98` | feat(alert): introduce AlertCode value object with validation | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `97ef59e` | feat(alert): add documentation for AlertCode value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `11ee64c` | Merge branch 'develop' into feature/monitoring | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `354e05d` | feat(device): introduce DeviceId value object with validation | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `574fd9e` | feat(device): add documentation for DeviceId value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `cc1343c` | feat(monitoring): introduce EquipmentCode value object with validation | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `5b4d72e` | feat(monitoring): add documentation for EquipmentCode value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `30516d1` | feat(monitoring): introduce Facility value object with validation | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ed7cbae` | feat(monitoring): add documentation for Facility value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2fc4478` | feat(monitoring): introduce SensorCode value object with validation | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7a046e8` | feat(monitoring): add documentation for SensorCode value object | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `b274df8` | feat(monitoring): introduce CalibrationStatus value object for equipment status | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `a94f90f` | feat(subscriptions): implement command and query services for plans and subscriptions | — | 28/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `14ac422` | feat(subscriptions): add resources and assemblers for plans and subscriptions | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `b54b68c` | feat(monitoring): introduce GetAllAlertsQuery for retrieving all monitoring alerts | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `f6014d0` | feat(monitoring): introduce GetAllEquipmentQuery for retrieving all equipment | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `af4cb80` | feat(monitoring): introduce GetAllReadingsQuery for retrieving all telemetry readings | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ce68eb2` | feat(monitoring): introduce GetAlertByCodeQuery for retrieving a monitoring alert by alert code | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `44f1951` | feat(monitoring): introduce GetAlertByIdQuery for retrieving a monitoring alert by ID | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2f15aa9` | feat(monitoring): introduce GetAllAlertsByBatchCodeQuery for retrieving alerts by batch code | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `1f47f70` | feat(monitoring): introduce GetAllAlertsBySensorCodeQuery for retrieving alerts by sensor code | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `75032a7` | feat(monitoring): introduce GetAllAlertsBySensorCodeQuery for retrieving alerts by sensor code | — | 29/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `9d51e64` | feat(monitoring): introduce GetAllReadingsBySensorCodeQuery for retrieving readings by sensor code | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2ad45da` | feat(monitoring): introduce GetAllSensorsByEquipmentCodeQuery for retrieving sensors by equipment code | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `934ffb0` | feat(monitoring): introduce GetAllSensorsQuery for retrieving all registered IoT sensors | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `95b4b97` | feat(monitoring): introduce GetEquipmentByCodeQuery for retrieving equipment by equipment code | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `b2997ba` | feat(subscriptions): implement PlansController and SubscriptionsController | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a7cbca1` | feat(monitoring): introduce GetEquipmentByIdQuery for retrieving equipment by ID | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `dc2aa2c` | feat(monitoring): introduce GetReadingByIdQuery for retrieving telemetry reading by ID | — | 30/10/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `defc701` | feat(configuration): add subscriptions error messages | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `fe592de` | feat(organizations): implement domain model, Ruc value object and repository | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `907b38e` | feat(production-batch): add BatchNumber attribute converter | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `3901680` | feat(monitoring): update AlertCode to increase max length and improve validation messages | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7d35f1e` | feat(monitoring): enhance DeviceId validation with improved error messages | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `c1c42a4` | feat(monitoring): improve Facility location validation with constants for error messages | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `5d590aa` | feat(monitoring): refactor SensorCode validation to use constants for error messages | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7ff0ce0` | feat(monitoring): refactor EquipmentCode validation to use constants for error messages | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `e9746f3` | feat(monitoring): simplify CalibrationStatus from method with streamlined logic | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `b2633d8` | feat(monitoring): add value object representations for AlertCode, CalibrationStatus, DeviceId, EquipmentCode, Facility, and SensorCode | — | 31/10/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `d5f1dfa` | feat(production-batch): implement CreateBatch Command | — | 01/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `e46dacb` | feat(manufacturing): add IncidentSeverity enumeration | — | 01/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `414e45a` | feat(manufacturing): add RegisterIncident Command | — | 01/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `724f0ea` | feat(production-batch): add CloseBatch Command for closing batches | — | 01/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `9563438` | feat(manufacturing): add BatchStatus enumeration for batch lifecycle management | — | 02/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `4696525` | feat(manufacturing): add query for searching batches by their identifier | — | 02/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `2e538fe` | feat(manufacturing): add query for retrieving a batch by its number | — | 02/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `7ee29b0` | feat(manufacturing): add query for retrieving all batches | — | 02/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `b1d8658` | feat(quality): add deviation and CAPA status enums | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `140f86a` | feat(quality): add batch release and document status enums | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e6fc60b` | feat(quality): add analytical result audit and report enums | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `923766c` | feat(quality): add deviation and CAPA aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `540b9b3` | feat(quality): add batch release aggregate | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `5916647` | feat(quality): add quality documents and evidence aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d842fd6` | feat(quality): add analytical result aggregate | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `110dd21` | feat(quality): add audit and audit finding aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `0323f27` | feat(quality): add audit event aggregate | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `67aa8a7` | feat(quality): add regulatory report aggregate | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `0229c2a` | feat(quality): add collaboration task and comment aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `7fabc8a` | feat(quality): add traceability gap aggregate | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `f826d15` | feat(quality): add deviation and CAPA domain repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `f9de05b` | feat(quality): add batch release domain repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `974e796` | feat(quality): add document and evidence domain repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `ef50952` | feat(quality): add analytical result domain repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `df25e48` | feat(quality): add audit domain repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `15670cb` | feat(quality): add regulatory report domain repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `ac90aa5` | feat(quality): add collaboration domain repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `1b552e8` | feat(quality): add traceability gap domain repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `b9b8507` | feat(quality): add deviation and CAPA JPA repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `889c1de` | feat(quality): add batch release JPA repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `106c6a3` | feat(quality): add document and evidence JPA repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `b437f4a` | feat(quality): add analytical result JPA repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d014dc8` | feat(quality): add audit JPA repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e2ff614` | feat(quality): add regulatory report JPA repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `8830c5f` | feat(quality): add collaboration JPA repositories | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `1d08e6f` | feat(quality): add traceability gap JPA repository | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `2b19323` | feat(quality): add interfaces | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `9fd5a28` | feat(quality): add acl | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `96aaff6` | feat(quality): add commands services | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `eebd9c2` | feat(quality): add query services | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `c3ef732` | feat(monitoring): add CreateAlertCommand for creating monitoring alerts | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `55fbfb2` | feat(monitoring): add CreateEquipmentCommand for creating equipment identification | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `00b4d77` | feat(monitoring): add CreateReadingCommand for creating reading function | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `4348c30` | feat(monitoring): add CreateSensorCommand for creating sensor readibility | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2a08e27` | feat(monitoring): add UpdateAlertCommand for updatining an alert message | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7ed8e67` | feat(monitoring): add UpdateEquipmentCommand for update equipment registration | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `5db100b` | feat(monitoring): add UpdateSensorCommand for update sensors detection | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `57f4e28` | feat(monitoring): add AlertRepository for managing alert aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a29bb08` | feat(monitoring): add EquipmentRepository for managing equipment aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `4442c5b` | feat(monitoring): add ReadingRepository for managing reading aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2b2e039` | feat(monitoring): add SensorRepository for managing sensor aggregates | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `19c62f5` | feat(monitoring): add AlertCodeAttributeConverter for AlertCode persistence | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `8748207` | feat(monitoring): add CalibrationStatusAttributeConverter for CalibrationStatus persistence | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `5eec8b1` | feat(monitoring): add DeviceIdAttributeConverter for DeviceId persistence | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a6deb4e` | feat(monitoring): add EquipmentCodeAttributeConverter for EquipmentCode persistence | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `694b752` | feat(monitoring): add FacilityAttributeConverter for Facility persistence | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `e0cb109` | feat(monitoring): add SensorCodeAttributeConverter for SensorCode persistence | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `75ae88c` | feat(monitoring): add Alert entity for telemetry alerts and monitoring anomalies | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `3af8456` | feat(monitoring): add Equipment entity for managing equipment details and maintenance | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `b90a02e` | feat(monitoring): add Reading entity for capturing IoT telemetry readings | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2fd788b` | feat(monitoring): add Sensor entity for managing IoT telemetry sensors | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `11ac224` | refactor(manufacturing): implement comments for understanding in java docs | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `e5d0120` | refactor(manufacturing): rename BatchNumberAttributeConverter to BatchNumberPersistenceConverter for clarity | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `b5b8f1f` | feat(monitoring): refactor AlertCode, CalibrationStatus, and DeviceId value objects for improved validation and UUID support | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `5a152db` | feat(manufacturing): add embeddable for Quantity value object to be persistent | — | 03/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `910208e` | build: pin lombok so the project compiles with java 27 | — | 04/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `1143cfd` | fix(subscriptions): enable jpa auditing so creation dates are saved | — | 05/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `69af5aa` | feat(shared): add application error and functional result | — | 05/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `f502aab` | fix(manufacturing): mark QuantityPersistenceEmbeddable as embeddable for persistence | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `6ab837d` | refactor(manufacturing): remove unnecessary import of jakarta.persistence.Embeddable from Quantity.java | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `310e33c` | feat(shared): add domain aggregate root and event publisher | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `6ddc877` | feat(manufacturing): add IncidentStatus enum for incident status representation | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `5f13809` | feat(manufacturing): add Incident entity to represent manufacturing incidents | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `fbdedb8` | feat(manufacturing): add MaterialConsumption entity to track material usage | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `fadd609` | feat(manufacturing): add MaterialConsumption entity to track material usage | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `51650c3` | feat(manufacturing): add MaterialConsumption entity to track material usage | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `a02e8f3` | fix(manufacturing): remove status parameter from Incident constructor | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `592faea` | feat(production-batch): add ProductionBatch aggregate root to manage production batches | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `a1f8282` | feat(shared): add auditable persistence entity and enable jpa auditing | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `888af88` | feat(monitoring): enhance validation for value objects and improve error handling | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `1e240d3` | feat(monitoring): add validation to command constructors for alerts, equipment, readings, and sensors | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `fc5bbd3` | feat(monitoring): add validation for alert, batch, sensor, and equipment query parameters | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `b37dc19` | feat(monitoring): add validation for alert, batch, sensor, and equipment query parameters | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `98c25c7` | refactor(monitoring): rename query classes for consistency and clarity | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `318f15d` | feat(monitoring): add queries for retrieving sensors by code and ID with validation | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ddbce2f` | feat(monitoring): add validation for ID in update commands for alerts, equipment, and sensors | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `34f5fa0` | feat(monitoring): enhance aggregate classes with validation and reconstitution methods | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ca085f9` | feat(monitoring): add AlertNotFoundException for handling missing alerts | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `c49c392` | feat(monitoring): add EquipmentNotFoundException for handling missing equipment | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `cc418b9` | feat(monitoring): add ReadingNotFoundException for handling missing readings | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `d80c4ff` | feat(shared): add plural snake case naming strategy for tables | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7cf1b01` | feat(monitoring): add SensorNotFoundException for handling missing sensors | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `76c960c` | feat(monitoring): add AlertRepository interface for managing Alert aggregates | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `4dda23f` | feat(monitoring): add EquipmentRepository interface for managing Equipment aggregates | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `e47b8a7` | feat(monitoring): add ReadingRepository interface for managing Reading aggregates | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `c956cb7` | feat(monitoring): add SensorRepository interface for managing Sensor aggregates | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `9bbd792` | feat(monitoring): add AlertCommandService and AlertQueryService interfaces for managing Alert commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `59eb1c8` | feat(monitoring): add EquipmentCommandService and EquipmentQueryService interfaces for managing Equipment commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `86d1896` | feat(monitoring): add ReadingCommandService and ReadingQueryService interfaces for managing Reading commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `3584997` | feat(monitoring): add SensorCommandService and SensorQueryService interfaces for managing Sensor commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `acb29c3` | feat(monitoring): add AlertCommandServiceImpl and AlertQueryServiceImpl for managing Alert commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2ed9ac2` | feat(monitoring): add EquipmentCommandServiceImpl and EquipmentQueryServiceImpl for managing Equipment commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `0311af8` | feat(monitoring): add ReadingCommandServiceImpl and ReadingQueryServiceImpl for managing Reading commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `4a60b2c` | feat(monitoring): add SensorCommandServiceImpl and SensorQueryServiceImpl for managing Sensor commands and queries | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `0d955e7` | feat(monitoring): improve null handling in attribute converters | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7965089` | feat(monitoring): add AlertPersistenceEntity for JPA persistence of alerts | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `fd9e45a` | feat(monitoring): add EquipmentPersistenceEntity for JPA persistence of equipment | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `f835d45` | feat(monitoring): add ReadingPersistenceEntity for JPA persistence of readings | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a5fcbda` | feat(monitoring): add SensorPersistenceEntity for JPA persistence of sensors | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `1d0ae45` | feat(monitoring): add AlertPersistenceRepository for JPA operations on alerts | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `861d8ee` | feat(shared): return errors as localized problem details | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ba1f07f` | feat(monitoring): add EquipmentPersistenceRepository for JPA operations on equipment | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2ce4ab8` | feat(monitoring): add EquipmentPersistenceRepository for JPA operations on equipment | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `0b9ff51` | feat(monitoring): add SensorPersistenceRepository for JPA operations on sensors | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `f614d3f` | feat(monitoring): add AlertPersistenceAssembler for converting between Alert and AlertPersistenceEntity | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a0cb20a` | feat(monitoring): add EquipmentPersistenceAssembler for converting between Equipment and EquipmentPersistenceEntity | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `6486d91` | feat(monitoring): add ReadingPersistenceAssembler for converting between Reading and ReadingPersistenceEntity | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ac61363` | feat(monitoring): add SensorPersistenceAssembler for converting between Sensor and SensorPersistenceEntity | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `bae6453` | feat(monitoring): implement AlertRepositoryImpl for JPA operations on alerts | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `1473344` | feat(monitoring): implement EquipmentRepositoryImpl for JPA operations on equipment | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a516389` | feat(monitoring): implement EquipmentRepositoryImpl for JPA operations on equipment | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `48ddaeb` | feat(monitoring): implement SensorRepositoryImpl for JPA operations on sensors | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `a4f1163` | chore(config): add dev and prod profiles, a dockerfile and shared settings | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-learning-center | `2c8a63d` | feat(shared): document the api with openapi and run on virtual threads | — | 06/11/2026 |
| IngesCompany/doofplus-platform | develop | `7621c3e` | Merge branch 'feature/shared-learning-center' into develop | — | 06/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `1df362c` | feat(monitoring): add AlertResource for monitoring alert representation | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `adbe54f` | feat(monitoring): add CreateAlertResource for creating monitoring alerts | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `e55e201` | feat(monitoring): add CreateEquipmentResource for creating equipment items | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `d1eefa8` | feat(monitoring): add CreateReadingResource for recording telemetry readings | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `585e345` | feat(monitoring): add CreateSensorResource for creating IoT sensors | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `bac4e80` | feat(monitoring): add EquipmentResource for equipment item representation | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `eadd8a1` | feat(monitoring): add ReadingResource for telemetry reading representation | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `451e287` | feat(monitoring): add SensorResource for IoT sensor representation | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `0bad7a7` | feat(monitoring): add UpdateAlertResource for updating monitoring alerts | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `3d47099` | feat(monitoring): add UpdateEquipmentResource for updating equipment items | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `6478a2f` | feat(monitoring): add UpdateSensorResource for updating IoT sensor details | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `2256efd` | feat(monitoring): add AlertResourceFromEntityAssembler for converting Alert domain to AlertResource | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `a09cdd6` | feat(exceptions): add BatchNotFoundException to handle missing batches | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `9527f32` | feat(repositories): add ProductionBatchRepository interface for managing production batches | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `44d20fd` | Merge branch 'develop' into feature/manufacturing | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `a3ea01c` | feat(infrastructure): add ProductionBatchPersistenceEntity for JPA mapping of production batches | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `9f600bf` | feat(repositories): add ProductionBatchPersistenceRepository for managing ProductionBatch entities | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `8b3fbaf` | feat(infrastructure): add ProductionBatchPersistenceAssembler for domain and persistence mapping | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `04b795f` | refactor(domain): move ProductionBatch to aggregates package and update imports | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `00f351c` | feat(repositories): implement ProductionBatchRepositoryImpl for domain repository integration with JPA | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `da715d6` | feat(monitoring): add command assemblers for creating alerts, equipment, readings, and sensors from resources | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `f28887c` | feat(monitoring): add assemblers for Equipment, Reading, and Sensor resources | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `0459d9a` | feat(monitoring): add AlertsController for managing monitoring alerts | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ccddb83` | feat(monitoring): add EquipmentController for managing equipment resources | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `f94c798` | feat(monitoring): add ReadingsController for managing telemetry readings | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `7ea814c` | feat(monitoring): add SensorsController for managing IoT telemetry sensors | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `e253df8` | Merge branch 'develop' into feature/monitoring | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `01b31c2` | feat(monitoring): extend aggregate roots to support domain event registration | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `ad1bba0` | feat(monitoring): update command services to use ApplicationError for result handling | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `9d25f2a` | feat(monitoring): refactor command services to use ApplicationError for result handling | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `eb6c654` | feat(monitoring): integrate DomainEventPublisher in repository implementations for event handling | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `fc69fba` | feat(monitoring): refactor persistence entities to extend AuditableAbstractPersistenceEntity for unified auditing | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `a5451fb` | feat(monitoring): refactor controllers to use ApplicationError and ResponseEntityAssembler for error handling | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `4d88cb3` | feat(monitoring): remove unused JPA repository interfaces for Alert, Equipment, Reading, and Sensor | — | 07/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `75046f8` | feat(application): implement Production Batch command service and implementation | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `523f04d` | feat(resources): add REST resources for Production Batch and Incident management | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `4181278` | feat(queryservices): add ProductionBatchQueryService interface and implementation for querying production batches | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `a7b87a7` | fix(application): annotate ProductionBatchCommandServiceImpl and ProductionBatchQueryServiceImpl with @Service | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `e3548ea` | feat(transform): add assemblers for creating and converting production batch and incident resources | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `9091e6d` | feat(controller): add ProductionBatchesController for managing production batch operations | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/manufacturing | `94be293` | fix(events): relax DomainEventPublisher signature to accept any AbstractDomainAggregateRoot | — | 08/11/2026 |
| IngesCompany/doofplus-platform | develop | `8aab90c` | Merge branch 'feature/manufacturing' into develop | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring | `0e39884` | Merge branch 'develop' into feature/monitoring | — | 08/11/2026 |
| IngesCompany/doofplus-platform | develop | `30f01b7` | Merge branch 'feature/monitoring' into develop | — | 08/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `5784e24` | Merge branch 'develop' into feature/quality | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `ea11ed6` | fix(quality): add deviation, capa domain and batch release aggregate | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `2c020b6` | feat(quality): add evidence domain value objects | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `590005d` | fix(quality): add quality document and evidence aggregates | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d894a84` | fix(quality): add analytical result aggregate | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e73038b` | fix(quality): add audit domain aggregates | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `f9c8c52` | fix(quality): add regulatory report aggregate | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e93622a` | fix(quality): add collaboration task aggregates | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `4e458ed` | fix(quality): add traceability gap aggregate | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `2c7cf6e` | feat(quality): add deviation and CAPA commands | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `9df092a` | feat(quality): add batch release commands | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `bbbb384` | feat(quality): add quality management commands | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `0f583e6` | feat(quality): add quality queries | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e971527` | feat(quality): add domain events | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `47f8847` | feat(quality): add domain exceptions | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `c1c939a` | feat(quality): define deviation and CAPA repository contracts | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `17a71a5` | feat(quality): define batch release repository contract | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e1ba1ad` | feat(quality): define quality document and evidence repository contracts | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `8b9f618` | feat(quality): define analytical result repository contract | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `786bc42` | feat(quality): define audit repository contracts | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `5ed55f3` | feat(quality): define regulatory report repository contract | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `682d284` | feat(quality): define collaboration repository contracts | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `327499c` | feat(quality): define traceability gap repository contract | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `048b3bb` | feat(quality): add deviation and CAPA persistence entities | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `f4abdd5` | feat(quality): add deviation and CAPA persistence repositories | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `dd19658` | feat(quality): implement deviation and CAPA repository adapters | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `007c01f` | fix(quality): implement deviation and CAPA repository adapters | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d1c7e6d` | fix(quality): implement deviation repository adapters | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `c56e61d` | feat(quality): add CAPA action persistence | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `eb44f32` | feat(quality): add batch release persistence | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `a5758fa` | feat(quality): add quality document persistence | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `3fd9196` | feat(quality): add evidence persistence | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d326723` | feat(quality): add analytical result persistence | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `85fb737` | feat(quality): add audit persistence | — | 09/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `8d31998` | feat(quality): add audit finding persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `6db7ffc` | feat(quality): add audit event persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `befd0f2` | feat(quality): add regulatory report persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `c041451` | feat(quality): add collaboration task persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `ec6a5a2` | feat(quality): add task comment persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `0429150` | feat(quality): add traceability gap persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `ddb87a8` | refactor(quality): reorganize bounded context architecture | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `5a6646a` | feat(quality): define deviation application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `7b62642` | feat(quality): define analytical result command service | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `9d2f34d` | feat(quality): define audit command service | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `df7e8ae` | feat(quality): define audit command service | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `66aae6b` | feat(quality): implement audit application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `342ac3d` | feat(quality): implement audit finding application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `5a5fba1` | feat(quality): implement batch release application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `b1dd88e` | feat(quality): implement batch release application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `c93d8d6` | feat(quality): implement capa plan application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `adb76e1` | feat(quality): implement collaboration task application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `4ec34be` | feat(quality): implement deviation application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `4372062` | feat(quality): implement evidence application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `e918e1f` | feat(quality): implement quality document application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `62ca56d` | feat(quality): implement regulatory report application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `1d7e12a` | feat(quality): implement task comment application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `3ee40c8` | feat(quality): implement traceability gap application services | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `2e7670f` | feat(quality): implement deviation trend query service | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `43ceb5b` | feat(quality): add analytical result REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d5b442b` | feat(quality): add audit REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `539ea74` | feat(quality): add audit event REST resource and assembler | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `33589bb` | feat(quality): add audit finding REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `904f0b1` | feat(quality): add batch release REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d514f9a` | feat(quality): add capa action REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `98daaba` | feat(quality): add capa plan REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `3324d13` | feat(quality): add collaboration task REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `8fb0044` | feat(quality): add deviation REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `53b1435` | feat(quality): add deviation trend REST resource and assembler | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `616c5dc` | feat(quality): add evidence REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `cf9575d` | feat(quality): add quality document REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `4dc19df` | feat(quality): add regulatory report REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `a98c29d` | feat(quality): add task comment REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `4b5ac07` | feat(quality): add traceability gap REST resources and assemblers | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `acb414a` | feat(quality): implement analytical result REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `42012aa` | feat(quality): implement audit REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `1e6d2e5` | feat(quality): add audit event REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `c635a13` | feat(quality): add audit finding REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `f72c449` | feat(quality): add batch release REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `1f70d83` | feat(quality): add capa action REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `d2cc4b8` | feat(quality): add capa plan REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `50d7436` | fix(quality): fix batch controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `ab689da` | feat(quality): add collaboration task REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `8dacf6d` | feat(quality): add deviation REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `6c460aa` | feat(quality): add deviation trend REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `3554b70` | feat(quality): add evidence REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `7155fc2` | feat(quality): add quality document REST endpoints | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `b06a1a1` | feat(quality): add regulatory report REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `22b036b` | feat(quality): add task comment REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `22d2902` | feat(quality): add traceability gap REST controller | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `f7c981d` | Merge branch 'develop' into feature/subscriptions | # Conflicts: # src/main/resources/messages.properties # src/main/resources/messages_es.properties | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `8b724fc` | refactor(subscriptions): use the shared result and error responses | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `77fdfed` | refactor(subscriptions): separate the domain model from the jpa persistence | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `be331bf` | feat(subscriptions): add the current period start and the renewal endpoint | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `95e298d` | refactor(organizations): aling the domain model with the class diagram | — | 10/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `89cc186` | fix(subscriptions): accept zero as unlimited in plan limits | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `7518324` | fix(subscriptions): limit the card brand length | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `5d1d921` | docs(subscriptions): use the same currency as the diagram | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `d839364` | feat(subscriptions): add the payment entity | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `eb69350` | feat(subscriptions): add the payment persistence | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `d4ce337` | feat(subscriptions): add the niubiz payment gateway | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-value-object-messages | `7e5f589` | fix(shared): translate value object error messages | — | 12/11/2026 |
| IngesCompany/doofplus-platform | develop | `a4c1fe2` | Merge branch 'feature/shared-value-object-messages' into develop | — | 12/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `213438a` | Merge remote-tracking branch 'origin/develop' into feature/organizations | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `e710dba` | refactor(organizations): fix the command, query and repository names and add the error messages | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `bd60fc1` | feat(organizations): add organization command and query services | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `17ee993` | feat(organizations): persist organizations and plants with jpa | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `bb9fcaa` | feat(organizations): expose the organizations rest endpoints (TS12) | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/cors-configuration | `c7ac61c` | feat(shared): add cors configuration for the web application | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `35eafb3` | Merge branch 'feature/cors-configuration' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-error-responses | `d86d9a4` | fix(shared): answer missing or mistyped request parameters with a bad request | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-error-responses | `e552e37` | fix(shared): translate the message keys of the application error details | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `4c447b5` | Merge branch 'feature/shared-error-responses' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `637cb3f` | feat(subscriptions): add the pay subscription endpoint | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `1cdb08d` | test(subscriptions): add plan and subscription tests | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `60118ff` | test(subscriptions): add payment tests | — | 13/11/2026 |
| IngesCompany/doofplus-platform | pub-org | `46d3122` | Merge remote-tracking branch 'origin/develop' into pub-org | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `60f351f` | fix(organizations): answer a duplicate ruc with a localized message | — | 13/11/2026 |
| IngesCompany/doofplus-platform | pub-quality | `5a42fdc` | Merge remote-tracking branch 'origin/develop' into pub-quality | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/quality | `83134c7` | fix(quality): read the creation date of batch releases and capa plans from the audit column | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `396c94e` | Merge branch 'feature/quality' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `9c77f70` | feat(organizations): add the contact inquiry domain model | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions | `9260ffa` | fix(subscriptions): use the niubiz security token path | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `2e8852e` | feat(organizations): add the contact inquiry services and jpa persistence | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations | `aa2d522` | feat(organizations): expose the contact inquiries rest endpoints (TS12) | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `8624efc` | Merge branch 'feature/organizations' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations-facilities | `9fc9a8e` | refactor(organizations): replace plant with facility as in the class diagram | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations-facilities | `c6e8e89` | feat(organizations): list organizations and facilities | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations-facilities | `a52f74d` | feat(organizations): add user profiles with their notification preferences | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/organizations-facilities | `fe53339` | feat(organizations): record and list the administrative activities | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `cad7ef9` | Merge branch 'feature/organizations-facilities' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/bounded-context-messages | `1a42271` | feat(shared): add the error messages of manufacturing, monitoring and quality | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `622c347` | Merge branch 'feature/bounded-context-messages' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/shared-unreadable-body | `1573168` | fix(shared): answer an unreadable request body with a bad request | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `b468f15` | Merge branch 'feature/shared-unreadable-body' into develop | — | 13/11/2026 |
| IngesCompany/doofplus-platform | develop | `fd94b12` | Merge branch 'feature/subscriptions' into develop | # Conflicts: # src/main/resources/messages.properties # src/main/resources/messages_es.properties | 13/11/2026 |
| IngesCompany/doofplus-platform | release/v1.0.0 | `6a47dc2` | chore(release): prepare version 1.0.0 | — | 13/11/2026 |
| IngesCompany/doofplus-platform | main | `529e7b6` | Merge branch 'release/v1.0.0' into main | — | 13/11/2026 |
| IngesCompany/doofplus-platform | feature/monitoring-delete-equipment-and-conflicts | `9a60d2c` | feat(monitoring): delete equipment and answer 409 for state changes that are not allowed | — | 14/11/2026 |
| IngesCompany/doofplus-platform | develop | `69f5245` | Merge branch 'feature/monitoring-delete-equipment-and-conflicts' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-platform | release/v1.1.0 | `4e1d432` | chore(release): prepare version 1.1.0 | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/iam-invitations | `63d5a24` | Merge branch 'release/v1.1.0' into main | — | 14/11/2026 |
| IngesCompany/doofplus-platform | develop | `05dd12d` | Merge branch 'release/v1.1.0' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/iam | `51b6190` | Merge branch 'develop' into feature/iam | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/subscriptions-change-plan | `bdfa7a6` | feat(subscriptions): change the plan and the billing cycle of a subscription | — | 14/11/2026 |
| IngesCompany/doofplus-platform | develop | `ed3d544` | Merge branch 'feature/subscriptions-change-plan' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/iam | `0de216c` | feat(iam): add sign-in with two-factor authentication and sign-up with jwt | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/iam | `e3f7969` | feat(iam): only administrators read the contact inquiries | — | 14/11/2026 |
| IngesCompany/doofplus-platform | develop | `31d3f4f` | Merge branch 'feature/iam' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/lookups-by-id-and-filters | `6377058` | feat(platform): add the lookups by id and the filters that the web app can use | — | 14/11/2026 |
| IngesCompany/doofplus-platform | develop | `2e52aa3` | Merge branch 'feature/lookups-by-id-and-filters' into develop | — | 14/11/2026 |
| IngesCompany/doofplus-platform | feature/quality-model-from-diagrams | `983c470` | feat(quality): implement the Quality contract from the class and database diagrams | — | 15/11/2026 |
| IngesCompany/doofplus-platform | develop | `1a6c7cb` | Merge branch 'feature/quality-model-from-diagrams' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-platform | release/v1.2.0 | `e536f9c` | chore(release): prepare version 1.2.0 | — | 15/11/2026 |
| IngesCompany/doofplus-platform | feature/iam-invitations | `451e551` | Merge branch 'release/v1.2.0' into main | — | 15/11/2026 |
| IngesCompany/doofplus-platform | develop | `b8ef89c` | Merge branch 'release/v1.2.0' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-platform | feature/iam-invitations | `b03c18d` | feat(iam): add the invitations of new members for administrators | — | 15/11/2026 |
| IngesCompany/doofplus-platform | develop | `3b8e4b0` | Merge branch 'feature/iam-invitations' into develop | — | 15/11/2026 |
| IngesCompany/doofplus-platform | release/v1.3.0 | `e6406a4` | chore(release): prepare version 1.3.0 | — | 15/11/2026 |
| IngesCompany/doofplus-platform | develop | `3e6729a` | Merge branch 'release/v1.3.0' into develop | — | 15/11/2026 |

**Curso de Responsabilidad Social** (`develop`, 35 commits)

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|------------|--------|-----------|----------------|---------------------|---------------------|
| IngesCompany/java-fundamentals-course-ingescompany | develop | `841c5d5` | chore: initial commit | — | 04/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/project-configuration | `1c41cd0` | docs: add course outline and resources for Java fundamentals | — | 04/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/project-configuration | `2552c8c` | docs: update team details and NRC in README | — | 04/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `04ad6f4` | Merge branch 'feature/project-configuration' into develop | — | 04/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-04 | `692fb89` | feat(lesson-04): add the starter code | — | 05/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-04 | `3c2df5f` | feat(lesson-04): add the completed example | — | 06/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-04 | `2f6f835` | docs(lesson-04): add the lesson script | — | 06/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-04 | `42b1ff5` | feat(slides): add the course slide deck | — | 06/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `10bdee3` | Merge branch 'feature/leccion-04' into develop | — | 06/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-03 | `f82c0d2` | feat(lesson-03): add the starter code | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-03 | `bf4166c` | feat(lesson-03): add the completed example | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-03 | `837f78b` | docs(lesson-03): add the lesson script | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `aea5073` | Merge branch 'feature/leccion-03' into develop | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-02 | `842ccb3` | feat(lesson-02): add the starter code | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-02 | `90342f8` | feat(lesson-02): add the completed example | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-02 | `bbad5b3` | docs(lesson-02): add the lesson script | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-02 | `5cfba29` | build: add the pandoc settings for the course plan pdf | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `021b821` | Merge branch 'feature/leccion-02' into develop | — | 07/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-04-starter | `20fd139` | fix(lesson-04): remove the scanner from the starter code | — | 10/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `245dc96` | Merge branch 'feature/leccion-04-starter' into develop | — | 10/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/leccion-03-starter | `6aea3be` | fix(lesson-03): remove the points variable from the starter code | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `58eeaaa` | Merge branch 'feature/leccion-03-starter' into develop | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/scripts-actualizados | `5faa98b` | docs(scripts): update the six lesson scripts with the new narration | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/lecciones-1-5-6 | `5da4cc0` | feat(lessons): add the starter and completed code of lessons 1, 5 and 6 | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `37abbe4` | Merge branch 'feature/scripts-actualizados' into develop | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/plan-del-curso | `54c1e93` | docs(course-plan): add the course plan and its pdf styles | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/plan-del-curso | `1f379cb` | build: ignore the pandoc build folder | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `d947c2a` | Merge branch 'feature/lecciones-1-5-6' into develop | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `276da07` | Merge branch 'feature/plan-del-curso' into develop | — | 12/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/readme-course-plan | `c0e5a64` | docs(readme): use the final course plan as the readme | — | 14/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `62cfedb` | Merge branch 'feature/readme-course-plan' into develop | — | 14/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/video | `26ec9ac` | docs(readme): update YouTube video and online practice links for lessons 1-6 | — | 15/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `e297ee5` | Merge branch 'feature/video' into develop | — | 15/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | feature/team-responsibilities | `835b6a8` | docs(readme): update the team responsibilities | — | 15/11/2026 |
| IngesCompany/java-fundamentals-course-ingescompany | develop | `61cdcbe` | Merge branch 'feature/team-responsibilities' into develop | — | 15/11/2026 |

#### 5.2.3.5. Execution Evidence for Sprint Review

En este Sprint el Website lleva a cada segmento a su entorno con un call to action propio, tiene enlaces a las redes sociales y se publica en GitHub Pages con GitHub Actions. La Web Application traduce los permisos de cada rol, busca por código desde la barra superior, enlaza con el Website y recibe las consultas de Contact us en su zona pública. Los RESTful Web Services quedaron desplegados con los seis bounded contexts: IAM (registro, inicio de sesión con JWT y segundo factor, usuarios, roles e invitaciones), Organizations & Profiles, Subscriptions & Payments (con el pago por Niubiz), Manufacturing & Batch Management, IoT Monitoring y Quality & Compliance. La Web Application `v1.4.0` usa ese API en los seis bounded contexts y ya no usa la Fake API. Los datos de demostración del laboratorio (organización, plantas, usuarios, invitaciones, planes, Manufacturing, IoT y Quality) están cargados en la base de producción.

- **Website:** https://ingescompany.github.io/doofplus-website/
- **Web Application:** https://doofplus-webapp.web.app
- **RESTful Web Services (Swagger UI):** https://doofplus-platform.onrender.com/swagger-ui.html

Video de navegación del producto: upc-pre-202620-1asi0729-7742-IngesCompany-productnavigation-sprint-3 (duración: 12:45), ver en Microsoft Stream: https://shorturl.at/bdRv6. Muestra la navegación de los tres productos en este orden:

- **Website:** 0:00 - 4:59.
- **Web Application:** 5:00 - 9:58.
- **RESTful Web Services (Swagger UI):** 9:59 - 12:45.

[![Video de navegación del producto del Sprint 3](assets/img/chapter5/sprint3/product-navigation-video.jpg)](https://shorturl.at/bdRv6)

*Figura: Cuadro del video de navegación del producto del Sprint 3 (minuto 7:10, evaluación de riesgo de una desviación en la Web Application conectada al API).*

#### 5.2.3.6. Services Documentation Evidence for Sprint Review

Los RESTful Web Services se documentan con OpenAPI (springdoc-openapi) y Swagger UI. La versión `v1.3.0`, desplegada en Render, expone 91 rutas y 134 operaciones bajo el prefijo `/api/v1`; la especificación se puede descargar en https://doofplus-platform.onrender.com/v3/api-docs. La URL base publicada es `https://doofplus-platform.onrender.com/api/v1` y la local, `http://localhost:8080/api/v1`. La siguiente tabla documenta cada operación, con su enlace a Swagger UI. El servicio usa el plan gratuito de Render, que lo suspende cuando no recibe peticiones, por lo que la primera petición puede tardar cerca de un minuto.

| Endpoint | Verbo HTTP | Sintaxis | Parámetros | Response | URL documentación |
|---|---|---|---|---|---|
| `/administrative-activities` | GET | `/api/v1/administrative-activities` | `organizationId` (query) | 200: Get the administrative activities, the most recent first | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Administrative%20Activities/getAllAdministrativeActivities |
| `/alerts` | GET | `/api/v1/alerts` | `sensorCode` (query), `batchCode` (query) | 200: Get alerts | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Alerts/getAllAlerts |
| `/alerts` | POST | `/api/v1/alerts` | recurso en el body (JSON) | 201, 400, 409: Create alert | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Alerts/createAlert |
| `/alerts` | GET | `/api/v1/alerts/{id}` | `id` (path) | 200, 404: Get alert by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Alerts/getAlertById |
| `/alerts` | PUT | `/api/v1/alerts/{id}` | `id` (path), recurso en el body (JSON) | 200, 400, 404: Update alert | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Alerts/updateAlert |
| `/analytical-results` | GET | `/api/v1/analytical-results` | `batchCode` (query) | 200: Get the analytical results | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Analytical%20results/getAnalyticalResults |
| `/analytical-results` | POST | `/api/v1/analytical-results` | recurso en el body (JSON) | 200: Create a analytical result | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Analytical%20results/createAnalyticalResult |
| `/analytical-results` | GET | `/api/v1/analytical-results/{analyticalResultId}` | `analyticalResultId` (path) | 200: Get a analytical result by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Analytical%20results/getAnalyticalResultById |
| `/analytical-results` | PUT | `/api/v1/analytical-results/{analyticalResultId}` | `analyticalResultId` (path), recurso en el body (JSON) | 200: Update a analytical result | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Analytical%20results/updateAnalyticalResult |
| `/audit-events` | GET | `/api/v1/audit-events` | `record` (query) | 200: Get the audit events | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audit%20events/getAuditEvents |
| `/audit-events` | POST | `/api/v1/audit-events` | recurso en el body (JSON) | 200: Create a audit event | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audit%20events/createAuditEvent |
| `/audit-events` | GET | `/api/v1/audit-events/{auditEventId}` | `auditEventId` (path) | 200: Get a audit event by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audit%20events/getAuditEventById |
| `/audit-findings` | GET | `/api/v1/audit-findings` | `auditCode` (query) | 200: Get the audit findings | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audit%20findings/getAuditFindings |
| `/audit-findings` | POST | `/api/v1/audit-findings` | recurso en el body (JSON) | 200: Create a audit finding | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audit%20findings/createAuditFinding |
| `/audit-findings` | GET | `/api/v1/audit-findings/{auditFindingId}` | `auditFindingId` (path) | 200: Get a audit finding by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audit%20findings/getAuditFindingById |
| `/audits` | GET | `/api/v1/audits` | — | 200: Get the audits | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audits/getAudits |
| `/audits` | POST | `/api/v1/audits` | recurso en el body (JSON) | 200: Create a audit | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audits/createAudit |
| `/audits` | GET | `/api/v1/audits/{auditId}` | `auditId` (path) | 200: Get a audit by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Audits/getAuditById |
| `/authentication` | POST | `/api/v1/authentication/sign-in` | recurso en el body (JSON) | 200, 401: Sign in | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Authentication/signIn |
| `/authentication` | POST | `/api/v1/authentication/sign-up` | recurso en el body (JSON) | 201, 400, 409: Sign up | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Authentication/signUp |
| `/batch-releases` | GET | `/api/v1/batch-releases` | — | 200: Get all batch releases | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Batch%20Releases/getAllBatchReleases |
| `/batch-releases` | POST | `/api/v1/batch-releases` | recurso en el body (JSON) | 200: Request a batch release | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Batch%20Releases/requestBatchRelease |
| `/batch-releases` | GET | `/api/v1/batch-releases/by-batch/{batchId}` | `batchId` (path) | 200: Get batch releases by batch ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Batch%20Releases/getBatchReleasesByBatchId |
| `/batch-releases` | GET | `/api/v1/batch-releases/{releaseId}` | `releaseId` (path) | 200: Get batch release by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Batch%20Releases/getBatchReleaseById |
| `/batch-releases` | PUT | `/api/v1/batch-releases/{releaseId}/approve` | `releaseId` (path), recurso en el body (JSON) | 200: Approve a batch release | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Batch%20Releases/approveBatchRelease |
| `/batch-releases` | PUT | `/api/v1/batch-releases/{releaseId}/reject` | `releaseId` (path), recurso en el body (JSON) | 200: Reject a batch release | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Batch%20Releases/rejectBatchRelease |
| `/capa-actions` | GET | `/api/v1/capa-actions` | `capaCode` (query) | 200: Get the capa actions | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20actions/getCapaActions |
| `/capa-actions` | POST | `/api/v1/capa-actions` | recurso en el body (JSON) | 200: Create a capa action | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20actions/createCapaAction |
| `/capa-actions` | GET | `/api/v1/capa-actions/{capaActionId}` | `capaActionId` (path) | 200: Get a capa action by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20actions/getCapaActionById |
| `/capa-actions` | PUT | `/api/v1/capa-actions/{capaActionId}` | `capaActionId` (path), recurso en el body (JSON) | 200: Update a capa action | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20actions/updateCapaAction |
| `/capa-plans` | GET | `/api/v1/capa-plans` | `sourceDeviation` (query) | 200: Get the capa plans | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20plans/getCapaPlans |
| `/capa-plans` | POST | `/api/v1/capa-plans` | recurso en el body (JSON) | 200: Create a capa plan | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20plans/createCapaPlan |
| `/capa-plans` | GET | `/api/v1/capa-plans/{capaPlanId}` | `capaPlanId` (path) | 200: Get a capa plan by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20plans/getCapaPlanById |
| `/capa-plans` | PUT | `/api/v1/capa-plans/{capaPlanId}` | `capaPlanId` (path), recurso en el body (JSON) | 200: Update a capa plan | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Capa%20plans/updateCapaPlan |
| `/collaboration-tasks` | GET | `/api/v1/collaboration-tasks` | `recordCode` (query) | 200: Get the collaboration tasks | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Collaboration%20tasks/getCollaborationTasks |
| `/collaboration-tasks` | POST | `/api/v1/collaboration-tasks` | recurso en el body (JSON) | 200: Create a collaboration task | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Collaboration%20tasks/createCollaborationTask |
| `/collaboration-tasks` | GET | `/api/v1/collaboration-tasks/{collaborationTaskId}` | `collaborationTaskId` (path) | 200: Get a collaboration task by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Collaboration%20tasks/getCollaborationTaskById |
| `/contact-inquiries` | GET | `/api/v1/contact-inquiries` | — | 200: Get every contact inquiry, the most recent first | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Contact%20Inquiries/getAllContactInquiries |
| `/contact-inquiries` | POST | `/api/v1/contact-inquiries` | recurso en el body (JSON) | 200: Send a contact inquiry | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Contact%20Inquiries/sendContactInquiry |
| `/contact-inquiries` | GET | `/api/v1/contact-inquiries/{id}` | `id` (path) | 200: Get a contact inquiry by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Contact%20Inquiries/getContactInquiryById |
| `/deviation-trends` | GET | `/api/v1/deviation-trends` | — | 200: Get the deviation trend | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Deviation%20trends/getDeviationTrends |
| `/deviations` | GET | `/api/v1/deviations` | `batchCode` (query) | 200: Get the deviations | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Deviations/getDeviations |
| `/deviations` | POST | `/api/v1/deviations` | recurso en el body (JSON) | 200: Create a deviation | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Deviations/createDeviation |
| `/deviations` | GET | `/api/v1/deviations/{deviationId}` | `deviationId` (path) | 200: Get a deviation by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Deviations/getDeviationById |
| `/deviations` | PUT | `/api/v1/deviations/{deviationId}` | `deviationId` (path), recurso en el body (JSON) | 200: Update a deviation | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Deviations/updateDeviation |
| `/equipment` | GET | `/api/v1/equipment` | `code` (query) | 200: Get all equipment | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Equipment/getAllEquipment |
| `/equipment` | POST | `/api/v1/equipment` | recurso en el body (JSON) | 201, 400, 409: Create equipment | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Equipment/createEquipment |
| `/equipment` | GET | `/api/v1/equipment/{id}` | `id` (path) | 200, 404: Get equipment by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Equipment/getEquipmentById |
| `/equipment` | PUT | `/api/v1/equipment/{id}` | `id` (path), recurso en el body (JSON) | 200, 400, 404: Update equipment | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Equipment/updateEquipment |
| `/equipment` | DELETE | `/api/v1/equipment/{id}` | `id` (path) | 204, 404, 409: Delete equipment | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Equipment/deleteEquipment |
| `/evidence` | GET | `/api/v1/evidence` | `recordCode` (query) | 200: Get the evidence | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Evidence/getEvidence |
| `/evidence` | POST | `/api/v1/evidence` | recurso en el body (JSON) | 200: Create a evidence | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Evidence/createEvidence |
| `/evidence` | GET | `/api/v1/evidence/{evidenceId}` | `evidenceId` (path) | 200: Get a evidence by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Evidence/getEvidenceById |
| `/evidence` | PUT | `/api/v1/evidence/{evidenceId}` | `evidenceId` (path), recurso en el body (JSON) | 200: Update a evidence | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Evidence/updateEvidence |
| `/evidence` | DELETE | `/api/v1/evidence/{evidenceId}` | `evidenceId` (path) | 200: Delete a evidence | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Evidence/deleteEvidence |
| `/facilities` | GET | `/api/v1/facilities` | `organizationId` (query) | 200: Get every facility, or the ones of an organization | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Facilities/getAllFacilities |
| `/facilities` | POST | `/api/v1/facilities` | recurso en el body (JSON) | 200: Add a facility to an organization | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Facilities/addFacility |
| `/invitations` | GET | `/api/v1/invitations` | `organizationId` (query) | 200: Get the invitations | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Invitations/getInvitations |
| `/invitations` | POST | `/api/v1/invitations` | recurso en el body (JSON) | 201, 400, 401, 403, 409: Send an invitation | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Invitations/sendInvitation |
| `/invitations` | GET | `/api/v1/invitations/{invitationId}` | `invitationId` (path) | 200, 404: Get an invitation by its id | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Invitations/getInvitationById |
| `/master-formulas` | GET | `/api/v1/master-formulas` | `productCode` (query) | 200: Get the master formulas, optionally of one product | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Master%20Formulas/getMasterFormulas |
| `/master-formulas` | POST | `/api/v1/master-formulas` | recurso en el body (JSON) | 200: Write a master formula | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Master%20Formulas/createMasterFormula |
| `/master-formulas` | GET | `/api/v1/master-formulas/{masterFormulaId}` | `masterFormulaId` (path) | 200: Get a master formula by its id | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Master%20Formulas/getMasterFormulaById |
| `/master-formulas` | POST | `/api/v1/master-formulas/{masterFormulaId}/approval` | `masterFormulaId` (path), recurso en el body (JSON) | 200: Approve a master formula | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Master%20Formulas/approveMasterFormula |
| `/material-lots` | GET | `/api/v1/material-lots` | — | 200: Get all raw material lots | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/getLots |
| `/material-lots` | POST | `/api/v1/material-lots` | recurso en el body (JSON) | 200: Receive a raw material lot | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/receiveLot |
| `/material-lots` | GET | `/api/v1/material-lots/{rawMaterialLotId}` | `rawMaterialLotId` (path) | 200: Get a raw material lot by its id | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/getLotById |
| `/material-lots` | POST | `/api/v1/material-lots/{rawMaterialLotId}/allocation` | `rawMaterialLotId` (path), recurso en el body (JSON) | 200: Allocate an approved lot to a batch | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/allocateLot |
| `/material-lots` | POST | `/api/v1/material-lots/{rawMaterialLotId}/approval` | `rawMaterialLotId` (path) | 200: Approve a lot in inspection | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/approveLot |
| `/material-lots` | PUT | `/api/v1/material-lots/{rawMaterialLotId}/inspection` | `rawMaterialLotId` (path), recurso en el body (JSON) | 200: Record the QC inspection of a lot | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/inspectLot |
| `/material-lots` | POST | `/api/v1/material-lots/{rawMaterialLotId}/rejection` | `rawMaterialLotId` (path) | 200: Reject a lot in inspection | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Material%20Lots/rejectLot |
| `/organizations` | GET | `/api/v1/organizations` | `ruc` (query) | 200: Get every organization, or the one registered with a RUC | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Organizations/getAllOrganizations |
| `/organizations` | POST | `/api/v1/organizations` | recurso en el body (JSON) | 200: Register a new organization | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Organizations/registerOrganization |
| `/organizations` | GET | `/api/v1/organizations/{organizationId}` | `organizationId` (path) | 200: Get an organization by id | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Organizations/getOrganizationById |
| `/plans` | GET | `/api/v1/plans` | — | 200: Get all plans | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Plans/getAllPlans |
| `/plans` | POST | `/api/v1/plans` | recurso en el body (JSON) | 201, 400, 409: Create a plan | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Plans/createPlan |
| `/plans` | GET | `/api/v1/plans/{id}` | `id` (path) | 200, 404: Get a plan by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Plans/getPlanById |
| `/production-batches` | GET | `/api/v1/production-batches` | `batchNumber` (query) | 200: Get all production batches or filter by batch number | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/getBatches |
| `/production-batches` | POST | `/api/v1/production-batches` | recurso en el body (JSON) | 200: Create a new production batch | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/createBatch |
| `/production-batches` | GET | `/api/v1/production-batches/by-number/{batchNumber}` | `batchNumber` (path) | 200: Get a production batch by its batch number | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/getBatchByNumber |
| `/production-batches` | GET | `/api/v1/production-batches/{batchId}` | `batchId` (path) | 200: Get production batch by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/getBatchById |
| `/production-batches` | POST | `/api/v1/production-batches/{batchId}/close` | `batchId` (path), recurso en el body (JSON) | 200: Close a production batch | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/closeBatch |
| `/production-batches` | POST | `/api/v1/production-batches/{batchId}/incidents` | `batchId` (path), recurso en el body (JSON) | 200: Register an incident for a production batch | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/registerIncident |
| `/production-batches` | PATCH | `/api/v1/production-batches/{batchId}/progress` | `batchId` (path), recurso en el body (JSON) | 200: Update the progress of a production batch | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/updateProgress |
| `/production-batches` | POST | `/api/v1/production-batches/{batchId}/release` | `batchId` (path), recurso en el body (JSON) | 200: Release a production batch for distribution | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/releaseBatch |
| `/production-batches` | POST | `/api/v1/production-batches/{batchId}/resume` | `batchId` (path) | 200: Resume a production batch that is on hold | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/resumeBatch |
| `/production-batches` | POST | `/api/v1/production-batches/{batchId}/start` | `batchId` (path) | 200: Start a planned production batch | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Batches/startBatch |
| `/production-orders` | GET | `/api/v1/production-orders` | — | 200: Get all production orders | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Orders/getProductionOrders |
| `/production-orders` | POST | `/api/v1/production-orders` | recurso en el body (JSON) | 200: Plan a production order | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Orders/createProductionOrder |
| `/production-orders` | GET | `/api/v1/production-orders/{productionOrderId}` | `productionOrderId` (path) | 200: Get a production order by its id | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Orders/getProductionOrderById |
| `/production-orders` | PUT | `/api/v1/production-orders/{productionOrderId}/operations/{sequence}` | `productionOrderId` (path), `sequence` (path), recurso en el body (JSON) | 200: Record the progress of an operation | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Orders/updateOperation |
| `/production-orders` | PUT | `/api/v1/production-orders/{productionOrderId}/status` | `productionOrderId` (path), recurso en el body (JSON) | 200: Change the status of a production order | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Production%20Orders/changeStatus |
| `/products` | GET | `/api/v1/products` | — | 200: Get all products | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Products/getProducts |
| `/products` | POST | `/api/v1/products` | recurso en el body (JSON) | 200: Register a product | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Products/createProduct |
| `/products` | GET | `/api/v1/products/{productId}` | `productId` (path) | 200: Get a product by its id | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Products/getProductById |
| `/products` | PUT | `/api/v1/products/{productId}` | `productId` (path), recurso en el body (JSON) | 200: Update a product | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Products/updateProduct |
| `/quality-documents` | GET | `/api/v1/quality-documents` | `code` (query) | 200: Get the quality documents | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Quality%20documents/getQualityDocuments |
| `/quality-documents` | POST | `/api/v1/quality-documents` | recurso en el body (JSON) | 200: Create a quality document | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Quality%20documents/createQualityDocument |
| `/quality-documents` | GET | `/api/v1/quality-documents/{qualityDocumentId}` | `qualityDocumentId` (path) | 200: Get a quality document by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Quality%20documents/getQualityDocumentById |
| `/quality-documents` | PUT | `/api/v1/quality-documents/{qualityDocumentId}` | `qualityDocumentId` (path), recurso en el body (JSON) | 200: Update a quality document | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Quality%20documents/updateQualityDocument |
| `/readings` | GET | `/api/v1/readings` | `sensorCode` (query), `batchCode` (query) | 200: Get readings | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Readings/getAllReadings |
| `/readings` | POST | `/api/v1/readings` | recurso en el body (JSON) | 201, 400: Record reading | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Readings/createReading |
| `/readings` | GET | `/api/v1/readings/{id}` | `id` (path) | 200, 404: Get reading by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Readings/getReadingById |
| `/regulatory-reports` | GET | `/api/v1/regulatory-reports` | — | 200: Get the regulatory reports | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Regulatory%20reports/getRegulatoryReports |
| `/regulatory-reports` | POST | `/api/v1/regulatory-reports` | recurso en el body (JSON) | 200: Create a regulatory report | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Regulatory%20reports/createRegulatoryReport |
| `/regulatory-reports` | GET | `/api/v1/regulatory-reports/{regulatoryReportId}` | `regulatoryReportId` (path) | 200: Get a regulatory report by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Regulatory%20reports/getRegulatoryReportById |
| `/roles` | GET | `/api/v1/roles` | — | 200, 401, 403: Get all roles | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Roles/getAllRoles |
| `/sensors` | GET | `/api/v1/sensors` | `equipmentCode` (query) | 200: Get sensors | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Sensors/getAllSensors |
| `/sensors` | POST | `/api/v1/sensors` | recurso en el body (JSON) | 201, 400, 409: Create sensor | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Sensors/createSensor |
| `/sensors` | GET | `/api/v1/sensors/{id}` | `id` (path) | 200, 404: Get sensor by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Sensors/getSensorById |
| `/sensors` | PUT | `/api/v1/sensors/{id}` | `id` (path), recurso en el body (JSON) | 200, 400, 404: Update sensor | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Sensors/updateSensor |
| `/subscriptions` | GET | `/api/v1/subscriptions` | `organizationId` (query) | 200, 400: Get subscriptions by organization | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/getSubscriptionsByOrganizationId |
| `/subscriptions` | POST | `/api/v1/subscriptions` | recurso en el body (JSON) | 201, 400, 404, 409: Create a subscription | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/createSubscription |
| `/subscriptions` | GET | `/api/v1/subscriptions/{id}` | `id` (path) | 200, 404: Get a subscription by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/getSubscriptionById |
| `/subscriptions` | POST | `/api/v1/subscriptions/{id}/activation` | `id` (path) | 200, 404, 409: Activate a subscription | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/activateSubscription |
| `/subscriptions` | POST | `/api/v1/subscriptions/{id}/cancellation` | `id` (path) | 200, 404, 409: Cancel a subscription | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/cancelSubscription |
| `/subscriptions` | POST | `/api/v1/subscriptions/{id}/payments` | `id` (path), recurso en el body (JSON) | 200, 400, 404, 409, 422, 503: Pay a subscription | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/paySubscription |
| `/subscriptions` | PUT | `/api/v1/subscriptions/{id}/plan` | `id` (path), recurso en el body (JSON) | 200, 400, 404, 409: Change the plan of a subscription | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/changeSubscriptionPlan |
| `/subscriptions` | POST | `/api/v1/subscriptions/{id}/renewal` | `id` (path) | 200, 404, 409: Renew a subscription | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Subscriptions/renewSubscription |
| `/task-comments` | GET | `/api/v1/task-comments` | `recordCode` (query) | 200: Get the task comments | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Task%20comments/getTaskComments |
| `/task-comments` | POST | `/api/v1/task-comments` | recurso en el body (JSON) | 200: Create a task comment | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Task%20comments/createTaskComment |
| `/task-comments` | GET | `/api/v1/task-comments/{taskCommentId}` | `taskCommentId` (path) | 200: Get a task comment by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Task%20comments/getTaskCommentById |
| `/telemetry` | POST | `/api/v1/telemetry` | recurso en el body (JSON) | 200: Receive a reading from ThingsBoard | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Telemetry/receiveTelemetry |
| `/tokens` | POST | `/api/v1/tokens` | recurso en el body (JSON) | 200, 401: Create authentication token (Sign-in) | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Tokens/generateToken |
| `/traceability-gaps` | GET | `/api/v1/traceability-gaps` | `batchCode` (query) | 200: Get the traceability gaps | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Traceability%20gaps/getTraceabilityGaps |
| `/traceability-gaps` | POST | `/api/v1/traceability-gaps` | recurso en el body (JSON) | 200: Create a traceability gap | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Traceability%20gaps/createTraceabilityGap |
| `/traceability-gaps` | GET | `/api/v1/traceability-gaps/{traceabilityGapId}` | `traceabilityGapId` (path) | 200: Get a traceability gap by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Traceability%20gaps/getTraceabilityGapById |
| `/user-profiles` | GET | `/api/v1/user-profiles` | `organizationId` (query) | 200: Get every user profile | https://doofplus-platform.onrender.com/swagger-ui/index.html#/User%20Profiles/getAllUserProfiles |
| `/user-profiles` | POST | `/api/v1/user-profiles` | recurso en el body (JSON) | 200: Create the profile of a user | https://doofplus-platform.onrender.com/swagger-ui/index.html#/User%20Profiles/createUserProfile |
| `/user-profiles` | GET | `/api/v1/user-profiles/{id}` | `id` (path) | 200: Get a user profile by its identifier | https://doofplus-platform.onrender.com/swagger-ui/index.html#/User%20Profiles/getUserProfileById |
| `/user-profiles` | PUT | `/api/v1/user-profiles/{profileId}` | `profileId` (path), recurso en el body (JSON) | 200: Update the notification preferences and the language of a user profile | https://doofplus-platform.onrender.com/swagger-ui/index.html#/User%20Profiles/updateUserProfile |
| `/users` | GET | `/api/v1/users` | — | 200, 401, 403: Get all users | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Users/getAllUsers |
| `/users` | POST | `/api/v1/users` | recurso en el body (JSON) | 201, 400, 409: Create user (Sign-up) | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Users/createUser |
| `/users` | GET | `/api/v1/users/{userId}` | `userId` (path) | 200, 401, 403, 404: Get user by ID | https://doofplus-platform.onrender.com/swagger-ui/index.html#/Users/getUserById |

#### 5.2.3.7. Software Deployment Evidence for Sprint Review

En este Sprint se publicaron las siguientes versiones, siguiendo GitFlow:

- **Website:** `release/v2.1.0` se fusionó en `main` con el tag `v2.1.0` (31/10/2026) y desde entonces el Website se publica en GitHub Pages con un workflow de GitHub Actions. Después se publicaron el hotfix `v2.1.1` (01/11/2026), `v2.2.0` (09/11/2026) y `v2.3.0` (15/11/2026), con los videos About-the-Product y About-the-Team y la página 404. URL: https://ingescompany.github.io/doofplus-website/.
- **Web Application:** el hotfix `v1.0.2` (01/11/2026) y `release/v1.1.0` (09/11/2026), con Contact us y los permisos por rol. Después se publicaron `v1.2.0` (14/11/2026), con Organizations & Profiles e IoT Monitoring en el API; `v1.3.0` (15/11/2026), con IAM, Subscriptions, Manufacturing y Quality & Compliance en el API; y `v1.4.0` (15/11/2026), con las invitaciones y los perfiles de rol en el API y sin la Fake API. Todas se publicaron en Firebase Hosting. URL: https://doofplus-webapp.web.app.
- **RESTful Web Services:** `release/v1.0.0` se fusionó en `main` con el tag `v1.0.0` (13/11/2026). Después se publicaron `v1.1.0` (14/11/2026), con el catálogo de Manufacturing y la telemetría de ThingsBoard; `v1.2.0` (15/11/2026), con IAM (JWT y segundo factor) y Quality & Compliance según los diagramas; y `v1.3.0` (15/11/2026), con las invitaciones de nuevos miembros. El API se publicó en un Web Service de Render con Docker, desde `main`, y su base de datos MySQL 8 en Railway; las credenciales se cargan como variables de entorno del servicio y no están en el repositorio. URL: https://doofplus-platform.onrender.com y Swagger UI en https://doofplus-platform.onrender.com/swagger-ui.html. Se comprobó que `POST /api/v1/contact-inquiries` responde 201 y, con un correo inválido, 400; y que los `GET` de cada bounded context responden 200.

#### 5.2.3.8. Team Collaboration Insights during Sprint

En este Sprint se incorporó Alisee Torres al equipo, por lo que participaron seis integrantes. La siguiente tabla resume los commits de cada integrante en el Sprint (desde el 18/10/2026, sin contar los commits de merge): en `main` del Website, de la Web Application y de los RESTful Web Services, y en `develop` del curso de Responsabilidad Social. Los analíticos de GitHub de cada repositorio están en *Insights › Contributors* y *Insights › Network*:

| Team Member | GitHub Username | Website | Web Application | RESTful Web Services | Curso (develop) | Total |
|---|---|:---:|:---:|:---:|:---:|:---:|
| Angulo Ramírez, Marcelo Martín | Zock2005 | 0 | 0 | 122 | 5 | 127 |
| Flores Martinez, Ricardo Andres | Nitoryu28 | 0 | 0 | 120 | 0 | 120 |
| Rojas Ambicho, Nestor Daniel | danRO-20 | 16 | 10 | 49 | 7 | 82 |
| Cobades Zamora, Yhoshua Hebert | YhoshuaCZ | 11 | 20 | 41 | 8 | 80 |
| Zavaleta Gutierrez, Rodolfo Martin | gutierrezrodolfo360-bit | 11 | 9 | 43 | 3 | 66 |
| Torres Juárez, Alisee Muriel | lLisee1 | 0 | 0 | 1 | 0 | 1 |

- **Website:** https://github.com/IngesCompany/doofplus-website/graphs/contributors y https://github.com/IngesCompany/doofplus-website/network
- **Web Application:** https://github.com/IngesCompany/doofplus-web-application/graphs/contributors y https://github.com/IngesCompany/doofplus-web-application/network
- **RESTful Web Services:** https://github.com/IngesCompany/doofplus-platform/graphs/contributors y https://github.com/IngesCompany/doofplus-platform/network

## 5.3. Validation Interviews

### 5.3.1. Diseño de Entrevistas

### 5.3.2. Registro de Entrevistas

### 5.3.3. Evaluaciones según heurísticas

Para el AV2 el equipo hizo una primera evaluación heurística interna sobre los productos publicados, con el formato del curso (Anexo D). Las sesiones de validación con usuarios de los segmentos objetivo (5.3.1 y 5.3.2) se hacen en la TB2, y esta evaluación se repetirá sobre ellas.

**UX Heuristics & Principles Evaluation**
**Usability – Inclusive Design – Information Architecture**

| | |
|---|---|
| **CARRERA** | Ingeniería de Software |
| **CURSO** | Desarrollo de Aplicaciones Open Source |
| **SECCIÓN** | 7742 |
| **PROFESORES** | Todos |
| **AUDITOR** | IngesCompany |
| **CLIENTE(S)** | Evaluación interna del equipo, sin usuarios externos (15/11/2026) |

**SITE o APP A EVALUAR:** DoofPlus: Website (https://ingescompany.github.io/doofplus-website/) y Web Application (https://doofplus-webapp.web.app).

**TAREAS A EVALUAR:**

El alcance de esta evaluación incluye la revisión de la usabilidad de las siguientes tareas:

1. Conocer el producto en el Website y cambiar el idioma.
2. Pasar del Website a la Web Application.
3. Elegir el entorno de trabajo (QA/QC, Producción o Administración).
4. Iniciar sesión y corregir los datos del formulario.

No están incluidas en esta versión de la evaluación las siguientes tareas, porque requieren una sesión con usuarios reales de cada rol:

1. Liberar un lote con firma electrónica.
2. Registrar una desviación y su plan CAPA.
3. Registrar una orden y un lote de producción.
4. Invitar a un usuario y gestionar la suscripción.

**ESCALA DE SEVERIDAD:**

| Nivel | Descripción |
|---|---|
| 1 | Problema superficial: puede ser fácilmente superado por el usuario u ocurre con muy poca frecuencia. No necesita ser arreglado a no ser que exista disponibilidad de tiempo. |
| 2 | Problema menor: puede ocurrir un poco más frecuentemente o es un poco más difícil de superar para el usuario. Se le debería asignar una prioridad baja de cara al siguiente release. |
| 3 | Problema mayor: ocurre frecuentemente o los usuarios no son capaces de resolverlo. Es importante que sea corregido y se le debe asignar una prioridad alta. |
| 4 | Problema muy grave: un error de gran impacto que impide al usuario continuar con el uso de la herramienta. Es imperativo que sea corregido antes del lanzamiento. |

**TABLA RESUMEN:**

| # | Problema | Escala de severidad | Heurística/Principio violada(o) |
|---|---|:---:|---|
| 1 | La primera petición al API, después de un rato sin uso, puede tardar hasta un minuto | 3 | Usability: Visibilidad del estado del sistema |
| 2 | El Website y la Web Application se abren en inglés aunque el navegador esté en español | 2 | Inclusive Design: Considera la situación |
| 3 | Mientras carga la fuente de íconos, se ven nombres como «science» o «check_circle» en lugar de los íconos | 1 | Usability: Consistencia y estándares |

**DESCRIPCIÓN DE PROBLEMAS:**

**PROBLEMA #1: La primera petición al API, después de un rato sin uso, puede tardar hasta un minuto**

Severidad: 3
Heurística violada: Usability - Visibilidad del estado del sistema

Problema: los RESTful Web Services están en el plan gratuito de Render, que suspende el servicio cuando no recibe peticiones. La primera acción contra el API después de ese tiempo (por ejemplo, iniciar sesión) puede tardar cerca de un minuto, y el usuario no sabe si el sistema está procesando o si falló.

Recomendación: mostrar un mensaje de espera («Conectando con DoofPlus…») cuando una petición tarda más de unos segundos y, para producción, usar un plan que no suspenda el servicio.

**PROBLEMA #2: El Website y la Web Application se abren en inglés aunque el navegador esté en español**

Severidad: 2
Heurística violada: Inclusive Design - Considera la situación

Problema: con el navegador en español (`es-US`, `es-419`) y sin una preferencia guardada, el Website y la Web Application se muestran en inglés. Los segmentos objetivo trabajan en laboratorios de Lima, por lo que la mayoría tendrá que buscar el selector EN/ES antes de empezar.

Recomendación: elegir el idioma inicial según el idioma del navegador y guardar la elección del usuario.

**PROBLEMA #3: Mientras carga la fuente de íconos, se ven nombres como «science» o «check_circle» en lugar de los íconos**

Severidad: 1
Heurística violada: Usability - Consistencia y estándares

Problema: en la primera visita a la pantalla de inicio de sesión de la Web Application, los íconos de Material se muestran por un momento como texto («science», «check_circle», «mail») hasta que termina de cargar su fuente.

Recomendación: ocultar los íconos hasta que la fuente esté lista (`font-display: block`) o incluir la fuente de íconos con la aplicación.

**Aspectos que cumplen las heurísticas:** el formulario de inicio de sesión marca cada campo obligatorio vacío con un mensaje claro («Enter a valid work email.», «Enter your password.»), permite mostrar la contraseña y explica antes de empezar que se pedirá un código de dos pasos; las imágenes del Website tienen texto alternativo y las dos aplicaciones tienen enlaces a los términos y la privacidad en el pie de página.

## 5.4. Video About-the-Product

En el video About-the-Product se presenta DoofPlus y se recorren el Website y la Web Application publicados.
[![About-The-Product](https://img.youtube.com/vi/saSnknxFqKw/maxresdefault.jpg)](https://www.youtube.com/watch?v=saSnknxFqKw)

**Enlace al video en YouTube:** https://youtu.be/saSnknxFqKw
**Enlace al video en Microsoft Stream**: https://upcedupe-my.sharepoint.com/:v:/g/personal/u20241f733_upc_edu_pe/IQCmIMtCezXVQb9zevKOpRwFAXgmSPglJLyvv4aHyw0Epdc?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=egQH7V
