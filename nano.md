# Nano Guide for n8n-fork

## Overview
[Brief description of the app/agent]

## Using the Splinter Persona

This app/agent can utilize the Master Splinter persona from Honcho to adjust and improve prompt outputs.

### How to Use

1. Import the Honcho connector from the weretradeIT connectors package:
   ```typescript
   import { getConnector, type HonchoClient } from '@weretradeit/connectors';
   ```

2. Initialize the connector (typically once at startup):
   ```typescript
   const honchoConfig = {
     apiKey: process.env.HONCHO_API_KEY!, // From keychain or environment
     workspaceId: 'assistant-agents',      // Where Splinter lives
     peerId: 'splinter'                    // The Master Splinter persona
   };

   const honcho = getConnector('honcho') as HonchoClient;
   ```

3. Retrieve the persona to inform your prompts:
   ```typescript
   async function getSplinterGuidance() {
     const persona = await honcho.getPersona();
     // Use persona.content to enhance your system prompts or context
     return persona;
   }
   ```

4. For iterative improvement, use calibration pairs:
   ```typescript
   await honcho.addCalibrationPair({
     input: "User's original query or prompt",
     claudeOutput: "Initial AI response",
     floriCorrection: "Spartan-style corrected guidance from Splinter's perspective",
     context: "optional-context-tag",
     lessons: "Key lessons learned"
   });
   ```

### Best Practices

- Use the persona to provide wisdom, patience, and mentorship in responses.
- For technical questions, emphasize discipline, foundational understanding, and clean solutions.
- For interpersonal issues, focus on understanding, compassion, and conflict resolution through wisdom.
- Regularly sync the persona to ensure you have the latest version:
   ```typescript
   await honcho.syncLocalPersona();
   ```

## References

- Honcho Connector: @weretradeit/connectors
- Splinter Persona: Available in Honcho workspace 'assistant-agents' as peer 'splinter'
