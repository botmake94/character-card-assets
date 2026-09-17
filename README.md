# character-card-assets

Imágenes públicas para **character cards `chara_card_v3`** (sistema *Secret Images*).
Servido por `raw.githubusercontent.com`; opcionalmente por el CDN de jsDelivr.

## Layout de carpetas

```
avatar/<personaje>.png              # miniatura de la card
<personaje>/greetings/<slug>.png    # first_mes y alternate_greetings
<personaje>/daily/<slug>.png        # acciones cotidianas
<personaje>/emotions/<slug>.png     # expresiones
<personaje>/clothing/<slug>.png     # estados de vestimenta
<personaje>/intimate/<slug>.png     # momentos íntimos (no sexuales)
<personaje>/sexual/<slug>.png       # solo cards adultas
```

Reglas de nombres: minúsculas, solo `[a-z0-9-]`, sin espacios ni acentos.
Un espacio sobrevive al push pero **rompe la URL raw**: siempre `shower-final.png`,
nunca `Shower Final.png`.

## URLs base

```
raw : https://raw.githubusercontent.com/botmake94/character-card-assets/main/<ruta>
cdn : https://cdn.jsdelivr.net/gh/botmake94/character-card-assets@main/<ruta>
```

Prefiere `raw` mientras iteras (cache de 5 minutos); `cdn` para galerías estables
(cache pública de 7 días, pero cachea por **ruta**: al reemplazar una imagen usa un
nombre nuevo, p. ej. `shower-02.png`).

## Añadir imágenes

```bash
python upload_images.py --src ./imagenes --repo . --subdir <personaje> \
    --manifest images.json --verify
```

El script sanitiza los nombres, copia, hace commit y push usando la credencial ya
guardada, y escribe `images.json` (que consume `build_card.py`). `--verify` debe
reportar `HTTP 200 | image/*` para cada URL antes de publicar la card.

Los commits van con el email noreply, así que no hay correo personal en el historial.
