# MANUAL PARA GENERAR LA CAPA DE FONDO EN OWGIS  A PARTIR DE VARIAS IMAGENES .PNG

## GEOREFERENCIAR UNA IMAGEN .PNG
#### Se tienen dos maneras para georeferenciar la imagen usando __gdal_translate__
1. Usando la bandera __-gcp__  
Lo que se hace es un mapeo de la posición del pixel a coordenadas _(x,y) -> (longitud,latitud)  
Por ejemplo:  
* _gdal_translate -gcp 0 0 -180 90 -a_srs EPSG:4326 imagen.png salida.tif_  
hace que el pixel (0,0) sea el latitud/longitud (-180 90)
2. Usando la bandera __-a_ullr__ 
