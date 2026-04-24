# LABORATORIO 4: Diseño y construcción de una incubadora neonatal a escala
## INTRODUCCIÓN
En el contexto de la ingeniería biomédica, el desarrollo de dispositivos que permitan garantizar condiciones adecuadas para la vida humana es una de las aplicaciones más relevantes. Entre estos dispositivos, las incubadoras neonatales cumplen un papel fundamental en la atención de recién nacidos que requieren cuidados especiales, ya que permiten mantener un entorno controlado que favorece su estabilidad y recuperación.

La presente práctica de laboratorio se enfoca en el diseño y construcción de una incubadora neonatal a escala, con el objetivo de integrar conocimientos de electrónica e instrumentación y biosensores. A través de este proyecto, se busca comprender el funcionamiento general de estos equipos e implementar soluciones tecnológicas que permitan regular variables críticas dentro de un sistema real.

Además, esta práctica permite analizar la importancia del monitoreo continuo y del control automático en dispositivos biomédicos, evidenciando cómo pequeñas variaciones en parámetros como la temperatura pueden tener un impacto significativo en el bienestar del paciente. De igual forma, se promueve el desarrollo de habilidades prácticas en diseño, simulación, construcción y validación de sistemas.

## FUNDAMENTOS TEÓRICOS

Lass incubadoras neonatales son dispositivos biomédicos diseñados para proporcionar un entorno controlado que garantice condiciones óptimas para el desarrollo de recién nacidos, especialmente prematuros. Su funcionamiento se basa en la regulación de variables fisiológicas y ambientales como la temperatura, la humedad, el flujo de aire y, en algunos casos, la concentración de oxígeno.

Desde el punto de vista físico, el principio de operación de una incubadora se fundamenta en la transferencia de calor por convección. El sistema utiliza un ventilador que hace circular el aire a través de un elemento calefactor, elevando su temperatura antes de introducirlo en el compartimiento del bebé, permitiendo así mantener una temperatura interna estable, típicamente en un rango cercano a los 36 °C – 37,5 °C, que es adecuado para la termorregulación del neonato.

En cuanto a su estructura, una incubadora neonatal está compuesta por varios subsistemas claramente definidos, como se observa en la imagen de referencia. El compartimiento del bebé corresponde a la cámara cerrada donde se mantiene el recién nacido, diseñada para minimizar pérdidas térmicas y permitir la observación constante. El módulo de control constituye el sistema central de operación, donde se visualizan y ajustan variables como la temperatura del aire y la temperatura de la piel.

El sistema también incluye una base estructural y gabinete móvil, que proporcionan soporte y facilitan el desplazamiento del equipo mediante ruedas con freno. Adicionalmente, elementos como la repisa y el atril permiten la integración de equipos auxiliares o documentación clínica.

Un componente clave dentro del funcionamiento es el sistema de sensores, encargado de medir variables en tiempo real, entre las cuales destaca el sensor de temperatura de aire, que monitorea el ambiente interno, y el sensor de temperatura de piel, que permite una medición más directa del estado térmico del neonato. Estos sensores envían señales al sistema de control, donde son procesadas para tomar decisiones automáticas.

El módulo de control, tal como se muestra en la imagen, integra diferentes indicadores y actuadores: displays para visualizar la temperatura, botones para ajustar los valores deseados, indicadores de potencia del sistema de calefacción y sistemas de alarma, encargadas de avisar cuando las variables se encuentran fuera de los rangos seguros, permitiendo una intervención oportuna.

<img width="320" height="360" alt="image" src="https://github.com/user-attachments/assets/382d679f-5c01-4469-b8de-b81a2d7200f4" />

## DESAROLLO DE LA PRÁCTICA
### 1. Diseño del circuito de medición de peso

El sistema de medición de peso implementado en la incubadora neonatal a escala se basa en el uso de una galga extensiométrica de 5 kg junto con el módulo HX711, el cual permite amplificar y digitalizar la señal proveniente del sensor. Este tipo de configuración es ampliamente utilizado en balanzas electrónicas debido a su alta sensibilidad y precisión.

La galga extensiométrica funciona a partir del principio de deformación mecánica: cuando se aplica una carga sobre ella, su estructura interna se deforma ligeramente, generando un cambio en su resistencia eléctrica. Este cambio es muy pequeño, por lo que no puede ser leído directamente por un microcontrolador, por tal razón, se emplea el módulo HX711, que incorpora un amplificador de instrumentación y un convertidor analógico-digital de alta resolución, permitiendo obtener una señal digital proporcional al valor de la carga aplicada.

El módulo HX711 se encarga de acondicionar la señal proveniente de la galga, incrementando su amplitud y reduciendo el ruido, para luego convertirla en datos digitales que pueden ser procesados por el microcontrolador, y así a partir de estos datos, y mediante un factor de calibración previamente determinado, el sistema convierte la lectura en una unidad de peso, como lo es el gramo.

En esta implementación se utilizó una única celda de carga, lo que simplifica el diseño del sistema y reduce la cantidad de componentes requeridos. Sin embargo, esta configuración implica que la medición puede verse afectada si la carga no se aplica de manera uniforme sobre la superficie de la galga, y esta no se encuentra lo suficientemente estable a la hora de aplicar el peso correspondiente.

Adicionalmente, el sistema incorpora un pulsador para la función de tara, el cual permite establecer un punto de referencia inicial, el cual es fundamental para eliminar el peso de la estructura o base sobre la que se encuentra la galga, garantizando que la medición corresponda únicamente al objeto de interés. Al activarse, el sistema ajusta las lecturas posteriores con respecto a este valor de referencia.

Por último, la información suministrada es visualizada mediante una pantalla OLED, donde se muestra el peso en tiempo real de forma clara y continua, permitiendo al usuario monitorear fácilmente las mediciones obtenidas.

### 2. Diseño del circuito de control de temperatura

El sistema de control de temperatura de la incubadora neonatal a escala fue diseñado con el objetivo de mantener un ambiente térmico estable dentro del rango requerido para el cuidado del neonato. Para ello, se implementó un sistema basado en un termistor NTC, un elemento calefactor (bombillo), un ventilador y dos módulos relé que permiten la activación de los actuadores.

El termistor NTC es el sensor encargado de medir la temperatura interna, su funcionamiento se basa en la variación de su resistencia eléctrica en función de la temperatura: a medida que la temperatura aumenta, su resistencia disminuye. Esta variación se convierte en una señal de voltaje mediante un divisor resistivo, permitiendo que el microcontrolador adquiera y procese la información.

Con base en la lectura del sensor, el sistema determina el estado térmico de la incubadora y actúa en consecuencia mediante un control tipo ON/OFF. El bombillo actúa como elemento calefactor, activándose cuando la temperatura se encuentra por debajo del rango establecido. Por su parte, el ventilador, controlado mediante un segundo relé, permite la circulación del aire y contribuye a disipar el calor cuando la temperatura es elevada.

Adicionalmente, el sistema incorpora un conjunto de dos LEDs indicadores, los cuales permiten identificar de manera visual el estado de la temperatura:

- El LED verde indica que la temperatura se encuentra dentro del rango adecuado.
- El LED rojo se activa cuando la temperatura se encuentra fuera del rango.

Este sistema de señalización facilita una interpretación rápida del estado térmico sin necesidad de observar continuamente los valores numéricos.

Por otra parte, la temperatura medida es visualizada en tiempo real mediante una pantalla OLED, donde se muestra el valor actual de manera clara y continua, mejorando la interacción con el sistema, permitiendo un monitoreo preciso del comportamiento térmico dentro de la incubadora.

En conjunto, este sistema representa una implementación de control en lazo cerrado, en la cual la medición constante de la temperatura permite accionar automáticamente los elementos de calefacción y ventilación, garantizando condiciones estables y seguras para el entorno simulado del neonato.

### 3. Modelo de incubadora neonatal a escala

La estructura externa de la incubadora neonatal a escala fue diseñada con el propósito de proporcionar un entorno térmicamente aislado, funcional y de fácil acceso para la manipulación del sistema interno. Para su construcción se utilizó icopor como material principal, complementado con una superficie plástica transparente en la parte visible.

El uso de icopor presenta varias ventajas importantes en este tipo de aplicaciones. En primer lugar, es un material con excelentes propiedades de aislamiento térmico, lo que permite reducir la pérdida de calor hacia el exterior y mejorar la eficiencia del sistema de calefacción. Además, es liviano, económico y fácil de trabajar, lo que facilita su corte, ensamblaje y adaptación a las dimensiones requeridas del prototipo.

Por otro lado, la incorporación de un plástico transparente en la parte superior y los laterales de la incubadora permite la visualización del interior sin necesidad de abrir la estructura, fundamental para el monitoreo del estado del sistema.

En cuanto al acceso, se diseñaron dos orificios circulares en la parte frontal, los cuales permiten la manipulación del interior de la incubadora, simulando los accesos presentes en equipos reales, los cuales facilitan la interacción con el neonato o los sensores sin comprometer significativamente las condiciones internas del sistema. Adicionalmente, la incubadora cuenta con un mecanismo de apertura lateral, lo que permite acceder completamente al interior cuando se requiere realizar ajustes, mantenimiento o instalación de los componentes electrónicos.

Las dimensiones del prototipo fueron de aproximadamente 40 cm × 20 cm × 22 cm, lo que permite un tamaño compacto adecuado para la implementación a escala, manteniendo al mismo tiempo el espacio suficiente para integrar todos los subsistemas desarrollados control de temperatura, medición de peso y su posterior visualización.

Es importante destacar que la base de la incubadora también fue construida en icopor, lo cual inicialmente facilitó la fabricación; sin embargo, durante las pruebas se evidenció que este material no soporta adecuadamente cargas mayores, presentando deformaciones que afectan la estabilidad del sistema de medición de peso. Por esta razón, se concluye que, para mejorar el desempeño estructural del prototipo, la base debería fabricarse con un material más rígido, como madera, acrílico o algún polímero de mayor resistencia, que garantice una mejor distribución de la carga y mayor precisión en las mediciones.

## IMPLEMENTACIÓN DEL SISTEMA

### Programación del sistema de medición de peso

```bash
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include "HX711.h"

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

#define DOUT  4
#define CLK   5
HX711 scale;

#define BOTON_TARA 14


float calibration_factor = -300;

bool yaTarado = false;
float peso_filtrado = 0;

void setup() {
  Serial.begin(115200);
  Wire.begin(21, 22);

  if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println("Error OLED");
    while(true);
  }

  display.clearDisplay();
  display.setTextColor(WHITE);

  display.setTextSize(1);
  display.setCursor(0, 20);
  display.println("Iniciando...");
  display.display();
  delay(2000);

  scale.begin(DOUT, CLK);
  scale.set_scale();
  scale.tare();

  pinMode(BOTON_TARA, INPUT_PULLUP);
}

void loop() {

  if (digitalRead(BOTON_TARA) == LOW && !yaTarado) {
    delay(200);
    scale.tare(15);
    peso_filtrado = 0;
    yaTarado = true;

    display.clearDisplay();
    display.setTextSize(1);
    display.setCursor(0, 25);
    display.println("TARA aplicada");
    display.display();

    delay(500);
  }

  if (digitalRead(BOTON_TARA) == HIGH) {
    yaTarado = false;
  }

  scale.set_scale(calibration_factor);

  float peso = scale.get_units(10);


  peso_filtrado = 0.7 * peso_filtrado + 0.3 * peso;


  if (abs(peso_filtrado) < 2) peso_filtrado = 0;

  Serial.print("Peso: ");
  Serial.println(peso_filtrado);

  display.clearDisplay();

  display.setTextSize(1);
  display.setCursor(0, 0);
  display.println("Balanza incubadora");

  display.setCursor(0, 15);
  display.print("Peso:");

  display.setTextSize(2);
  display.setCursor(0, 30);
  display.print(peso_filtrado, 1);
  display.print(" g");

  display.display();

  delay(150);
}
```
El sistema de medición de peso fue implementado mediante una ESP32, integrando el módulo HX711, una pantalla OLED y un pulsador para la función de tara. En el programa se inicializan las librerías necesarias para la comunicación I2C con la pantalla y para la adquisición de datos del sensor de peso. Durante la etapa de configuración (setup), se establece la comunicación serial, se inicializa la pantalla OLED mostrando un mensaje de inicio, y se configura el módulo HX711 realizando una tara inicial que permite establecer un punto de referencia sin carga. Además, el botón de tara se configura con resistencia interna tipo INPUT_PULLUP, lo que garantiza una lectura estable.

En el ciclo principal del programa (loop), el sistema ejecuta continuamente la lectura del peso y su procesamiento, una vez el usuario presiona el pulsador, se activa nuevamente la función de tara del HX711, reiniciando el valor de referencia y mostrando un mensaje en la pantalla que confirma la acción. Para evitar múltiples activaciones por rebote, se utiliza una variable de control que limita la ejecución de la tara a una sola vez por pulsación.

La lectura del peso se realiza mediante el módulo HX711, utilizando un promedio de varias muestras para mejorar la estabilidad de la medición. Posteriormente, se aplica un factor de calibración que permite convertir la señal digital en unidades de masa. Para reducir el ruido y las fluctuaciones en la señal, se implementa un filtro digital de tipo exponencial, el cual suaviza los cambios y proporciona una lectura más estable, aunque con una leve demora en la respuesta.

El valor del peso es mostrado en tiempo real en la pantalla OLED, junto con un encabezado identificador del sistema. La actualización constante de la pantalla permite al usuario monitorear de manera clara y continua las mediciones obtenidas.

### Programación del sistema de control de temperatura
# COSTOS DEL SISTEMA DESARROLLADO

| Componente                         | Cantidad | Costo unitario (COP) | Costo total (COP) |
| ---------------------------------- | -------- | -------------------- | ----------------- |
| Arduino / ESP32                    | 1        | 35.000               | 35.000            |
| HX711                              | 1        | 7.000                | 7.000             |
| Celda de carga 5 kg                | 1        | 11.000               | 11.000            |
| Pantalla OLED                      | 1        | 20.000               | 20.000            |
| Termistor NTC                      | 1        | 1.500                | 1.500             |
| Relé                               | 2        | 8.000                | 16.000            |
| Ventilador                         | 1        | 7.000                | 7.000             |
| Bombillo                           | 1        | 5.000                | 5.000             |
| LEDs                               | 3        | 500                  | 1.500             |
| Metro cable UTP                    | 1        | 500                  | 500               |
| Icopor                             | 1        | 15000                | 15000             |
| Balso                              | 1        | 1600                 | 1600              |
| Plástico                           | 1        | 15000                | 15000             |
| Protoboard                         | 1        | 10000                | 10000             |
| TOTAL                              | -        | -                    | 146.600           |

## Comparación de soluciones comerciales ofrecidas a proveedores

| Característica | Prototipo desarrollado | Dräger             | Instrumentalia S.A.S. | LEEX Medical       |
| -------------- | ---------------------- | ------------------ | --------------------- | ------------------ |
| Costo          | 146.600 COP            | 40–60 millones COP | 20–40 millones COP    | 25–50 millones COP |
| Uso            | Académico              | Clínico            | Clínico               | Clínico            |
| Control        | ON/OFF                 | PID avanzado       | PID / automático      | Automático         |
| Sensores       | Básicos                | Alta precisión     | Alta precisión        | Alta precisión     |
| Seguridad      | Baja                   | Muy alta           | Alta                  | Alta               |
| Certificación  | No                     | Sí                 | Sí                    | Sí                 |

El sistema desarrollado presenta un costo significativamente inferior en comparación con las incubadoras neonatales comerciales ofrecidas por empresas como Dräger, Instrumentalia S.A.S. y LEEX Medical. Esta diferencia se debe principalmente a que dichos equipos están diseñados para uso clínico y cumplen con estrictas normativas de seguridad, incorporando sensores de alta precisión, sistemas de control avanzados y múltiples mecanismos de protección para el paciente.

En contraste, el prototipo desarrollado tiene un enfoque académico, permitiendo simular el funcionamiento básico de una incubadora neonatal mediante el control de temperatura y la medición de peso. No obstante, presenta limitaciones importantes, como el uso de un control ON/OFF en lugar de sistemas más sofisticados, menor precisión en los sensores y una estructura mecánica menos robusta, especialmente en la base construida en icopor.

# ANÁLISIS DE RESULTADOS
## Análisis 1: Evaluación del sistema de temperatura y medición de peso

El sistema de control de temperatura implementado demostró un funcionamiento adecuado en términos generales. Se evidenció que el bombillo utilizado como elemento calefactor logró incrementar la temperatura dentro de la cabina, y que este se apagaba correctamente al alcanzar el valor deseado, lo que confirma el correcto funcionamiento del control tipo ON/OFF. De igual manera, los LEDs indicadores respondieron de manera adecuada, permitiendo identificar si la temperatura se encontraba por debajo, dentro o por encima del rango establecido, igualmente a pantalla OLED mostró correctamente la temperatura en tiempo real, y el termistor NTC proporcionó lecturas coherentes, lo que indica un correcto funcionamiento del sistema de sensado y visualización.

No obstante, se presentó una dificultad en el sistema de ventilación. Aunque el módulo relé correspondiente al ventilador sí se activaba, el ventilador no encendía, lo cual indica que el problema no se encontraba en la lógica de control ni en la señal enviada por el microcontrolador, sino en la conexión eléctrica o el propio dispositivo. A pesar de esta limitación, el sistema logró mantener la temperatura dentro de rangos adecuados mediante el control del elemento calefactor.

En cuanto al sistema de medición de peso, los resultados no fueron satisfactorios. Al utilizar un patrón de peso conocido de 3 kg aproximadamente, se observaron valores significativamente alejados del valor real. Inicialmente, la medición presentaba un error menor, pero con el tiempo las lecturas se desviaron considerablemente, lo que indica problemas de estabilidad y precisión en el sistema. Este comportamiento puede atribuirse a varios factores, como una calibración inadecuada del sensor, la utilización de una sola celda de carga,la falta de rigidez en la base construida en icopor, la cual se deformó en medio de la medición y afectó la carga.

## Análisis 2: Comparación con sistemas comerciales

Al comparar el sistema desarrollado con incubadoras neonatales comerciales ofrecidas por empresas como Dräger, Instrumentalia S.A.S. y LEEX Medical, se evidencian diferencias significativas en términos de capacidades, limitaciones y costo.

En cuanto a las capacidades, los sistemas comerciales cuentan con controladores avanzados que permiten mantener condiciones extremadamente precisas de temperatura, humedad y oxígeno, además de incorporar múltiples sensores de grado clínico. Por el contrario, el prototipo desarrollado implementa un control básico tipo ON/OFF, limitado únicamente a la regulación de temperatura y medición de peso, lo que reduce su precisión y funcionalidad.

Respecto a las limitaciones, el sistema desarrollado presenta la falta de precisión en la medición de peso, la dependencia de materiales poco rígidos como el icopor, y fallas en la integración de algunos componentes como el ventilador. En cambio, los equipos comerciales están diseñados bajo estándares médicos estrictos, con sistemas de seguridad, alarmas confiables y estructuras mecánicas robustas que garantizan estabilidad y precisión.

En términos de costo, el prototipo presenta una ventaja significativa, ya que su valor es considerablemente bajo en comparación con los sistemas comerciales, los cuales tienen costos elevados debido a su tecnología, certificaciones y nivel de seguridad requerido para uso clínico.



