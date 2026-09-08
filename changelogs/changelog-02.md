# Changelog — AtomikPE

## Chunk Loader Real added

### Arreglado
- **`ChunkManager` nunca liberaba chunks de memoria.** Solo existía `flushDirty()` (guardaba a disco pero no liberaba RAM). Los chunks se acumulaban para siempre mientras el server corría.
  - Nuevo `ChunkManager::unloadChunk(x, z, save=true)` — saca el chunk del mapa, lo guarda a disco si está sucio (fuera del lock, para no bloquear otros `getChunk()` mientras escribe), y lo destruye.
  - Nuevo `ChunkManager::loadedChunkCoords()` — snapshot de qué hay cargado, para iterar sin retener el lock durante todo el barrido.
- **Fuga paralela en el registro de tile-entities.** Si se descargaba un chunk sin más, `Level::tiles_` seguía reteniendo los cofres/tiles de ese chunk para siempre.
  - Nuevo `Level::evictTilesForChunk(cx, cz)` — antes de tirar un chunk, vuelca cualquier tile-entity sucio de ese chunk (un cofre con cambios) a su NBT, y saca esos tiles del registro `tiles_`.
- Nuevo `Level::ChunkViewer` + `Level::unloadDistantChunks(viewers, margin=4)` — recorre los chunks cargados y descarga cualquiera que esté fuera del radio de visión de **todos** los jugadores conectados, con margen de histéresis para no cargar/descargar en bucle si alguien camina justo en el borde.
- `Server::tick()` ahora corre el barrido cada 100 ticks (~5s): arma la lista de "viewers" (posición de chunk + radio real de cada jugador) y llama a `unloadDistantChunks()`. Loguea cuánto se liberó.

### Encontrado en el camino
- `Player::viewDistance()` es en la práctica un **diámetro**, no un radio — `buildChunkSpiral(vd)` solo alcanza `vd/2` en cada eje (medido, no asumido). El sweep usa `viewDistance()/2` como radio real; con el valor crudo se hubieran descargado chunks que los jugadores todavía necesitaban.
