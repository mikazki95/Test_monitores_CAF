# Test_monitores_CAF
Este repositorio es para crear test de perifericos para un sistema QNX de CAF
# Proyecto Pixy CAF - Diagnóstico y Reparación

## 1. Acceso y Red
- Cambiar IP: `ifconfig en0 192.168.1.185 netmask 255.255.255.0`
- Ruta por defecto: `route add default 192.168.1.1`
- Iniciar Telnet: `inetd &`
- Conectarse desde PC: `telnet 192.168.1.185`

## 2. Arranque de QNX
- Script maestro: `/etc/system/sysinit`
- Script de CAF: `/etc/rc.d/rc.cafinit`
- Script local: `/etc/rc.d/rc.local`
- Lanzador CAF: `/home/traintic/bin/caf_start.ksh`
- Lanzar con log: `./caf_start.ksh > /tmp/caf.log 2>&1 &`

## 3. Driver MVB (XCommSrv)
- Binario: `/home/traintic/bin/XCommSrv_SIEPC104`
- Lanzar manual (si es necesario): `/tmp/XCommSrv HAS_MVB_BUS=1 ...`
- **Solución al error `NO_MVBC`**: En BIOS, `Enable Memory Gap` = `Extended`
- Ver log: `cat /tmp/mvb_log.txt`

## 4. Diagnóstico Rápido
- Ver procesos: `pidin | grep -E "XCommSrv|MMEX|HMIBoot"`
- Ver log del sistema: `sloginfo`
- Ver log del MVB: `cat /tmp/mvb_log.txt`

## 5. Recuperación de Contraseña (QNX)
- Montar partición QNX4 desde Tiny Core: `mount -t qnx4 /dev/sda1 /mnt/qnx`
- Editar shadow: `vi /mnt/qnx/etc/shadow` (dejar `root::...`)
- Generar hash DES: `perl -e 'print crypt("nueva", "AB"), "\n"'`
