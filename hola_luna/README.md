### Conceptos
En este proyecto se usan los conceptos vistos en el proyecto hola_mundo, la **gravedad**, el **cuerpo**, la **densidad**, y la **fricción**, pero los valores de gravedad y fricción cambian. Ahora se hace una simulación de una caída libre en la luna, con una gravedad de 1.62 m/s^2 y una fricción de 0.
### Código
```
#include <iostream>  
#include <Box2d/Box2d.h>  
  
int main() {  
    // Creacion del mundo y de su gravedad  
    b2Vec2 gravity(0.0f, -1.62f);  
    b2World world(gravity);  
  
    // Caracteristicas del cuerpo  
    b2BodyDef groundBodyDef;  
    groundBodyDef.position.Set(0.0f, -10.0f);  
  
    // Crecion del cuerpo  
    b2Body* groundBody = world.CreateBody(&groundBodyDef);  
  
    // Creacion de la forma del cuerpo  
    b2PolygonShape groundBox;  
    groundBox.SetAsBox(50.0f, 1.0f);  
  
    groundBody ->CreateFixture(&groundBox, 0.0f);  
  
    b2BodyDef bodyDef;  
    bodyDef.type = b2_dynamicBody;  
    bodyDef.position.Set(0.0f, 20.0f);  
  
    b2Body* body = world.CreateBody(&bodyDef);  
  
    b2PolygonShape dynamicBox;  
    dynamicBox.SetAsBox(1.0f, 1.0f);  
  
    b2FixtureDef fixtureDef;  
    fixtureDef.shape = &dynamicBox;  
    fixtureDef.density = 1.0f;  
    fixtureDef.friction = 0.0f;  
  
    body ->CreateFixture(&fixtureDef);  
  
    float timeStep = 1.0f/60.0f;  
  
    int32 velocityIterations = 6;  
    int32 positionIteration = 2;  
  
    for (int32 i = 0; i <60; ++i)  
    {  
        world.Step(timeStep, velocityIterations, positionIteration);  
        b2Vec2 position = body->GetPosition();  
        float angle = body->GetAngle();  
        printf("%4.2f %4.2f %4.2f\n", position.x, position.y, angle);  
    }  
}
```
##### Explicación
Lo primero que se hace es la creación del mundo y se establece la gravedad, en este caso se toma de referencia a la luna y por eso la gravedad es de 1.62 m/s^2.
Después se establecen las características de un cuerpo físico y se le da una posición inicial en el mundo, dándole una posición inicial de 0 en *x* y -10 en *y*. Se crea el cuerpo con sus características en el mundo, se le da su forma y se establecen sus dimensiones, en este caso 50 metros de ancho y 1 metro de alto. Luego se establece que el tipo del cuerpo sea dinámico y se establece uno nueva posición con 0 en *x* y 20 en *y*. Se hace que el cuerpo dinámico tenga una anchura y altura de 1 metro y se le da una densidad de 1 kg/m^2 y fricción de 0 con el mundo. Para finalizar se crea un contador de tiempo y se hace una función para establecer como pasara ese tiempo y la acción que tomará el cuerpo durante ese tiempo, que será una caída libre durante 60 segundos.