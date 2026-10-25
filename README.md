# Mixamo Rig for Blender 5.x

Add-on de Blender que genera un **rig de control** (IK/FK, controles de pies, manos, columna y cabeza) a partir de un esqueleto **Mixamo** importado en FBX, y retargetea la animación de Mixamo a esos controles.

Esta versión (**1.2.0**) adapta el add-on a los cambios de la API de Python de **Blender 5.x**. La probé en **Blender 5.2.3 LTS**.

## Origen

- Basado en: [gitlab.com/x190/mixamo_blender4](https://gitlab.com/x190/mixamo_blender4) (port para Blender 4.x de Xin y TinkerBoi)
- Que a su vez se basa en: [Mixamo Add-on for Blender (Adobe)](https://www.adobe.com/products/substance3d/plugins/mixamo-in-blender.html)

## Descargas y compatibilidad

| Archivo | Versión de Blender | Estado |
|---|---|---|
| `mixamo_rig_blender5-1.2.0.zip` (esta versión) | 5.1 – 5.2 LTS | ✅ Probada en 5.2.3 LTS |
| | 4.0 – 5.0 | ⚠️ Mantiene compatibilidad en el código, pero no está probada |
| `mixamo_blender4` original (1.1.x) | 4.0 – 5.0 | ✅ Funciona |
| | 5.1 en adelante | ❌ Error `'Action' object has no attribute 'fcurves'` |
| Add-on oficial de Adobe | Anteriores a 4.0 | Descárgalo desde el enlace de Adobe |

Las dos versiones (1.2.0 y la original 1.1.x) están disponibles en la sección **Releases** de este repositorio.

## Instalación

1. Descarga el `.zip` que corresponda a tu versión de Blender. No lo descomprimas.
2. En Blender, ve a **Edit → Preferences → Get Extensions**. Si tienes instalada una versión anterior del add-on, desinstálala.
3. En el menú **▾** de la esquina superior derecha, elige **Install from Disk…** y selecciona el `.zip`.
4. El panel aparece en **Vista 3D → barra lateral (N) → pestaña Mixamo**.

## Uso básico

1. Importa el FBX de Mixamo (**File → Import → FBX**).
2. Selecciona el armature y, en la pestaña *Mixamo*, pulsa **Create Control Rig**. Activa *Apply Animation* para pasar la animación del FBX a los controles.
3. Para añadir más animaciones del mismo personaje, importa otro FBX, elígelo como *Source* y usa **Import Animation**.
4. En modo Pose, el panel *Mixamo Rig Settings* (pestaña *Tool*) incluye el cambio IK/FK con snap para un frame o para un rango de frames.

## Cambios en la versión 1.2.0

- **Acciones con slots (Blender 5.x):** Blender eliminó `action.fcurves`. El add-on ahora lee, crea y borra las F-Curves mediante los *channelbags* de la acción y sigue funcionando con la API antigua en 4.x. Este cambio corrige Create Control Rig, Zero Out, Import Animation y el bake interno.
- **Selección de huesos (Blender 5.x):** La selección en modo Pose ahora está en `PoseBone.select` y `Bone.select` ya no existe. Añadí funciones de selección que funcionan con ambas versiones. Afectaba al bake de controles y al snap IK/FK.
- **Slot de la acción:** el add-on siempre asigna un slot válido después de crear o importar una animación. Antes fallaba si la lista de slots disponibles venía vacía.
- **Diálogos de bake IK/FK:** ya no fallan si el rig no tiene animación; en ese caso usan el rango de frames de la escena.
- **Bake Animation (NLA):** si cambian los argumentos de `nla.bake`, el add-on reintenta con un conjunto reducido de opciones.
- **Ruta de `cs.blend`:** ahora usa `os.path.join` en lugar de `"\cs.blend"`, que solo funcionaba en Windows y genera un aviso en Python 3.13.

## Problemas conocidos

- Probé esta versión con un esqueleto que imita la estructura de Mixamo. Si encuentras un fallo con un FBX concreto, abre un *issue* con el error de la consola y, si puedes, el archivo.

## Créditos y licencia

Autores originales: Mixamo (Adobe), Xin y TinkerBoi. Adaptación a Blender 5.x: Ángel Pérez.

Licencia: **GPL-2.0-or-later**, la misma del proyecto original.
