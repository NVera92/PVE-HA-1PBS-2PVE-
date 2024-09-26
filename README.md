# PVE-HA-1PBS-2PVE-PROXMOX-LINSTOR

Documentacion para lograr High Aviability en Proxmox con 2 nodos PVE y 1 PBS con Linstor

Herramental 3 Pc´s

En 2 instalar Proxmox-PVE y PBS en la restante

Se corren los scripts para el post-install de TTEK segun corresponda a su variante, en los de PVE no deshabilitar HA.

Recurso:  https://tteck.github.io/Proxmox/#proxmox-ve-tools

El PBS va a ser elegido como controlador y se le va a instalar el kernel de PVE (pve-kernel-6.2) se va a modificar su source.list para admitir los paquetes de PVE.

Recurso:  https://forum.proxmox.com/threads/install-pve-on-an-existing-pbs-server.133572/
          https://pve.proxmox.com/wiki/Install_Proxmox_VE_on_Debian_11_Bullseye (en mi caso utilice la version Wormbook, remplace la version Bullseye por Wormbook)

Se siguen las instrucciones del video oficial de instalación de Linstor con Proxmox.

Recursos: https://linbit.com/blog/linstor-setup-proxmox-ve-volumes/
          https://www.youtube.com/watch?v=pP7nS_rmhmE&embeds_referring_euri=https%3A%2F%2Flinbit.com%2F

Se crea el cluster y se agregan los nodos via comando, lo cual permite visualizar en cualquiera de los PVE los 3 equipos en el GUI.

Recursos:  https://pve.proxmox.com/wiki/Cluster_Manager

Una vez armado el cluster, se crea un HA-GROUP que solo contenga a los PVE, mi intencion es que solo estos ejecuten las VM y CT.

Se crea una VM en cualquiera de los PVE, una vez listo y desmontado el ISO, se prueba migrar hacia el otro PVE, si se realiza de manera exitosa, vamos con la prueba de
manejo de HA, se produce desconexion del equipo que contiene la VM y aproximadamente al minuto y medio el cluster registra la caida del equipo y un minuto y medio más
deberia realizar la migracíon al PVE restante iniciar automaticamente recuperando asi el servicio.
