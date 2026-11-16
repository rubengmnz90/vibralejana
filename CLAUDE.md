# Vibra Lejana (web estática)

Sitio de una sola página: `index.html` + `assets/`. Las fechas están en el arreglo de eventos dentro de `index.html` (cada una con `fecha`, `lugar`, `hora`, `tipo`, `detalle`, `flyer`). Los eventos pasados se mueven solos a "anteriores" por la fecha.

## Cómo agregar/cambiar fechas
1. Editar el arreglo de eventos en `index.html` (flyers en `assets/`, `flyer: null` si no hay).
2. Eventos privados: `lugar: "Evento privado"`, `tipo: "Show en eventos privados"`, `flyer: null`.
3. Commit en español (con la línea Co-Authored-By) y `git push` a `main` (GitHub rubengmnz90/vibralejana).

## Deploy (cuando el usuario lo pida)
- Servidor: `ssh charizard`, carpeta `/var/www/webs/vibralejana` (contenedor nginx `vibra-lejana`).
- El usuario normalmente corre `nodob && nodou` (alias en `~/configurations/scripts/`: `nodo_build.sh` = git pull + `docker compose build`; `nodo_up.sh` = `compose down` + `up -d`). No modificar esos scripts ni el servidor más allá de esto.
- Los alias solo existen en shell interactivo: `ssh charizard 'bash -ic "nodou"'`.
- Problema conocido: `.git` del servidor es de www-data/root, así que `git pull` como `ubuntu` falla (`FETCH_HEAD: Permission denied`) y `nodob` se corta. Solución usada: 
  `ssh charizard 'cd /var/www/webs/vibralejana && sudo git pull && sudo docker compose build && bash -ic "nodou"'`
- Verificar: `curl -s https://www.vibralejana.com | grep <fecha>` y `git log -1` en el servidor.
