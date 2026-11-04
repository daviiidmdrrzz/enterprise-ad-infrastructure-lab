# Enterprise Hybrid Infrastructure & AD DS Automation Lab 🏢⚡

Despliegue y administración integral de una infraestructura corporativa multisede basada en **Windows Server 2022**, segmentada y protegida perimetralmente con **pfSense Firewall**, automatizada mediante scripts de **PowerShell** y endurecida mediante directivas avanzadas de seguridad (**GPO & PSO**).

---

> 💡 **Nota de Arquitectura:** Este repositorio gestiona el núcleo de identidades, servicios de red y seguridad perimetral de la infraestructura corporativa. El subsistema de telefonía IP integrada y archivado cloud asociado a este entorno se encuentra documentado en: [cloud-callcenter-voip-archiver](https://github.com/daviiidmdrrzz/cloud-callcenter-voip-archiver).

---

## 📌 Escenario Empresarial Simulado

El proyecto implementa la infraestructura de red y servicios de directorio para **InnovaTech Global**, una organización distribuida que requiere:
1. **Seguridad perimetral y segmentación lógica:** Filtrado de tráfico, control de acceso entre departamentos y salida controlada a Internet a través de un firewall dedicado (**pfSense**).
2. **Servicios de Directorio tolerantes a fallos:** Topología de **Active Directory Domain Services (AD DS)** multisede con replicación consistente y resolución interna de nombres.
3. **Gobierno y ciclo de vida de puestos (PIU):** Estandarización de parque informático mediante scripts para el renombrado masivo de equipos retirados/sustituidos (`-OLD`) asegurando trazabilidad en auditorías.
4. **Hardening de identidades:** Separación estricta de privilegios administrativos mediante directivas de contraseñas afinadas (**PSO**) y directivas de grupo (**GPO**).

---

## 🏗️ Topología de Red y Arquitectura

```text
                                [ INTERNET / WAN ]
                                        │
                         ┌──────────────┴──────────────┐
                         │      pfSense Firewall       │
                         │   (Gateway, NAT, Routing)   │
                         └──────────────┬──────────────┘
                                        │
       ┌────────────────────────────────┼────────────────────────────────┐
       │                                │                                │
[ VLAN 10 - Core / Servers ]  [ VLAN 20 - VoIP / Comms ]    [ VLAN 30 - Workstations / PIU ]
Subnet: 172.16.10.0/24        Subnet: 172.16.20.0/24        Subnet: 172.16.30.0/24
Gateway: 172.16.10.1          Gateway: 172.16.20.1          Gateway: 172.16.30.1
       │                                │                                │
 ├── SRV-DC01 (172.16.10.10)     └── SRV-PBX (172.16.20.10)      ├── WS-CORP-01 (172.16.30.50)
 │   (PDC, DNS, DHCP)                 (VoIP / Asterisk)          └── WS-CORP-02 (172.16.30.51)
 └── SRV-DC02 (172.16.10.11)                                          (Puestos de Usuario)
     (BDC Replicado, DNS)
