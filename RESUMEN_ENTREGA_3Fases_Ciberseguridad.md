# Proyecto Final de Ciberseguridad - 4Geeks Academy

**Sergio Maturana Mena**  
*Bootcamp de Ciberseguridad*  
*Fecha: Febrero 2026*  
[GitHub Profile](https://github.com/SergioMaturana) | [LinkedIn](https://www.linkedin.com/in/sergio-maturana-mena-748a141bb/)

[![Cybersecurity Project](https://img.shields.io/badge/4Geeks%20Academy-Final%20Project-brightgreen)](https://4geeksacademy.com/es/coding-bootcamps/curso-ciberseguridad) [![NIST 800-61](https://img.shields.io/badge/NIST%20800-61-blue)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) [![ISO 27001](https://img.shields.io/badge/ISO%202701-SGSI-orange)](https://www.iso.org/standard/27001)

## 📋 Resumen Ejecutivo

Restauración de servidor Debian comprometido (8 octubre 2024). **3 Fases**:

1. **Fase 1**: Análisis forense (Autopsy), SSH brute force root (192.168.0.134), vsftpd anónimo, hardening.
2. **Fase 2**: Nmap (192.168.100.20), WordPress REST API enumeración (`/wp-json/wp/v2/users`), Hydra brute force `wordpress-user`.
3. **Fase 3**: NIST 800-61 + ISO 27001 SGSI (riesgos, DLP, PHVA).

## 🛡️ Arquitectura Final Propuesta

![Diagrama de Red Segura](Diagrama_Red.jpg)

## 📂 Estructura del Proyecto

cybersecurity-final-project-sergio-maturana/
├── 📄 README.md
├── 🔍 AUTOPSY.docx (Fase 1 Forense)
├── 🛡️ INFORME_TECNICO_INCIDENTE_DE_SEGURIDAD-copia.docx (Fase 1)
├── 🎯 INFORME_TECNICO_AUDITORIA_EXPORTACION.docx (Fase 2)
├── 📋 PLAN_RESPUESTA_INCIDENTES_CERTIFICACION.docx (Fase 3)
├── 🗺️ Diagrama_Red.jpg
└── 📁 evidencias/ (capturas opcionales)

## 📋 Detalle por Fase

### Fase 1: Corrección Hackeo
- **Hallazgos** (`AUTOPSY.docx`): SSH brute force root (192.168.0.134), vsftpd (anon enable), net-tools, socket `/tmp/ssh-XXXXXXGZVLks`, permisos 777 `/wp-content/uploads`.
- **Acciones** (`INFORME_TECNICO_INCIDENTE`): `systemctl stop/disable vsftpd`, chmod 644/755, UFW (solo 22/80/443), `PermitRootLogin no`, `passwd root`. Rootkits descartados manualmente. [file:2][file:3]

### Fase 2: Nueva Vulnerabilidad
- **Escaneo**: `nmap -p- -sV -sC 192.168.100.20` → Puerto 80 Apache/WordPress.
- **Exploit**: Enumeración `/wp-json/wp/v2/users` → usuario `wordpress-user` → Hydra + rockyou.txt en `wp-login.php`.
- **Corrección**: `.htaccess` bloquea REST API y `?author=n` (403 Forbidden verificado). [file:4]

### Fase 3: Plan Respuesta SGSI
- **NIST 800-61**: Preparación (Fail2Ban), detección logs, contención UFW, erradicación parches.
- **ISO 27001**: Tabla riesgos (fuerza bruta ALTA), políticas PoLP, backups 3-2-1 cifrados, PHVA. [file:5]

## 🎯 Recomendaciones Finales
- Fail2Ban, SSH keys only, SFTP vs FTP, WAF, MFA WordPress. [file:3][file:5]

## 📚 Referencias
- [Proyecto Oficial](https://github.com/breatheco-de/cybersecurity-final-project)

---

⭐ **¡Gracias por la revisión!** *Bootcamp 4Geeks Cybersecurity*

