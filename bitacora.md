# BITACORA -- PROYECTO SOFTMOD R36 ULTRA

Log de Desarrollo - 27/02/2026

## PRESENTACION DEL PROYECTO (O ALMENOS UN INTENTO)
Este proyecto que tengo en mente es para experimentar, sacarle jugo a la consola R36Ultra (en especifico ya que es con la que cuento por el momento) y poder ayudar a la comunidad.
Por el momento tengo algunas ideas tales como: buscar la manera de pasar archivos por ftp o ssh, buscar una manera mas robusta de controlar los Leds RGB que vienen en los Analogos, poder implementar una ventana que nos muestre la temperatura del cpu, entre otras ideas que ire analizando y anotando con el tiempo.
he investigado en algunos foros, grupos de facebook y videos en Yt y tiktok a ver que dicen acerca de la consola pero muchos solo hablan de lo mismo, respaldar la micro sd y cambiarla, agregar juegos, o pura publicidad de la tiktok shop. 
No he encontrado mucho contenido sobre softmod en esta consola o nada tan interesante mas que cambiar el SO que por defecto la mayoria al ser clon cambian de EmuEelec a ArkOs par clones.
Por eso me he decidido a crear este proyecto y trastear con la consola esperando no brickearla en el camino haha.

## MI ENTORNO DE TRABAJO (por el momento)
**PC Dell OptiPlex 7040** 
- CPU Intel Core i5-6500 3.20Ghz
- 8 gb Ram (modelo y frecuencia por definir, no las recuerdo haha)
- HDD Toshiba 2TB  DT01ACA200
**Sistema Operativo**
- Elementary OS 8.1
 
## COMIENZA EL PROYECTO
### INICIAMOS EL CAMBIO DE SO

- Para comenzar en este proyecto me he decidido ir por el cambio de Sistema Operativo por el ArkOs para clones y probarlo unos dias a ver que tal funciona y que tan robusto esta y en base a mi criterio y necesidades ir haciendo modificaciones a nivel software.
 Se que no es hacer enchiladas asi que si alguien llega a ver esto y no he subido nada en un año, probablemente mi hiperfocus ya paso y encontre un nuevo sentido a mi vida botando este proyecto por la borda hahaha.
- Comence haciendo un respaldo de la sd la cual habia ya remplazado hace un par de semanas para evitar poroblemas con la sd normal. El respaldo lo hice desde la terminal utilizando el comando " sudo dd if=/dev/sdb of=~/r36Ultra-logs/backup_factory_MLS.img status=progress " (sin las comillas obviamente)
- Debo admitir que fue un proceso un poquito tardado pero en teoria se hizo un copia exacta bit a bit de lo que era mi SD actual, no era 100% necesario pero preferi hacerlo ya que no esta de mas.
- Descargue el ArkOS R3XS V2.0 (11072025) de AeolusUX.
- Flashee esa version de ArkOs en la sd con ayuda del comando
 \`\`\`bash 
# Comando usado paara el flash de micro sd:
sudo dd if='/home/ds118/Descargas/ArkOS_R35S-R36S_v2.0_11072025_MultiPanel.img' of=/dev/sdb bs=4M status=progress conv=fsync
 \`\`\`
 pero mi sorpresa fue que no funciono, honestamente no esperaba mucho ya que en el github de AeolusUx no se menciona que tenga compatibilidad con esta consola en espicifico pero igual no perdia mucho con intentarlo y para sorpresa de nadie la consola no encendio con la sd ya flasheada y con sus particiones correctas insertada dentro de la consola.
- Como ya todos los que han tenido esta consola saben, esta consola solo contiene una ranura para micro sd, pero investigando en teoria deberia de darle preferencia la consola a el SO que este instalado en la sd antes del que esta en la memoria interna.

### ¿PORQUE NO PRENDIO? 
- Se supone que en ArkOs puede llegar a haber problemas de compatibilidad con las consolas genericas o clones de la r36s original, un problema muy frecuente es el de incompatibilidad con el "Driver" de la Pantalla segun tengo entendido por lo que he investigado.
incluso ha habido reportes de gente que mensiona haber podido instalar ArkOs original en una consola generica pero con errores "cromaticos" en la pantalla de la consola o incluso con la relacion de aspecto.
- Una vez flasheada la micro Sd con el ArkOs de AeolusUx en la particion boot nos podemos encontrar unos archivos  tales como **rk3326-r35s-linux.dtb** el cual funciona como un "Traductor de Hardware" que le dice al Sistema Operativo que piezas tiene la consola y en que "idioma" (voltajes,pines,frecuencia,etc) hablarles.
Asi que si el archivo DTB tiene un mapa de componentes que tu consola no tiene o tiene en diferente pocision, modelos o pines, puede no reconocer directamente los componentes o no tener una respuesta de ellos y por ende la consola se "proteje" entrando en un bucle en el que no puede inciar el sistema, no mostrar imagen o simple y sencillamente no encender como fue mi caso.
decidi probar que booteara con los demas archivos DTB que vienen en la particion **BOOT** pero ninguno me funciono, asi que me he dicidido ir po otra alternativa como el ArkOs4clones de lcdyk0517.

### PROBANDO EL ARKOS4CLONE DE lcdyk0517
- Descargue la version mas reciente que hay hasta el momento en su github el cual es la version 20260109.
viene en 3 partes, es importante descargar las 3 partes y descomprimir la primera parte y solito tomara los archivos restantes en las otras partes para tener un archivo unico final. 

