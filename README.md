# Integración Eleonor - MiDocOnline

Este repositorio contiene la documentación y el diseño del proyecto de integración entre las plataformas **Eleonor** y **MiDocOnline**, enfocado en mejorar la experiencia de pacientes y médicos mediante el uso de una interfaz inteligente, denominada **"Humanoide"**, que asiste en la detección de padecimientos.

## Objetivo del Proyecto

El objetivo principal de esta integración es establecer una comunicación eficiente entre ambas plataformas, aprovechando el modelo de IA de MiDocOnline para generar diagnósticos y recomendaciones de medicamentos, los cuales se integrarán en el flujo de trabajo de Eleonor. El sistema se desarrollará en múltiples fases y abarcará tanto el flujo del paciente como el del médico.

---

## Fases del Proyecto

### Para el Paciente
1. **Formulario de Registro (Eleonor)**  
   Eleonor presentará al paciente un formulario para registrar información básica:  
   - **Datos personales:** Nombre, apellidos, sexo, fecha de nacimiento, nacionalidad, entre otros.  
   - **Historia clínica inicial:** Información médica relevante.  

2. **Interfaz Humanoide (MiDocOnline)**  
   Una vez registrado, Eleonor redirigirá al paciente al **Humanoide** de MiDocOnline, donde este podrá describir su padecimiento con asistencia del modelo de IA.

### Para el Médico
3. **Recomendaciones IA (MiDocOnline → Eleonor)**  
   MiDocOnline procesará los datos del paciente y enviará a Eleonor:
   - Diagnósticos sugeridos.  
   - Medicamentos recomendados basados en el análisis del modelo de IA.  

4. **Revisión y Selección (Eleonor)**  
   - En la interfaz de Eleonor, el médico revisará las sugerencias generadas por el Humanoide.  
   - Seleccionará libremente los diagnósticos y medicamentos que considere adecuados para el paciente.

5. **Feedback Médico (Eleonor → MiDocOnline)**  
   - Eleonor proporcionará retroalimentación a MiDocOnline sobre los diagnósticos y medicamentos finalmente registrados por el médico.  
   - Estos datos servirán para mejorar el modelo de IA de MiDocOnline.

---

## Consideraciones Técnicas

### Identificación de Pacientes
- **Eleonor:** Identifica a los pacientes mediante un campo único `PK`.  
- **MiDocOnline:** Utiliza el correo electrónico del paciente como identificador único.  
Se debe establecer un mecanismo de mapeo para garantizar la coherencia en ambas plataformas.

### Historia Clínica
- Determinar y documentar los valores equivalentes de historia clínica en ambas plataformas.  
- Establecer un estándar común para garantizar la interoperabilidad.

### Comunicación de Servicios REST
- Diseñar la estructura de los mensajes JSON para intercambiar información.  
- Los mensajes incluirán datos sobre diagnósticos y medicamentos en ambos sentidos:
  - **MiDocOnline → Eleonor:** Diagnósticos y medicamentos sugeridos.  
  - **Eleonor → MiDocOnline:** Diagnósticos y medicamentos seleccionados por el médico.  

Ejemplo de estructura de JSON para diagnósticos y medicamentos:  
```json
{
  "patientId": "unique-id-eleonor",
  "email": "patient@example.com",
  "diagnostics": [
    {
      "code": "D01",
      "description": "Gripe común",
      "confidence": 0.85
    }
  ],
  "medications": [
    {
      "name": "Paracetamol",
      "dosage": "500mg",
      "frequency": "Cada 8 horas"
    }
  ]
}
