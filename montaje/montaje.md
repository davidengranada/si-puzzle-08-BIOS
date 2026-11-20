# SI · UT2 — Ficha de taller: montaje y revisión de un ordenador

## 1. Orden de trabajo

**Fecha:** 16/11/2026  **Puesto:** ____________________  **Equipo / etiqueta:** ____________________

**Integrantes del grupo (2 o 3):**

1. Nombre y apellidos: David Martinez do Nascimento
2. Nombre y apellidos: Sergio Alvarez Marfil
3. Nombre y apellidos (si procede): __________________________________

> **Equipo A:** ordenador de prácticas utilizado para el montaje o la revisión. Puede estar averiado; no se exige que arranque.
>
> **Equipo B:** vuestro propio ordenador funcional. Se utiliza a partir del apartado 9 para analizar el arranque y el hardware desde Linux.

## 2. Recepción e inspección visual · Equipo A

**Trabajo previsto:**



- [x] Desmontaje y montaje
- [ ] Revisión / diagnóstico
- [ ] Otro: ___________________________________

**Estado al recibirlo:**

- [ ] Completo
- [ ] Faltan piezas
- [ ] Sucio
- [ ] Daños visibles

**Síntomas conocidos, piezas ausentes o daños observados:**

________________________________________________________________________

________________________________________________________________________

## 3. Seguridad y preparación · Equipo A

- [X] Equipo desconectado de la corriente y de los periféricos.
- [X] Botón de encendido pulsado tras desconectar.
- [X] Superficie despejada y piezas organizadas.
- [X] Estado inicial y conexiones fotografiados.

**Herramientas utilizadas:** destornilladores

**No abráis la fuente ni forcéis piezas.** Ante daños o baterías, avisad al profesor.

## 4. Componentes identificados · Equipo A

Anotad lo que podáis verificar. Si no se distingue, escribid «no identificado».

| Componente | Marca / modelo | Dato observado |
|---|---|---|
| Placa base | Gigabyte GA-H81M-D2V | Socket 1150, DDR3, micro-ATX |
| Procesador | Intel, modelo no identificado | Socket 1150 (tapado por la pasta) |
| RAM | no identificado | DDR3 (según la placa) |
| Almacenamiento | WD Blue WD5000AAKX | HDD 500 GB, SATA, 16 MB caché |
| Fuente | no identificado | |
| Disipador / ventilador | Intel E97379-001 (Nidec) | 12 V, 0,28 A, ventilador de 4 pines |
| Tarjetas / otros | no identificado | |

## 5. Conexiones y observaciones · Equipo A

Identificad y marcad las conexiones presentes y comprobadas:

- [x] Alimentación de la placa
- [x] Alimentación de la CPU
- [x] Ventilador de la CPU
- [x] Datos de almacenamiento
- [x] Alimentación del disco
- [x] Panel frontal

**¿Hay algún cable suelto, conector dañado o conexión que no sepáis identificar?**

________________________________________________________________________

________________________________________________________________________

**Fotografías de referencia (nombre de archivo o ubicación):**

Carpeta `images/`: `03-cable-photos.jpg`, `04-cable-photos-2.jpg` (estado inicial) y `05`–`09` (cada conector).

No retiréis la CPU ni el disipador sin indicación del profesor. Si se retira el disipador, consultad sobre limpieza y pasta térmica antes de volver a instalarlo.

## 6. Registro del trabajo · Equipo A

Registrad únicamente lo que hayáis hecho; marcad **N/P** si no procede.

| Operación | Hecho | N/P | Foto / observaciones |
|---|:---:|:---:|---|
| Apertura y fotos iniciales | ☒ | ☐ | `01`–`04` |
| Desconexión y organización de cables | ☒ | ☐ | `05`–`09` |
| Desmontaje / montaje de memoria | ☐ | ☐ | |
| Revisión / montaje de almacenamiento | ☒ | ☐ | `10` |
| CPU y disipador, si se autoriza | ☒ | ☐ | `11`–`14`, `16`: limpieza y pasta térmica nueva (Arctic) |
| Tarjetas de expansión | ☐ | ☐ | |
| Reconexión y orden de cables | ☐ | ☐ | |
| Cierre y limpieza del puesto | ☐ | ☐ | |

## 7. Incidencia o reparación · Equipo A

**Problema encontrado / hipótesis** (si no hay, indicadlo):

________________________________________________________________________

________________________________________________________________________

**Acción realizada y resultado observado:**

________________________________________________________________________

________________________________________________________________________

________________________________________________________________________

## 8. Comprobación final · Equipo A

- [ ] Piezas sujetas.
- [ ] RAM encajada.
- [ ] Cables revisados.
- [ ] Sin tornillos sueltos.
- [ ] Ventilador de CPU conectado.
- [ ] Puesto recogido.

**¿Encendido autorizado?** ☐ Sí  ☐ No

**Resultado / motivo:** ___________________________________________________

________________________________________________________________________

Una observación no demuestra por sí sola la causa de una avería.

---

## 9. Identificación y arranque · Equipo B

Utilizad vuestro propio ordenador funcional para los siguientes apartados.

**Equipo:** ☒ Portátil (Victus by HP Gaming Laptop 15-fa2xxx)  ☐ Sobremesa  ☐ Otro: ___________________________

**Linux:** ☒ Instalado directamente  ☐ Máquina virtual

**Sistema operativo y versión:** Linux Mint 22.3 (kernel 7.0.0-43-generic)

**Si es virtual: sistema anfitrión y programa de virtualización:** No procede

**¿Arranca con normalidad? ¿Qué observáis desde el encendido hasta el inicio?**

Sí. Se ve el logo de HP (firmware), luego el gestor de arranque GRUB, la carga de Linux y por último el escritorio. Según `systemd-analyze`, tarda 25 s: firmware 5,3 s + gestor de arranque 6,5 s + kernel 3,8 s + espacio de usuario 9,5 s.

**¿Qué es el POST y en qué se diferencia de la UEFI y del sistema operativo?**

El POST (Power-On Self-Test) es la comprobación del hardware (CPU, RAM, dispositivos) que se hace nada más encender. La UEFI es el firmware de la placa: ejecuta el POST, guarda la configuración y carga el gestor de arranque. El sistema operativo (Linux) arranca después y es el que gestiona el equipo mientras se usa.

**¿Habéis accedido a la UEFI o consultado información de ella? ¿Qué dato habéis visto?**

La he consultado desde Linux (`/sys/class/dmi/id`, `mokutil`): firmware AMI, versión F.07 del 03/04/2026, arranque en modo UEFI y Secure Boot desactivado.

No cambiéis ajustes de UEFI sin indicación del profesor. Si no podéis acceder, indicadlo.

## 10. Linux: procesador · `lscpu`

Ejecutad `lscpu`. Adjuntad la salida revisada o indicad si el comando falla.

**Modelo / CPU presentada a Linux:** 13th Gen Intel Core i5-13420H

**Arquitectura:** x86_64  **CPU lógicas visibles:** 12

**¿Qué diferencia hay entre núcleo e hilo? ¿Qué podéis concluir de la salida?**

Un núcleo es una unidad física que ejecuta instrucciones; un hilo es una tarea que el sistema le asigna. Con Hyper-Threading, un núcleo puede llevar 2 hilos a la vez.

Hay 8 núcleos (4 de rendimiento con 2 hilos cada uno y 4 de eficiencia con 1 hilo), así que Linux ve 12 CPU lógicas. `lscpu` muestra «2 hilos por núcleo» aunque eso solo se cumple en los núcleos de rendimiento.

```text
Arquitectura:                         x86_64
CPU(s):                               12
Nombre del modelo:                    13th Gen Intel(R) Core(TM) i5-13420H
Hilo(s) de procesamiento por núcleo:  2
Núcleo(s) por «socket»:               8
«Socket(s)»:                          1
CPU MHz máx.:                         4600,0000
Virtualización:                       VT-x
Caché L3:                             12 MiB (1 instancia)
```

## 11. Linux: memoria · `free -h`

Adjuntad las salidas de los comandos. Si alguno falla o no está disponible, anotadlo. Antes de entregarlas, ocultad usuarios, nombres de equipo, números de serie y UUID. En una máquina virtual pueden mostrarse recursos virtuales, no el hardware físico completo.

**Memoria total:** 15 GiB  **Memoria disponible:** 8,6 GiB

**¿Qué significa «disponible» y por qué puede diferir de «libre»?**

«Libre» es la RAM que no se está usando para nada. «Disponible» es la que pueden usar los programas nuevos: la libre más la caché/búfer que el sistema suelta cuando hace falta. Por eso disponible (8,6 GiB) es mayor que libre (5,0 GiB).

```text
               total       usado       libre  compartido   búf/caché  disponible
Mem:            15Gi       6,6Gi       5,0Gi       914Mi       4,8Gi       8,6Gi
Inter:         2,0Gi          0B       2,0Gi
```

## 12. Linux: almacenamiento · `lsblk`

**Disco identificado:** `nvme0n1`, SSD NVMe de 476,9 GB

**Partición y punto de montaje, si aparecen:** `nvme0n1p5` → `/` (sistema) y `nvme0n1p1` → `/boot/efi` (arranque UEFI)

**Explicad la diferencia entre disco, partición y punto de montaje:**

El disco es el dispositivo físico. Una partición es una división lógica del disco. El punto de montaje es la carpeta desde la que Linux da acceso a una partición.

```text
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
nvme0n1     259:0    0 476,9G  0 disk
├─nvme0n1p1 259:1    0   200M  0 part /boot/efi
├─nvme0n1p2 259:2    0 244,2G  0 part
└─nvme0n1p5 259:3    0 232,6G  0 part /
```

## 13. Linux: dispositivos · `lspci` y `lsusb`

**Dispositivo 1 y función:** NVIDIA GeForce RTX 3050 6GB Laptop GPU (`lspci`): tarjeta gráfica dedicada

**Dispositivo 2 y función:** HP Wide Vision HD Camera (`lsusb`): webcam integrada por USB

**¿Por qué podría no aparecer un componente físico o mostrarse de otra forma en una máquina virtual?**

Porque la máquina virtual solo ve el hardware virtual que le da el programa de virtualización (gráfica, red o disco genéricos), no el hardware real. Un dispositivo solo aparece si se le pasa explícitamente a la VM.

```text
$ lspci   (resumen)
00:02.0 VGA compatible controller: Intel Corporation Raptor Lake-P [UHD Graphics]
01:00.0 VGA compatible controller: NVIDIA Corporation [GeForce RTX 3050 6GB Laptop GPU]
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller PM9C1a
03:00.0 Network controller: Realtek Semiconductor Co., Ltd. Device b520
04:00.0 Ethernet controller: Realtek RTL8111/8168/8211/8411 Gigabit Ethernet

$ lsusb   (resumen)
Bus 003 Device 002: ID 0408:5482 Quanta Computer, Inc. HP Wide Vision HD Camera
Bus 003 Device 003: ID 0bda:b86a Realtek Semiconductor Corp. Bluetooth Radio
```

## 14. Duda técnica y uso crítico de IA

Podéis usar una IA de Internet. No compartáis datos personales ni información privada del centro. Sin acceso a IA, resolved la duda con una fuente técnica.

**Herramienta utilizada y fecha:** Claude,Gemini y Chatgpt

**Pregunta planteada:**

Como pegar en markdown, como poner los cuadros "[]", como usar los comandos de bash en mk, como pegar algo de la terminal dentro de nvim ""+p.

Para el montaje los cables que salian del hdd y tenian muchas conexiones, foto a gemini y nos dijo el nombre

Chatgpt para entender la salida de los comandos de linux

**Respuesta resumida y afirmación concreta que decidisteis comprobar:**

________________________________________________________________________

________________________________________________________________________

**Fuente técnica o prueba utilizada y resultado:** confirmada / corregida / no verificada.

________________________________________________________________________

________________________________________________________________________

## 15. Valoración y entrega

**¿Qué paso fue más difícil y cómo lo resolvisteis?**

Al abrir esta caja tan antigua no estoy acostumbrado pero me costo y con calma fui poco a poco pero tarde, tambien lo mismo para algunos cables que costaba sacarlos o los tronillos del disipador que cuesta apretarlos

*¿Qué relación existe entre el montaje y la información de Linux? Recordad que son equipos distintos.**

Si el montaje falla lo que sea el equipo directamente no arranca, asi que lo primero no puede fallar y por otra parte es curioso como puedes saber todos tus componentes sin tener que verlos, dentro del software puedes sacar toda la informacion que quieras de los componentes y si van bien o fallan

**¿Qué haríais de otra manera en un próximo montaje?**

________________________________________________________________________

________________________________________________________________________

## LINK REPO

****

Antes de entregar:

- [ ] Ficha completa.
- [ ] Fotos identificadas.
- [ ] Salidas de Linux revisadas.
