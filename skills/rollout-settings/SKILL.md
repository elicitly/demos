---
name: rollout-settings
description: Elicitly demo (starts nothing). Collect staged-rollout settings for the sample Brightwater Portal release in one form. Use only when the user asks to set up the Brightwater Portal demo rollout or to run the rollout-settings demo.
license: MIT-0
compatibility: Elicitly Free or Pro (elicit_form) in a host that renders form elicitation; see https://www.elicitly.ai/docs/elicitation/support-matrix/
---

# Rollout settings

> **Demo.** Uses made-up sample data from `assets/`, connects to no real system, and changes nothing. It's a reference for how to use Elicitly: adapt it to your own data and systems.

One `elicit_form` dialog collects every answer the rollout needs — text, a
number, a toggle, a single choice and a multi-choice — instead of five rounds
of chat questions.

## Steps

1. Call `elicit_form` with `timeoutSeconds: 600` (a five-field form takes a
   while to fill in), the message `Configure the Brightwater Portal v3.2.0
   rollout`, and this `requestedSchema`:

   ```json
   {
     "type": "object",
     "properties": {
       "releaseName": { "type": "string", "title": "Release name", "description": "Shown in the changelog", "maxLength": 50 },
       "rolloutPercent": { "type": "integer", "title": "Initial rollout %", "minimum": 0, "maximum": 100, "default": 10 },
       "notifyCustomers": { "type": "boolean", "title": "Email customers", "default": false },
       "channel": {
         "type": "string",
         "title": "Channel",
         "oneOf": [
           { "const": "stable", "title": "Stable" },
           { "const": "beta", "title": "Beta" },
           { "const": "canary", "title": "Canary" }
         ],
         "default": "beta"
       },
       "regions": {
         "type": "array",
         "title": "Regions",
         "minItems": 1,
         "items": { "type": "string", "enum": ["us-east", "eu-west", "ap-south"] },
         "default": ["us-east"]
       }
     },
     "required": ["releaseName", "rolloutPercent", "channel", "regions"]
   }
   ```

2. Act on `action`:
   - `accept`: restate the plan in one sentence from `content` (for example,
     "Rolling out 'Autumn release' to 10% of beta users in us-east, without
     customer email."). This demo starts nothing; say "In a real skill, the
     rollout would start here."
   - `decline` or `cancel`: acknowledge and stop.
   - `error`: the dialog couldn't be shown or timed out. Don't guess the
     settings; offer to try again.
