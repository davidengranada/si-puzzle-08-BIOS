# Teoría · Pieza 08: (BIOS/UEFI)

**Grupo:** David Martinez do Nascimento · Sergio Alvarez Marfil

## Presupuesto de espacio

| Sección de `teoria.md` | Palabras aprox. | Qué sacar del README |
|---|---|---|
| Conceptos clave | 250 | §1, §2 |
| Tabla resumen | 150 | §4 (BIOS vs UEFI) |
| Datos que hay que saberse | 150 | §3 (límites, comandos) |
| Test (8 preguntas) | 400 | todo lo anterior |

## 1. Conceptos clave (8–9 bullets, 1–2 líneas cada uno)

Sugerencia de contenido, ya resumido:

- **Firmware:** primer software que se ejecuta al encender; vive en memoria flash de la placa; inicializa el hardware y lanza el bootloader.
- **BIOS heredada:** IBM PC 1981, modo real 16 bits, 1 MiB direccionable, arranca desde el primer sector del disco (MBR).
- **UEFI:** sucesora estandarizada; 32/64 bits; carga archivos `.efi` desde la ESP; no exige menú gráfico.
- **POST:** comprobación inicial (RAM, dispositivos). Los errores se avisan con pitidos/LEDs/display según la placa (mirar el manual).
- **Pila CR2032 + CMOS/NVRAM:** la pila mantiene el reloj (y CMOS en diseños clásicos); en UEFI las variables de arranque (`BootOrder`, `Boot####`) están en NVRAM, no dependen de la pila.
- **ESP (EFI System Partition):** partición FAT32 con los cargadores `.efi`. Ruta de reserva: `\EFI\BOOT\BOOTX64.EFI`.
- **MBR vs GPT:** MBR = 4 primarias, ~2 TiB; GPT = direcciones de 64 bits, tablas redundantes + CRC, 128 entradas habituales.
- **Secure Boot:** valida firmas de los ejecutables de arranque. `db` = autorizados, `dbx` = revocados. No garantiza ausencia de malware.
- **TPM / Measured Boot:** chip (o fTPM) que guarda medidas en registros PCR; puede condicionar la liberación de una clave (LUKS/BitLocker).

Cadena de Ubuntu con Secure Boot (ponla en una línea, es muy de examen):
`Encendido → POST → shim → GRUB → kernel + initramfs → systemd → login`

## 2. Tabla resumen (BIOS vs UEFI, 5–6 filas)

Adapta la tabla del README §4 a las columnas de `teoria.md` (Tipo | Dato clave | Cuándo se usa):

| Tipo | Dato clave | Cuándo se usa |
|---|---|---|
| BIOS heredada | 16 bits, MBR, sin Secure Boot | Equipos antiguos / modo Legacy-CSM |
| UEFI | 64 bits, GPT + ESP, Secure Boot | PCs modernos, Windows 11, Ubuntu actual |
| MBR | 4 primarias, ~2 TiB | Discos pequeños / BIOS |
| GPT | 128 entradas, CRC, redundante | Discos grandes / UEFI |
| Secure Boot | `db`/`dbx`, firmas | Evitar cargadores no confiables |
| TPM 2.0 | PCR, claves | Windows 11, cifrado de disco |


