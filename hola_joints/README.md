## Conceptos
###### b2DistanceJointDef
Esta clase nos permite crear una articulación de distancia. La joint de distancia nos permite conectar dos cuerpo de manera que mantengan siempre la misma distancia entre ellos.
###### b2RevoluteJointDef
Esta clase nos permite crear una articulación  de revolución. La joint de revolución nos da la opción de anclar un cuerpo dinámico a uno estático y rotar en su eje.
###### b2PrismaticJointDef
Esta clase nos permite crear una articulación  prismática. 
###### b2GearJointDef
Esta clase nos permite crear una articulación  de engranaje.
###### b2WeldJointDef
Esta clase nos permite crear una articulación  de soldadura.
###### b2WheelJointDef
Esta clase nos permite crear una articulación  de rueda.

## Código
```
#include <iostream>  
#include <Box2d/Box2d.h>  
#include <SFML/Graphics.hpp>  
  
constexpr float SCALE = 30.0f;  
  
class Cube {  
public:  
    Cube(b2World &world, float x, float y, int state) {  
        b2BodyDef bodydef;  
        bodydef.position.Set(x / SCALE, y / SCALE);  
        switch (state) {  
            case 0:  
                bodydef.type = b2_staticBody;  
                break;  
            case 1:  
                bodydef.type = b2_dynamicBody;  
                break;  
            case 2:  
                bodydef.type = b2_kinematicBody;  
        }  
        body = world.CreateBody(&bodydef);  
  
        b2PolygonShape shape;  
        shape.SetAsBox((10.f / 2) / SCALE, (10.f / 2) / SCALE);  
  
        b2FixtureDef fixturedef;  
        fixturedef.shape = &shape;  
        fixturedef.density = 1.0f;  
        body->CreateFixture(&fixturedef);  
  
        box.setSize(sf::Vector2f(10.f, 10.f));  
        box.setFillColor(sf::Color::Red);  
        box.setOrigin(5.f, 5.f);  
    }  
  
    void update() {  
        box.setPosition(SCALE * body->GetPosition().x, SCALE * body->GetPosition().y);  
        box.setRotation(body->GetAngle() * 180 / b2_pi);  
    }  
  
    void draw(sf::RenderWindow &win) const {  
        win.draw(box);  
    }  
  
    void resetPosition() {  
        body->SetTransform(b2Vec2(0, 0), body->GetAngle());  
    }  
  
    void stop() {  
        body->SetLinearVelocity(b2Vec2(0, 0));  
    }  
  
    b2Body *getBody() {  
        return body;  
    }  
  
private:  
    sf::RectangleShape box;  
    b2Body *body;  
};  
  
int main() {  
    sf::RenderWindow window(sf::VideoMode(1000, 900), "SFML works!");  
  
    b2Vec2 gravity(0.0f, 0.0f);  
    b2World world(gravity);  
  
    // Objetos de la clase Cube  
    Cube cube(world, 400, 200, 1);  
    Cube cube2(world, 550, 200, 1);  
    Cube cube3(world, 850, 200, 1);  
    Cube cube4(world, 700, 200, 0);  
    Cube cube5(world, 300, 400, 1);  
    Cube cube6(world, 300, 500, 1);  
    Cube cube7(world, 700, 400, 0);  
    Cube cube8(world, 850, 500, 1);  
  
    // Articulacion de Distancia  
    b2DistanceJointDef jointDefDistance;  
    jointDefDistance.Initialize(cube.getBody(), cube2.getBody(), cube.getBody()->GetWorldCenter(), cube2.getBody()->GetWorldCenter());  
    float frequencyHz = 30.0f;  
    float dampingRatio = 0.1f;  
    b2LinearStiffness(jointDefDistance.stiffness, jointDefDistance.damping, frequencyHz, dampingRatio, jointDefDistance.bodyA, jointDefDistance.bodyB);  
    world.CreateJoint(&jointDefDistance);  
  
    // Articulacion de Rotacion  
    b2RevoluteJointDef jointDefRevolute;  
    jointDefRevolute.Initialize(cube3.getBody(), cube4.getBody(), cube4.getBody()->GetWorldCenter());  
    jointDefRevolute.enableMotor = true;  
    jointDefRevolute.maxMotorTorque = 1.0f;  
    jointDefRevolute.motorSpeed = 0.1f;  
    world.CreateJoint(&jointDefRevolute);  
  
    // Articulacion Prismatica  
    b2PrismaticJointDef jointDefPrismatic;  
    jointDefPrismatic.Initialize(cube.getBody(), cube4.getBody(), cube.getBody()->GetWorldCenter(), b2Vec2(1.0f, 0.0f));  
    jointDefPrismatic.lowerTranslation = -10.0f;  
    jointDefPrismatic.upperTranslation = 10.0f;  
    jointDefPrismatic.enableLimit = true;  
    world.CreateJoint(&jointDefPrismatic);  
  
    // Articulacion de Engrane  
    b2GearJointDef jointDefGear;  
  
    // Articulacion de Soldadura  
    b2WeldJointDef jointDefWeld;  
    jointDefWeld.Initialize(cube5.getBody(),cube6.getBody(),cube5.getBody()->GetWorldCenter());  
    jointDefWeld.stiffness = 20.0f;  
  
    world.CreateJoint(&jointDefWeld);  
  
    // Articulacion de Rueda  
    b2WheelJointDef jointDefWheel;  
    jointDefWheel.Initialize(cube7.getBody(),cube8.getBody(),cube7.getBody()->GetWorldCenter(),b2Vec2(1.0f, 0.0f));  
    jointDefWheel.enableMotor = true;  
    jointDefWheel.maxMotorTorque = 1.0f;  
    jointDefWheel.motorSpeed = 0.1f;  
    world.CreateJoint(&jointDefWheel);  
  
    while (window.isOpen()) {  
        sf::Event event;  
        while (window.pollEvent(event)) {  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::D)) {  
                cube.getBody()->ApplyForceToCenter(b2Vec2(0.1f, 0.0f), true);  
                cube5.getBody()->ApplyForceToCenter(b2Vec2(0.1f, 0.0f), true);  
            }  
  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::A)) {  
                cube.getBody()->ApplyForceToCenter(b2Vec2(-0.1f, 0.0f), true);  
                cube5.getBody()->ApplyForceToCenter(b2Vec2(-0.1f, 0.0f), true);  
            }  
  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::W)) {  
                cube.getBody()->ApplyForceToCenter(b2Vec2(0.0f, -0.1f), true);  
                cube5.getBody()->ApplyForceToCenter(b2Vec2(0.0f, -0.1f), true);  
            }  
  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::S)) {  
                cube.getBody()->ApplyForceToCenter(b2Vec2(0.0f, 0.1f), true);  
                cube5.getBody()->ApplyForceToCenter(b2Vec2(0.0f, 0.1f), true);  
            }  
  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::Space)) {  
                cube.resetPosition();  
                cube5.resetPosition();  
            }  
  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::R)) {  
                cube.stop();  
                cube5.stop();  
            }  
  
            // The Z key event to close the window  
            if (sf::Keyboard::isKeyPressed(sf::Keyboard::Z)) {  
                window.close();  
                return 0; // return from the main function, effectively ending the program  
            }  
        }  
  
        world.Step(1 / 60.f, 8, 3);  
        cube.update();  
        cube2.update();  
        cube3.update();  
        cube4.update();  
        cube5.update();  
        cube6.update();  
        cube7.update();  
        cube8.update();  
  
        window.clear();  
        cube.draw(window);  
        cube2.draw(window);  
        cube3.draw(window);  
        cube4.draw(window);  
        cube5.draw(window);  
        cube6.draw(window);  
        cube7.draw(window);  
        cube8.draw(window);  
        window.display();  
    }  
    return 0;  
}
```
Este código tiene lo mismo que se vio en la prueba de sfml, con la clase Cube, el movimiento para el cubo, y la librería SFML para imprimir en grafico/pantalla los cubos. Solo que se le agregan 7 cubos mas y 6 joints; DistanceJoint, RevoluteJoint, PrismaticJoint, GearJoint, WeldJoint y WheelJoint.
En el joint de distancia se usan dos cubos dinámicos, declarando que el cubo 2 esta anclado al cubo uno haciendo que se mantenga a la misma distancia en todo momento, siguendo al cubo 1. Sin embargo esto no evita que el cubo 2 rote sobre el cubo 1.
El joint de revolución usa el cubo 3, estático, y el cubo 4, dinámico. Ancla el cubo 4 al cubo 3 pero le agrega un motor, velocidad de motor y torque para mantenerse cerca del cubo 3, haciendo que el cubo 4 rote alrededor de cubo 3 indefinidamente.
El joint prismático hace que el cubo 1 solo pueda moverse en el eje x y con un limite de 10 a cada lado.
El joint de engranaje solo esta declarado, pero no esta inicializado ni tiene ninguna función. Esto debido a su complejo funcionamiento, del que desconozco.
El joint de soldadura esta declarado e inicializado, pero no encontré como hacerlo funcionar, no logre averiguar para que sirven sus atributos y solo hace que el cubo 6 este anclado al cubo 5 y lo siga a donde se mueva, manteniendo la misma distancia entre ellos.
El joint de rueda usa a los cubos 7 y 8, anclando al cubo 8 al 7, haciendo que, con un motor, velocidad y torque, el cubo 8 ruede sobre su eje y se mueva en el eje y con cierto limite.