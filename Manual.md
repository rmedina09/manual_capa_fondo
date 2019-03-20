# MANUAL PARA GENERAR LA CAPA DE FONDO EN OWGIS  A PARTIR DE VARIAS IMAGENES .PNG

## GEOREFERENCIAR UNA IMAGEN .PNG
#### Se tienen dos maneras para georeferenciar la imagen usando __gdal_translate__
1. Usando la bandera __-gcp__  
Lo que se hace es un mapeo de la posición del pixel a coordenadas _(x,y) -> (longitud,latitud)_

   Por ejemplo con una imagen de 5400 * 2400 :  
   __gdal_translate -gcp 0 0 -180 90 -gcp 5400 0 180 90 -gcp 0 2700 -180 -90 -gcp 5400 2700 180 -90 -a_srs EPSG:4326 imagen.png salida.tif__  
   * el pixel (0, 0)       sera en latitud/longitud el punto(-180, 90)
   * el pixel (5400, 0)    sera en latitud/longitud el punto(180, 90)
   * el pixel (0, 2700)    sera en latitud/longitud el punto(-180, -90)
   * el pixel (5400, 2700) sera en latitud/longitud el punto(180, -90)
2. Usando la bandera __-a_ullr__  
   Esta bandera unicamente necesita los puntos de la esquina superior izquierda y la esquina inferior derecha, y se utiliza de    la siguiente manera en una imagen de 5400 * 2400 (_gdal_translate -a_srs tipo_proyeccion -a_ullr ulx uly lrx lry imagen.jpg out.tif_):
   
   __gdal_translate -a_srs EPSG:4326 -a_ullr -180 90 180 -90 imagen.jpg out3.tif__
   
   en donde el mapeo de la esquina superior izquierda (ulx, uly) = (0, 0) se hace a la coordenada (-180, 90) y de la esquina      inferior derecha (lrx, lry) = (5400, 2400) se hace a la coordenada (180,-90).  
   * ulx = upper left x , uly = upper left y
   * lrx = lower right x, lry = lower right y
-------------------------------
## UNIR VARIOS ARCHIVOS .tif

Por medio de la utilidad __gdal_merge.py__ que crea un mosaico de manera automatica a partir de un conjunto de imagenes (.tif), las cuales deben tener el mismo sistema de coordenadas. Se mezclan o unen el conjunto de imagenes que queremos manjear como una sola de la siguiente manera:

   __gdal_merge.py -o out_merge.tif file_1.tif file_2.tif . . . file_n.tif__

--------------------------------
## GENERAR PIRAMIDE DE MOSAICOS

Para generar la piramide de mosaicos lo haremos por medio de la utilidad __gdal_retile.py__ , por ejemplo :

__gdal_retile.py -v -r bilinear -levels 4 -ps 2048 2048 -co "TILED=YES" -co "COMPRESS=JPEG" -targetDir *directorio* *input.tif*__
