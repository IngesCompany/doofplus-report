# Conclusiones

## Conclusiones y recomendaciones

### Conclusiones

1. **Sobre los Problem Statements:** las entrevistas confirmaron el problema planteado. El 100 % de los especialistas QA/QC trabaja con un esquema mixto de registros físicos y digitales, el 100 % de los jefes y supervisores de producción registra el seguimiento de los lotes en formularios físicos y hojas de cálculo, y el 67 % de ambos segmentos tiene dificultades para reconstruir el historial completo de un lote. DoofPlus responde a esta situación centralizando en una sola plataforma la documentación de calidad, los lotes, las desviaciones y los datos de los equipos.
2. **Sobre los Assumptions:** el equipo asumió que la resistencia al cambio sería una de las principales barreras de adopción. En las entrevistas, el 100 % de los participantes mostró una percepción favorable hacia la digitalización de sus procesos, siempre que la plataforma reduzca el trabajo manual y no agregue pasos a su rutina; esto orientó el diseño de la Web Application hacia entornos separados por rol y flujos cortos.
3. **Sobre los Hypothesis Statements y los criterios de éxito:** al cierre del Sprint 2 el Website y la Web Application están publicadas y cubren los flujos necesarios para probar las hipótesis: registro y seguimiento de lotes, desviaciones y CAPA, liberación con firma electrónica, audit trail y monitoreo IoT. La validación de las hipótesis y de los criterios de éxito con usuarios de cada segmento se realizará en las Validation Interviews (sección 5.3) de la siguiente entrega.

### Recomendaciones

1. **Para la siguiente entrega (AV2):** implementar los RESTful Web Services en Spring Boot y conectar la Web Application, que hoy consume una Fake API, empezando por Identity & Access Management, del que dependen el inicio de sesión con 2FA y las firmas electrónicas.
2. **Para la validación:** realizar las Validation Interviews con especialistas QA/QC y jefes de producción sobre la versión publicada de la Web Application, midiendo el tiempo necesario para reconstruir el historial de un lote y para preparar una auditoría, que son los criterios de éxito del Problem Statement.

## Video About-The-Team

### Resumen del video

El video About-The-Team presenta una síntesis del proceso de trabajo desarrollado por el equipo a lo largo del proyecto. Combina imágenes y video de sesiones reales de trabajo con una narración en voz en off que guía al espectador por las etapas principales: la organización del equipo, la distribución de roles, el desarrollo de las actividades y los resultados obtenidos. De este modo muestra la dinámica colaborativa y la manera en que se abordaron los desafíos del proyecto.

Además, el video incluye el testimonio ante cámara de cada participante, quien describe las actividades que realizó, el logro de los outcomes planteados y las competencias que desarrolló durante la experiencia. Estos testimonios aportan una mirada personal y complementan la visión global del trabajo en equipo, y muestran el aprendizaje alcanzado de forma individual y colectiva.

**Duración total:** [00:09:12]

### Cuadro de video representativo

[![About-The-Team](https://img.youtube.com/vi/U-Wlk2l3wbA/maxresdefault.jpg)](https://www.youtube.com/watch?v=U-Wlk2l3wbA)

*Cuadro representativo del video About-The-Team.*

### Pauta de secuencias de contenido

| N.º | Sección / Secuencia                        | Tiempo de inicio (hh:mm:ss) | Descripción breve                                                                                                                                                                                                      |
|:---:|--------------------------------------------|:---------------------------:|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1  | Introducción / Presentación del equipo     |          00:00:00           | Startup IngesCompany, desarrolladora de Doofplus, empezamos escuchando a los usuarios, haciendo entrevistas, oyendo sus problemas, gracias a esto se pudo hacer el needfinding, para luego pasar a DDD               |
|  2  | Proceso de trabajo del equipo (voz en off) |          00:00:19           | Una explicación del trabajo realizado a lo largo del curso, se menciona lo desarrollado en el sprint 1, sprint 2 y el sprint 3. Además, de mencionar brevemente de lo que desarrollará en el sprint 4                  |
|  3  | Testimonio de Marcelo Angulo               |          00:04:15           | Trabajó en las entrevistas con los segmentos objetivos. Además, se encargó de la programación del bounded context Monitoring. <br> Para el outcome: trabajó comunicandose de forma clara tanto en oral como en escrito |
|  4  | Testimonio de Yhoshua Cobades              |          00:05:13           | Trabajó en los aspectos de Domain Driven Design (Lenguaje Ubicuo), se encargó de los bounded context Quality y Manufacturing. <br> Para el outcome: expuso en el diseño del dominio                                    |
|  5  | Testimonio de Ricardo Flores               |          00:06:25           | Trabajó en las entrevistas de segmentos por producción. se encargó del bounded context Quality. <br> Para el outcome: presentó el sprint planning por escrito.                                                         |
|  6  | Testimonio de Daniel Rojas                 |          00:07:18           | Diseñó la arquitectura C4, diagramas c4, se encargó del bounded context Subscriptions. <br> Para el outcome: se encargó de explicar a sus compañeros sobre el código que implementaba.                                 |
|  7  | Testimonio de Rodolfo Zavaleta             |          00:08:10           | Presentó al equipo, trabajó en la arquitectura del código de la Web Application, se encargó del bounded context Manufacturing y Shared. <br> Para el outcome: expuso el proyecto a un público de negocio.              |

### Enlaces del video

| Plataforma | URL                                                                                                                                                                                                                                                                                                                     | Uso |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| Microsoft Stream | https://upcedupe-my.sharepoint.com/:v:/g/personal/u20241f733_upc_edu_pe/IQDAODnF4cJATq3fvJ5N25dXAbNuKp45yHqBcpQGjiZQMS4?e=MVjjbN&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D | Versión publicada |
| YouTube | https://youtu.be/U-Wlk2l3wbA                                                                                                                                                                                                                                                                              | Versión incrustada en el Landing Page |


