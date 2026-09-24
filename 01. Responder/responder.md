# Responder

Responder es una herramienta de seguridad utilizada para evaluar protocolos de resolución de nombres y autenticación en redes Windows, especialmente LLMNR, NBT-NS y mDNS.

En una prueba controlada, Responder puede detectar solicitudes de resolución de nombres que no fueron resueltas correctamente y responder haciéndose pasar por el recurso solicitado. Esto puede provocar que un equipo Windows intente autenticarse contra el equipo que ejecuta Responder.

## Preparación del Entorno

| Componente                 | Preparación                                                       |
| -------------------------- | ----------------------------------------------------------------- |
| **Kali Linux**             | Máquina destinada a las pruebas de seguridad                      |
| **Windows 10**             | Equipo de prueba unido al dominio                                 |
| **Controlador de dominio** | Windows Server con el dominio `raynex.lab`                        |
| **Red**                    | Todas las máquinas conectadas al mismo segmento de laboratorio    |

## Flujo de la Etapa

```
┌─────────────────────┐
│      Windows 10     │
│   Equipo de prueba  │
└──────────┬──────────┘
           │
           │ 1. Intenta acceder a:
           │    \\ARCHIVO-SRV\Publico
           │
           │    DNS no encuentra el nombre
           ▼
┌──────────────────────────────┐
│       Red del laboratorio    │
│                              │
│       LLMNR / NBT-NS         │
│                              │
│  "¿Quién es ARCHIVO-SRV?"    │
└──────────────┬───────────────┘
               │
               │ 2. Responder recibe
               │    la solicitud
               ▼
┌─────────────────────┐
│      Kali Linux     │
│      Responder      │
└──────────┬──────────┘
           │
           │ 3. Responde:
           │    "ARCHIVO-SRV soy yo"
           ▼
┌─────────────────────┐
│      Windows 10     │
│                     │
│  4. Intenta realizar│
│     autenticación   │
└─────────────────────┘
```
En esta etapa, el equipo Windows intenta resolver un recurso que no puede localizar mediante DNS. Al recurrir a mecanismos como LLMNR/NBT-NS, Responder recibe la solicitud y proporciona una respuesta indicando que el recurso solicitado se encuentra en el equipo atacante. De esta forma, Responder suplanta la resolución del recurso, provocando que Windows dirija la comunicación hacia Kali.
