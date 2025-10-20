# Recuperación de archivo borrado con Git

## Contexto
Repositorio: `proyecto-pruebas` 
Rama principal: `master`
Archivo afectado: `errores.sh`

## Error simulado
Después de **subir a GitHub** el archivo `errores.sh` (commit `feat: añade errores.sh
 para simulación de errores`), lo **borré por accidente** y subí ese borrado con:
```bash
rm errores.sh
git add .
git commit -m "chore: elimina errores.sh por accidente"
git push -u origin master
```
## Enseñanza
Aprendí que es posible recuperar archivos borrados incluso ya hecho un commit. 

## Recuperación del archivo

Para recuperar el archivo, primero utilicé `git reflog` para localizar el commit anterior al borrado:

```bash
git reflog
```

Identifiqué el commit donde el archivo todavía existía (hash 5645dca en mi caso).
Después recuperé solo ese archivo usando:

```bash
git checkout 5645dca -- errores.sh  # Usar el hash correspondiente al commit donde existía el archivo, en este caso 5645dca
```

Verifiqué que el archivo había vuelto:

```bash
ls -l
cat errores.sh
```

Finalmente, lo añadí de nuevo al historial:

```bash
git add errores.sh
git commit -m "fix: recupera errores.sh tras eliminación accidental"
git push
```

## Herramientas comparadas

**git reflog** → Útil para encontrar el punto exacto antes del error.
**git checkout <hash> -- archivo** → Recupera un archivo específico sin alterar el resto del proyecto.
**git reset** → Podría regresar todo el proyecto a un commit previo, pero no lo usé porque habría afectado otros cambios.

## Conclusión / Aprendizaje

Aprendí que incluso si un archivo se elimina y se sube al remoto por error, Git conserva todo el historial.
Gracias a `reflog` y `checkout` es posible restaurar versiones anteriores sin perder el trabajo.
También comprendí que es fundamental hacer git push antes del error para simular un caso real de recuperación en entornos DevOps.


---





