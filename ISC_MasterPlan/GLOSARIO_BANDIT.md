======================================================================
       GLOSARIO TÉCNICO: MANUAL DE SOBREVIVENCIA (BANDIT 0-34)
======================================================================
Rol: Ingeniería de Sistemas / Ciberseguridad (ISC 2.0)
Uso: Referencia rápida para Terminal Linux y Wargames.
----------------------------------------------------------------------

1. MOVIMIENTO Y EXPLORACIÓN (Navegación de archivos)
----------------------------------------------------------------------
ls -la       : Lista TODO (archivos ocultos, permisos y tamaños).
cd [dir]     : Cambia de directorio (cd - regresa al anterior).
pwd          : Imprime tu ubicación actual (Print Working Directory).
file [f]     : Determina el tipo real de archivo (IGNORA la extensión).
du -b [f]    : Muestra el tamaño exacto en bytes de un archivo.
mkdir /tmp/X : Crea carpetas en el directorio temporal (para permisos).
cp / mv      : Copia / Mueve o renombra archivos.
ln -s [f] [l]: Crea un enlace simbólico (acceso directo).

2. LECTURA Y EXTRACCIÓN (Análisis de datos)
----------------------------------------------------------------------
cat [file]   : Muestra el contenido completo (solo para texto ASCII).
strings [f]  : Extrae texto legible de archivos binarios o corruptos.
head -n X    : Lee las primeras X líneas del archivo.
tail -n X    : Lee las últimas X líneas (útil para logs).
xxd [f]      : Genera un volcado hexadecimal.
xxd -r [f]   : "Reverse Hexdump" (Hexadecimal -> Binario real).

3. BÚSQUEDA AVANZADA (El comando FIND)
----------------------------------------------------------------------
Uso: find [ruta] [flags] 2>/dev/null
-user [nom]  : Archivos que pertenecen a este usuario.
-group [nom] : Archivos que pertenecen a este grupo.
-size [Xc]   : Tamaño exacto en caracteres/bytes (ej: 33c).
-readable    : Solo archivos que tú puedes leer.
-perm -4000  : Busca archivos con el bit SUID activo (privilegios).
2>/dev/null  : SILENCIA los errores de "Permiso denegado".

4. FILTRADO Y TUBERÍAS (Análisis de texto)
----------------------------------------------------------------------
grep "str"   : Busca una cadena específica en un texto o salida.
grep -v " "  : EXCLUYE las líneas que contienen el patrón.
sort         : Ordena las líneas alfabéticamente.
uniq -u      : Muestra ÚNICAMENTE las líneas que NO se repiten.
awk '{print}': Extrae columnas o filtra por largo (length($0) == 32).
cut -d' ' -f2: Corta por delimitador y extrae una columna específica.

5. CRIPTOGRAFÍA Y COMPRESIÓN
----------------------------------------------------------------------
base64 -d    : Decodifica datos en formato Base64.
tr 'A-Za-z' 'N-ZA-Mn-za-m' : Cifrado ROT13 (César).
openssl s_client -connect [h]:[p] : Conexión cifrada TLS/SSL.
gunzip [f]   : Descomprime .gz (requiere extensión correcta).
bzip2 -d [f] : Descomprime .bz2.
tar -xf [f]  : Extrae archivos empaquetados .tar.

6. REDES Y PUERTOS
----------------------------------------------------------------------
ssh -p 2220  : Acceso seguro al servidor de Bandit.
nc [h] [p]   : Netcat. Envía/Recibe datos crudos por un puerto.
nc -l -p [p] : Escucha en un puerto específico (Modo servidor).
nmap [host]  : Escanea puertos abiertos en una IP.
ss -tlpn     : Muestra puertos abiertos en TU máquina.
localhost    : IP 127.0.0.1. Se usa para servicios internos.

7. GIT PARA PENTESTING (Historial Forense)
----------------------------------------------------------------------
git clone [u]: Descarga el repositorio y su historia oculta.
git branch -a: Muestra todas las ramas (incluyendo remotas).
git log -p   : Muestra cambios detallados línea por línea (borrados).
git tag      : Lista etiquetas de versiones.
git show [t] : Muestra el contenido de un tag o commit específico.
git checkout : Salta a un commit o rama diferente.

8. GESTIÓN DE PERMISOS (chmod)
----------------------------------------------------------------------
Modo numérico (Suma): R=4, W=2, X=1
- 777 : Control total para todos (Inseguro).
- 644 : Dueño lee/escribe, resto solo lee.
- 755 : Dueño total, resto lee/ejecuta.
- 400 : Solo el dueño puede leer (Llaves SSH).
chmod u+s [f]: Activa bit SUID (el archivo corre con permisos del dueño).

----------------------------------------------------------------------
LÓGICAS DE ATAQUE / ESCAPE
----------------------------------------------------------------------
- ESCAPE DE SHELL: Escribir "$0" para invocar la shell original.
- BYPASS GIT: Usar "git add -f" para forzar archivos en .gitignore.
- BRUTEFORCE: "for i in {0000..9999}; do echo $i; done | nc localhost [p]"
- BUCLE LVL 12: file -> rename -> decompress -> REPETIR.
======================================================================
