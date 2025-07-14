# Monitor de Recursos del Servidor con cAdvisor

Este proyecto implementa un sistema de monitoreo de recursos del servidor utilizando cAdvisor (Container Advisor) de Google, integrado con Traefik como proxy inverso.

## Características

- Monitoreo en tiempo real de recursos del sistema (CPU, memoria, red, etc.)
- Interfaz web intuitiva
- Integración con Docker
- Seguridad con HTTPS a través de Traefik
- Renovación automática de certificados SSL

## Requisitos Previos

- Docker y Docker Compose instalados
- Red Docker llamada `proxy` creada previamente
- Servidor Traefik configurado y en ejecución
- Dominio configurado para apuntar a tu servidor

## Estructura del Proyecto

```
monitor/
├── docker-compose.yml
└── README.md
```

## Configuración

1. **Crea el directorio del proyecto**:
   ```bash
   mkdir -p ~/monitor
   cd ~/monitor
   ```

2. **Crea el archivo `docker-compose.yml`** con el contenido proporcionado.

## Despliegue

1. **Inicia el servicio de monitoreo**:
   ```bash
   docker-compose up -d
   ```

2. **Verifica que el contenedor esté en ejecución**:
   ```bash
   docker ps
   ```

## Acceso

Una vez desplegado, podrás acceder a la interfaz de cAdvisor en:
- https://tu-dominio.com

## Configuración de Red

Asegúrate de que la red `proxy` esté creada antes de desplegar:
```bash
docker network create proxy
```

## Personalización

### Cambiar el dominio
Para cambiar el dominio predeterminado (`tu-dominio.com`), modifica la siguiente línea en `docker-compose.yml`:
```yaml
- "traefik.http.routers.cadvisor.rule=Host(`tu-dominio.com`)"
```

### Cambiar el puerto de cAdvisor
Si necesitas cambiar el puerto interno de cAdvisor (por defecto 8080), actualiza:
```yaml
- "traefik.http.services.cadvisor.loadbalancer.server.port=NUEVO_PUERTO"
```

## Seguridad

- El acceso a cAdvisor está protegido por HTTPS
- Asegúrate de que tu firewall permita el tráfico en los puertos 80 y 443
- Considera agregar autenticación básica para mayor seguridad

## Solución de Problemas

- **No se puede acceder al panel**: Verifica que el dominio esté configurado correctamente y apunte a la IP de tu servidor.
- **Problemas de red**: Asegúrate de que la red `proxy` exista y que Traefik esté en ejecución.
- **Ver logs**: Usa `docker-compose logs -f` para ver los logs en tiempo real.

## Mantenimiento

Para detener el servicio:
```bash
docker-compose down
```

Para actualizar cAdvisor a la última versión:
```bash
docker-compose pull
docker-compose up -d
```

## Licencia

Este proyecto está bajo la licencia MIT.
