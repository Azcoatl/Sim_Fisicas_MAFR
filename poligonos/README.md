## Conceptos
##### b2PolygonShape
Es la clase que se uso en el código para la creación de los polígonos.
##### b2Vec2
Es la clase que se uso para establecer los vectores con sus coordenadas de los polígonos.
## Código
```
#include <iostream>  
#include <Box2d/Box2d.h>  
  
int main() {  
  
    // Creacion de Triangulo Rectangulo  
     // Se establece una variable de 3 vectores para el triangulo rectangulo y se le da un posicion a cada vector    b2Vec2 rightTriangleV [3];  
    rightTriangleV [0]. Set(0.0f, 0.0f);  
    rightTriangleV [1]. Set(1.0f, 0.0f);  
    rightTriangleV [2]. Set(0.0f, 1.0f);  
     // Se establece el poligono para el triangulo rectangulo  
    b2PolygonShape rightTriangle;  
    rightTriangle.Set(rightTriangleV , 3);  
  
    // Creacion de Cuadrado  
     // Se establece una variable de 4 vectores para el cuadrado y se le da un posicion a cada vector    b2Vec2 squareV [4];  
    squareV [0]. Set(0.0f, 0.0f);  
    squareV [1]. Set(1.0f, 0.0f);  
    squareV [2]. Set(1.0f, 1.0f);  
    squareV [3]. Set(0.0f, 1.0f);  
     // Se establece el poligono para el cuadrado  
    b2PolygonShape square;  
    square.Set(squareV , 4);  
  
    // Creacion de Pentagono  
     // Se establece una variable de 5 vectores para el pentagono y se le da un posicion a cada vector    b2Vec2 pentagonV [5];  
    pentagonV [0]. Set(0.0f, 0.0f);  
    pentagonV [1]. Set(-0.2f, 0.7f);  
    pentagonV [2]. Set(0.5f, 1.3f);  
    pentagonV [3]. Set(1.2f, 0.7f);  
    pentagonV [4]. Set(1.0f, 0.0f);  
     // Se establece el poligono para el pentagono  
    b2PolygonShape pentagon;  
    pentagon.Set(pentagonV , 5);  
  
    // Creacion de Hexagono  
     // Se establece una variable de 6 vectores para el hexagono y se le da un posicion a cada vector    b2Vec2 hexagonV [6];  
    hexagonV [0]. Set(0.0f, 0.0f);  
    hexagonV [1]. Set(-0.5f, 0.9f);  
    hexagonV [2]. Set(0.0f, 1.7f);  
    hexagonV [3]. Set(1.0f, 1.7f);  
    hexagonV [4]. Set(1.5f, 0.9f);  
    hexagonV [5]. Set(1.0f, 0.0f);  
     // Se establece el poligono para el hexagono  
    b2PolygonShape hexagon;  
    hexagon.Set(hexagonV , 6);  
  
    // Creacion de Octagono  
     // Se establece una variable de 8 vectores para el octagono y se le da un posicion a cada vector    b2Vec2 octagonV [8];  
    octagonV [0]. Set(0.0f, 0.0f);  
    octagonV [1]. Set(-0.7f, 0.7f);  
    octagonV [2]. Set(-0.7f, 1.7f);  
    octagonV [3]. Set(0.0f, 2.4f);  
    octagonV [4]. Set(1.0f, 2.4f);  
    octagonV [5]. Set(1.7f, 1.7f);  
    octagonV [6]. Set(1.7f, 0.7f);  
    octagonV [7]. Set(1.0f, 0.0f);  
     // Se establece el poligono para el octagono  
    b2PolygonShape octagon;  
    octagon.Set(octagonV , 8);  
  
    return 0;  
}
```

### Explicación
El código lo que hace es crear cinco figuras; un triangulo rectángulo, un cuadrado, un pentágono, un hexágono y un octágono. Para esto se usa la clase b2PolygonShape (para establecer polígonos) y b2Vec2 (para establecer vectores). Primero se usa el b2Vec2 para establecer el número de vectores que se usaran y sus coordenadas en *x* y en *y* para darle forma a los polígonos. Después se crea, con la clase b2PolygonShape, el polígono. Y por último se setean con ".Set" los puntos/vectores en el polígono y cuantos son en total. Y se hacen los mismos pasos para cada polígono que se forma.