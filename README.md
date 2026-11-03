# Enterprise Hybrid Infrastructure & AD DS Automation Lab 🏢⚡

Simulación y despliegue integral de una infraestructura corporativa multisede basada en **Windows Server 2022**, automatización de ciclo de vida con **PowerShell**, endurecimiento de seguridad (*Hardening*) y preparación para sincronización híbrida con **Microsoft Entra ID / AWS**.

---

## 📌 Escenario Empresarial Simulado

La empresa ficticia **InnovaTech Global** cuenta con una sede principal (Madrid HQ) y una delegación remota (Barcelona Branch). El objetivo del proyecto es:
1. Diseñar y desplegar una topología de Directorio Activo tolerante a fallos.
2. Estandarizar el ciclo de vida de identidades y equipos según normativas de auditoría corporativa.
3. Automatizar operativas repetitivas de N1/N2 mediante scripting para reducir errores manuales.
4. Aplicar políticas de mínimo privilegio y directivas de seguridad avanzadas.

---

## 🏗️ Arquitectura y Topología de Red

```text
[ Red Corporativa 172.16.0.0/16 ]
 │
 ├── Sede Madrid (HQ) [172.16.1.0/24]
 │    ├── SRV-DC01 (Windows Server 2022 - FSMO Roles, DNS, DHCP)
 │    └── WS-CORP-01 (Windows 11 Pro - Endpoint corporativo)
 │
 └── Sede Barcelona (Branch) [172.16.2.0/24]
      ├── SRV-DC02 (Windows Server 2022 - DC Adicional, Replicación)
      └── WS-CORP-02 (Windows 11 Pro - Endpoint corporativo)
