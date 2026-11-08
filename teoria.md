# Teoría · Pieza 08: BIOS / UEFI

**Grupo:** David Martinez do Nascimento · Sergio Alvarez Marfil



## Conceptos clave

- **Firmware:** lo primero que se ejecuta al encender el PC. Está en un chip flash de la placa base, prepara el hardware y deja listo el gestor de arranque.
- **BIOS clásica:** viene del IBM PC (1981). Trabaja en modo real de 16 bits, con solo 1 MiB de memoria direccionable, y arranca ejecutando el primer sector del disco (el MBR).
- **UEFI:** la sustituta de la BIOS. Arranca archivos `.efi` guardados en la ESP y ofrece más servicios (red, drivers, Secure Boot). Su menú puede ser gráfico, pero no tiene por qué.
- **POST:** el chequeo que hace el firmware nada más encender (RAM, dispositivos...). Si falla, avisa con pitidos, LEDs o códigos en un display, según la placa. Hay que mirar el manual.
- **Pila CR2032:** mantiene el reloj (y los ajustes CMOS en placas antiguas). En UEFI, el orden de arranque (`BootOrder`, `Boot####`) se guarda en la NVRAM y no depende de la pila.
- **ESP:** partición FAT32 donde viven los cargadores `.efi`. Si no hay entrada en la NVRAM, se usa la ruta de reserva `\EFI\BOOT\BOOTX64.EFI`.
- **MBR vs GPT:** MBR admite 4 particiones primarias y unos 2 TiB. GPT usa direcciones de 64 bits, guarda tablas redundantes con CRC y suele permitir 128 particiones.
- **Secure Boot:** comprueba las firmas de lo que se va a arrancar. `db` es la lista de lo permitido y `dbx` la de lo revocado. No te protege de todo el malware.
- **TPM:** chip (o fTPM, integrado en la CPU) que guarda medidas del arranque en sus registros PCR. Se usa para liberar claves de cifrado (LUKS, BitLocker).

Cadena de arranque de Ubuntu con Secure Boot:
`Encendido → POST → shim → GRUB → kernel + initramfs → systemd → login`

## Tabla resumen

| Tipo | Dato clave | Cuándo se usa |
|---|---|---|
| BIOS clásica | 16 bits, MBR, sin Secure Boot | Equipos antiguos o modo Legacy/CSM |
| UEFI | 64 bits, GPT + ESP, Secure Boot | PCs actuales, Windows 11, Ubuntu |
| MBR | 4 primarias, ~2 TiB | Discos pequeños y BIOS |
| GPT | 128 entradas, CRC, copia de seguridad | Discos grandes y UEFI |
| Secure Boot | `db` permite, `dbx` revoca | Evitar cargadores no confiables |
| TPM 2.0 | Registros PCR, claves | Windows 11 y cifrado de disco |

## Datos que hay que saberse

- 256 Mbit son **32 MB** (cuidado con bits y bytes).
- BIOS en modo real: **1 MiB**. UEFI de 64 bits supera ese límite.
- MBR: **~2 TiB** con sectores de 512 B. GPT: 128 particiones habituales.
- Pila de la placa: **CR2032, 3 V**.
- UEFI y GPT **no son sinónimos**.
- Windows 11 pide **TPM 2.0 y UEFI "Secure Boot capable"** (no hace falta que esté activado).
- Comandos en Linux:
  - `[ -d /sys/firmware/efi ] && echo UEFI` → ¿arrancó en UEFI?
  - `mokutil --sb-state` → estado de Secure Boot
  - `efibootmgr -v` → entradas de arranque
  - `sudo dmidecode -t bios` → datos del firmware
- Fallos típicos:
  - Pierde la hora al apagar: pila agotada.
  - "No bootable device": modo UEFI/Legacy mal elegido, o disco MBR con firmware UEFI.
  - Ubuntu no arranca con Secure Boot: módulos sin firmar (se firman con MOK).
  - Pierdes la clave de LUKS o BitLocker al cambiar el firmware, porque cambian los PCR.

## Preguntas tipo test (8)

1. ¿Qué hace el firmware nada más encender el equipo?
   - a) Carga directamente el entorno de escritorio
   - b) Inicializa el hardware y prepara el gestor de arranque  ← correcta
   - c) Instala los drivers del sistema operativo
   - d) Formatea la ESP
   - Explicación: el firmware prepara el hardware y el gestor de arranque carga después el sistema operativo.

2. ¿Qué características tiene el entorno de la BIOS clásica?
   - a) 64 bits y 4 GiB de memoria
   - b) 32 bits y GPT obligatorio
   - c) 16 bits en modo real y 1 MiB direccionable  ← correcta
   - d) 64 bits con Secure Boot
   - Explicación: es el entorno heredado del IBM PC.

3. ¿Qué es la ESP?
   - a) Un chip de la placa que guarda el firmware
   - b) Una partición FAT32 con los cargadores `.efi`  ← correcta
   - c) Un registro del TPM
   - d) El primer sector del disco
   - Explicación: UEFI arranca los archivos `.efi` que están en la ESP.

4. ¿Qué límite tiene MBR con sectores de 512 B?
   - a) 128 particiones y 1 PiB
   - b) 4 primarias y unos 2 TiB  ← correcta
   - c) 2 primarias y 512 GiB
   - d) No tiene límites
   - Explicación: por eso en discos grandes se usa GPT.

5. En Secure Boot, ¿qué contiene `dbx`?
   - a) Las firmas y claves autorizadas
   - b) Las claves del TPM
   - c) Los ajustes de la CMOS
   - d) Las firmas o claves revocadas  ← correcta
   - Explicación: `db` autoriza y `dbx` revoca.

6. ¿Cuál es el orden de arranque de Ubuntu con Secure Boot?
   - a) GRUB → shim → kernel
   - b) shim → GRUB → kernel  ← correcta
   - c) kernel → shim → GRUB
   - d) GRUB → kernel → shim
   - Explicación: el firmware valida shim, shim valida GRUB y GRUB valida el kernel.

7. ¿Qué exige Windows 11 en cuanto a firmware?
   - a) BIOS clásica y TPM 1.2
   - b) Solo Secure Boot activado, sin TPM
   - c) TPM 2.0 y UEFI compatible con Secure Boot  ← correcta
   - d) Cualquier firmware con 4 GB de RAM
   - Explicación: además deben cumplirse los requisitos de CPU, RAM y almacenamiento.

8. Un PC pierde la hora y la fecha cada vez que se apaga. ¿Cuál es la causa más probable?
   - a) Secure Boot desactivado
   - b) La ESP está dañada
   - c) Disco en GPT
   - d) La pila CR2032 está agotada  ← correcta
   - Explicación: la pila mantiene el reloj cuando el equipo está apagado.
