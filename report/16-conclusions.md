# Conclusiones

## Conclusiones y recomendaciones

### Conclusiones

1. **Sobre los Problem Statements:** las entrevistas confirmaron el problema planteado. El 100 % de los especialistas QA/QC trabaja con un esquema mixto de registros físicos y digitales, el 100 % de los jefes y supervisores de producción registra el seguimiento de los lotes en formularios físicos y hojas de cálculo, y el 67 % de ambos segmentos tiene dificultades para reconstruir el historial completo de un lote. DoofPlus responde a esta situación centralizando en una sola plataforma la documentación de calidad, los lotes, las desviaciones y los datos de los equipos.
2. **Sobre los Assumptions:** el equipo asumió que la resistencia al cambio sería una de las principales barreras de adopción. En las entrevistas, el 100 % de los participantes mostró una percepción favorable hacia la digitalización de sus procesos, siempre que la plataforma reduzca el trabajo manual y no agregue pasos a su rutina; esto orientó el diseño de la Web Application hacia entornos separados por rol y flujos cortos.
3. **Sobre los Hypothesis Statements y los criterios de éxito:** al cierre del Sprint 2 el Website y la Web Application están publicadas y cubren los flujos necesarios para probar las hipótesis: registro y seguimiento de lotes, desviaciones y CAPA, liberación con firma electrónica, audit trail y monitoreo IoT. La validación de las hipótesis y de los criterios de éxito con usuarios de cada segmento se realizará en las Validation Interviews (sección 5.3) de la siguiente entrega.

### Recomendaciones

1. **Para la siguiente entrega (AV2):** implementar los RESTful Web Services en Spring Boot y conectar la Web Application, que hoy consume una Fake API, empezando por Identity & Access Management, del que dependen el inicio de sesión con 2FA y las firmas electrónicas.
2. **Para la validación:** realizar las Validation Interviews con especialistas QA/QC y jefes de producción sobre la versión publicada de la Web Application, midiendo el tiempo necesario para reconstruir el historial de un lote y para preparar una auditoría, que son los criterios de éxito del Problem Statement.

## Video About-the-Team

El video About-the-Team se presentará en la entrega AV2. En él, cada integrante contará su experiencia en el desarrollo de DoofPlus y el equipo expondrá la proyección del producto: la integración de la Web Application con los RESTful Web Services, la conexión con ThingsBoard para la telemetría real de los sensores y la incorporación de los laboratorios piloto.
