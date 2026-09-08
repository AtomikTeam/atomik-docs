# Atomik Changelog — 03

> Development changelog for Atomik.

**Date:** September 8, 2026  
**Status:** Released

---

## Overview

Esta versión corrige dos bugs reales en el inventario del jugador: uno
que permitía que un item recogido del suelo terminara en un slot de
armadura, y otro que duplicaba el paquete de confirmación de slot en
cada click de inventario.

## Fixed

### Inventario

- Corregido: `canAddItem`, `addItem`, `removeItem` y `firstEmpty` en
  `BaseInventory` usaban el tamaño interno crudo (40, incluye armadura)
  en vez del tamaño público (36, solo inventario principal). Esto
  permitía que un item recogido del suelo se colocara en un slot de
  armadura vacío (casco, pechera, pantalones o botas) cuando el
  inventario principal estaba lleno.
- Corregido: se enviaba un `ContainerSetSlotPacket` de confirmación
  duplicado en cada click de inventario (ramas principal, armadura,
  hotbar y creativo) — `PlayerInventory::onSlotChange()` ya lo manda
  automáticamente tras cada `setItem()`/`clear()`.
- Corregido: el mismo envío duplicado ocurría en `ItemFlintSteel::applyDurability()`
  al desgastar el pedernal y acero.

## Technical Notes

- El fix de armadura queda aislado a los métodos de "búsqueda de
  capacidad" (`canAddItem`/`addItem`/`removeItem`/`firstEmpty`);
  `setItem`/`clear` siguen usando el tamaño total a propósito, ya que
  necesitan direccionar la armadura por índice absoluto.
- Sin cambios de API pública ni de comportamiento visible para el
  cliente — el fix de duplicados solo elimina un paquete de red
  redundante por click, no cambia qué se confirma.
- Verificado compilando el proyecto completo (312/312 `.cpp`, 74/74
  `.c`, link exitoso), no solo revisando el código.

---

**AtomikTeam**  
