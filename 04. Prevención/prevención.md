## Medidas de prevención

- Deshabilitar LLMNR y NBT-NS mediante GPO en los equipos del dominio.
- Implementar SMB Signing en servidores y estaciones de trabajo que lo requieran.
- Establecer políticas de contraseñas robustas, evitando contraseñas comunes o reutilizadas.
- Aplicar mínimo privilegio, especialmente sobre cuentas con acceso administrativo.
- Segmentar la red, limitando las comunicaciones SMB entre estaciones y servidores.

Estas medidas reducen la posibilidad de que un atacante pueda provocar, capturar y posteriormente utilizar autenticaciones NTLM dentro de la red.

**Joseph González** - Best H4cker in Town :) 
