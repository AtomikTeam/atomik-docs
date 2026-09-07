Changelog

Todos los cambios importantes de AtomikPE se documentan en este archivo.

[Unreleased]

Sistema de Eventos

- Conectado "PlayerMoveEvent" al movimiento de jugadores.
- Conectado "PlayerInteractEvent" a las interacciones con bloques.
- Conectado "PlayerTeleportEvent" con soporte de cancelación.
- Conectado "EntityDamageEvent" y "EntityDamageByEntityEvent" al sistema de daño.
- Conectado "PlayerDeathEvent" al ciclo de muerte del jugador.
- Conectado "InventoryClickEvent" a los inventarios de jugadores y cofres.
- Conectado "InventoryOpenEvent" a la apertura de cofres.
- Conectado "PlayerRespawnEvent" al sistema de respawn.

Combate

- Implementado un sistema funcional de daño para entidades.
- Añadido soporte para daño causado por otras entidades.
- Añadido control de salud y detección de muerte.
- Implementado el ataque cuerpo a cuerpo entre jugadores.
- Añadido cooldown de ataques a nivel del servidor.
- Implementadas las animaciones de daño y muerte mediante paquetes.
- Añadidas causas básicas de daño.
- Los jugadores muertos ya no pueden moverse ni atacar.

Respawn

- Implementado el formato legacy de "RespawnPacket".
- Añadido soporte para "ACTION_SPAWN_SAME_DIMENSION".
- Implementado "Player::respawn()".
- Añadida la posibilidad de modificar la posición de respawn mediante "PlayerRespawnEvent".
- Añadida sincronización del jugador con el cliente después del respawn.
- Corregido "PlayerRespawnEvent" para que no sea cancelable.

Persistencia de Tile Entities

- Implementada la carga de Tile Entities desde los chunks Anvil.
- Implementado el guardado de Tile Entities en los chunks Anvil.
- Añadida serialización NBT para cofres.
- Añadida deserialización NBT para cofres.
- Añadida serialización NBT para carteles.
- Añadida deserialización NBT para carteles.
- Añadido control del estado "dirty" de las Tile Entities.
- Añadido sistema de hidratación de Tile Entities por chunk.
- Los contenidos de los cofres ahora persisten después de reiniciar el servidor.

Almacenamiento de Mundos

- Corregida la creación de directorios para mundos nuevos.
- Evitados fallos silenciosos al guardar mundos cuando los directorios padre no existen.

Cambios

- Convertidos varios paquetes legacy que eran stubs en implementaciones funcionales.
- Actualizada la interfaz NBT de "Tile" para utilizar la implementación NBT real del proyecto.
- Actualizado el procesamiento de paquetes del jugador para los sistemas de interacción y contenedores.
- Mejorado el manejo de cancelación de eventos.
- Añadida la sincronización de Tile Entities antes de guardar los chunks modificados.

Correcciones

- Corregida la pérdida de contenido de cofres después de reiniciar el servidor.
- Corregido el sistema de daño y muerte de jugadores.
- Corregido el procesamiento del respawn de jugadores.
- Corregidos fallos silenciosos durante el guardado de mundos.
- Corregida la sincronización de Tile Entities que podía eliminar entidades sin cambios durante un guardado.

Pendiente

- "BlockUpdateEvent" mientras las actualizaciones programadas de bloques permanezcan desactivadas.
- Persistencia del contenido de "TileFurnace".
- Persistencia del contenido de "TileSpawner".
- Soporte para Double Chests.
- Sincronización en tiempo real entre múltiples jugadores viendo el mismo cofre.
- Validación de alcance para abrir cofres.
- Validación de alcance para ataques.
- Daño específico según el ítem utilizado.
- Knockback.
- Invulnerabilidad temporal después del respawn.
- Causas de daño por fuego, caída y ahogamiento.
- Respawn entre dimensiones y soporte para Nether.
