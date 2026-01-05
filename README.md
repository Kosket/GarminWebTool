# 🏃‍♂️ AI Plan Importer (Intervals.icu)

> Herramienta profesional para importar planes JSON a Intervals.icu con validación de seguridad estricta para Garmin.

## ⚙️ Configuración
Necesitas tu **API Key** y **Athlete ID** de Intervals.icu (Settings > Developer Settings).

## 🤖 PROMPT MAESTRO (Copia esto a la IA)

Usa este prompt EXACTO para generar los entrenamientos:

\`\`\`text
Actúa como entrenador de running de élite. Genera un plan estructurado en JSON.
MIS DATOS: [Objetivo, Nivel, Días disponibles]

REGLAS DE SISTEMA (CRÍTICO):
1. FORMATO: JSON estricto ("workout_plans" -> "weeks" -> "days").
2. REGLA DE HARDWARE (MEZCLA PROHIBIDA):
   - Una sesión debe ser EXCLUSIVAMENTE de "Pace_Zone" (Ritmo) o de "Heart_Rate_Zone" (Pulso).
   - NUNCA mezcles ambos tipos en el mismo día (ej: Calentamiento por pulso y series por ritmo = ERROR).
   - Si haces series por ritmo, el calentamiento/enfriamiento debe ser "Open" (sensaciones) o "Pace_Zone", pero NO pulso.
3. ZONAS DE PULSO (1-7):
   - Usa SOLO números enteros del 1 al 7. NO uses BPMs.
   - Referencia de Zonas (Intensidad):
     Z1: Recuperación / Muy suave
     Z2: Aeróbico Extensivo / Rodaje
     Z3: Tempo / Aeróbico Intensivo
     Z4: Umbral (Sub-Threshold)
     Z5: Super-Umbral (VO2max bajo)
     Z6: Capacidad Aeróbica (VO2max alto)
     Z7: Anaeróbico / Sprint
4. DISTANCIA:
   - Siempre en METROS (ej: 12000, 400).
5. NOTAS:
   - Usa el campo "notes" para instrucciones clave.
   - NO uses símbolos matemáticos como '<' o '>'.

ESTRUCTURA JSON EJEMPLO:
{
  "workout_plans": [
    {
      "weeks": [
        {
          "days": [
            {
              "session_name": "2026-01-20 Rodaje Z2",
              "session_type": "Run",
              "steps": [
                { 
                  "step_type": "Run", 
                  "duration_type": "Distance", "duration_value": 10000, 
                  "target_type": "Heart_Rate_Zone", "target_value_min": 2, "target_value_max": 2,
                  "notes": "Ritmo constante" 
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
\`\`\`
