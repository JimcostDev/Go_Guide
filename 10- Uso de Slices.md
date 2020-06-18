# Uso de Slices 

los array en GO funcionan como un conjunto de valores, no como un conjunto de referencias, es decir, al enviarlo a una función, esta hace una copia de los valores. Los slices funcionan como referencias, internamente GO utiliza slices por encima de arreglos y recomienda usarlos siempre que sea posible:

https://www.godesignpatterns.com/2014/05/arrays-vs-slices.html

