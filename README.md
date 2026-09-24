# LLMNR/NBT-NS Poisoning 

El LLMNR/NBT-NS Poisoning es una técnica que aprovecha mecanismos de resolución de nombres utilizados por Windows dentro de la red local. Cuando un equipo no puede resolver un nombre mediante DNS, puede recurrir a LLMNR o NBT-NS para intentar localizar el recurso mediante una consulta a otros dispositivos de la red.

En este escenario, Responder puede interceptar estas solicitudes y responder haciéndose pasar por el host solicitado. Si la víctima intenta conectarse al recurso controlado por el atacante, Windows puede iniciar un proceso de autenticación contra este sistema.

Como resultado, el atacante puede capturar material de autenticación NetNTLMv2, que posteriormente puede ser analizado o sometido a cracking offline para intentar recuperar la contraseña asociada.

## Flujo del Ataque

```
┌──────────────┐
│    Víctima   │
└──────┬───────┘
       │
       │ 1. Solicita un recurso inexistente
       │    (LLMNR / NBT-NS)
       ▼
┌────────────────────┐
│     Red local      │
└─────────┬──────────┘
          │
          │ 2. Responder recibe la solicitud
          ▼
┌────────────────────┐
│     Responder      │
│   (Atacante)       │
└─────────┬──────────┘
          │
          │ 3. Responde: "Ese recurso soy yo"
          │    → IP del atacante
          ▼
┌──────────────┐
│    Víctima   │
└──────┬───────┘
       │
       │ 4. Intenta conectarse al recurso
       │    y se autentica contra Responder
       ▼
┌────────────────────┐
│     Responder      │
│   (Atacante)       │
└─────────┬──────────┘
          │
          │ 5. Recibe la petición de autenticación
          │    y captura el desafío/respuesta
          ▼
┌────────────────────┐
│ NetNTLMv2 capturado│
└────────────────────┘
```

El punto clave del ataque es que la víctima inicia la autenticación. Responder no necesita conocer previamente las credenciales: provoca que el equipo víctima intente autenticarse contra el sistema controlado por el atacante y captura el material de autenticación generado durante ese proceso.
