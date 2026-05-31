# Security Policy

## Versiones soportadas

Negativo Lab es una aplicación de un único archivo HTML que se ejecuta
enteramente en el navegador, sin servidor ni dependencias externas. Solo
se da soporte de seguridad a la última versión publicada.

| Versión | Soportada          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reportar una vulnerabilidad

Si encuentras un problema de seguridad, por favor **no abras un issue
público**. Repórtalo de forma privada por una de estas vías:

- Usando "Report a vulnerability" en la pestaña Security del repositorio
  (requiere tener activado Private vulnerability reporting).

Procuraré responder en un plazo de 7 días. Si el reporte se acepta,
publicaré un parche y un aviso (security advisory); si se descarta, te
explicaré el motivo.

## Alcance

Toda la imagen se procesa en local y nunca se sube a ningún servidor.
Los vectores relevantes son básicamente: procesado de archivos de imagen
no confiables (corrupción de memoria del navegador, cuelgues) y la carga
opcional de fuentes desde Google Fonts. No hay backend, autenticación ni
almacenamiento de datos del usuario.
