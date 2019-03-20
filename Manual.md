# MANUAL PARA GENERAR LA CAPA DE FONDO EN OWGIS  A PARTIR DE VARIAS IMAGENES .PNG

## GEOREFERENCIAR UNA IMAGEN .PNG
#### Se tienen dos maneras para georeferenciar la imagen usando __gdal_translate__
1. Usando la bandera __-gcp__  
Lo que se hace es un mapeo de la posición del pixel a coordenadas _(x,y) -> (longitud,latitud) 

Por ejemplo con una imagen de 5400 * 2400 :  
__gdal_translate -gcp 0 0 -180 90 -gcp 5400 0 180 90 -gcp 0 2700 -180 -90 -gcp 5400 2700 180 -90 -a_srs EPSG:4326 imagen.png salida.tif__  
 * el pixel (0,0) sera en latitud/longitud el punto(-180 90)
 * el pixel (0,0) sera en latitud/longitud el punto(-180 90)
 * el pixel (0,0) sera en latitud/longitud el punto(-180 90)
 * el pixel (0,0) sera en latitud/longitud el punto(-180 90)
2. Usando la bandera __-a_ullr__ 
