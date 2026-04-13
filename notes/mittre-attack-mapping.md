# MITRE ATT&CK Mapping | Forgotten Portal.

| Táctica | ID | Técnica | Aplicación en el laboratorio |
|---|---|---|---|
| Reconocimiento | T1595.001 | Active Scanning: IP Blocks | Escaneo de puertos con nmap |
| Reconocimiento | T1595.002 | Vulnerability Scanning | Enumeración de servicios con nmap -sV |
| Descubrimiento | T1083 | File and Directory Discovery | Enumeración con gobuster y ls |
| Descubrimiento | T1087.001 | Account Discovery: Local Account | Lectura de /etc/passwd y /home |
| Descubrimiento | T1082 | System Information Discovery | whoami e id para identificar usuario |
| Acceso inicial | T1190 | Exploit Public-Facing Application | Explotación del formulario de subida .php |
| Ejecución | T1059.004 | Unix Shell | Comandos via web shell y reverse shell |
| Persistencia | T1505.003 | Web Shell | Carga de shell.php en el servidor |
| Comando y control | T1071.001 | Web Protocols | Reverse shell via netcat sobre TCP |
| Acceso a credenciales | T1552.001 | Credentials in Files | Credenciales en Base64 en access_log |
| Acceso a credenciales | T1552.004 | Private Keys | Clave RSA replicada entre usuarios |
| Acceso a credenciales | T1552.003 | Bash History | Revisión de .bash_history de alice |
| Movimiento lateral | T1078.003 | Valid Accounts: Local | Credenciales de alice y bob |
| Movimiento lateral | T1021.004 | Remote Services: SSH | Acceso como bob via SSH con clave RSA |
| Escalación de privilegios | T1548.003 | Sudo and Sudo Caching | tar con sudo para obtener shell root |