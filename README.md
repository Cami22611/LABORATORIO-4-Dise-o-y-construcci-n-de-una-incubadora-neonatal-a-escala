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

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/382d679f-5c01-4469-b8de-b81a2d7200f4" />

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

´´´bash
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include "HX711.h"

// OLED
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

// HX711
#define DOUT  4
#define CLK   5
HX711 scale;

// Botón
#define BOTON_TARA 14


float calibration_factor = -300;

bool yaTarado = false;
float peso_filtrado = 0;

void setup() {
  Serial.begin(115200);
  Wire.begin(21, 22);

  // OLED
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

  // HX711
  scale.begin(DOUT, CLK);
  scale.set_scale();
  scale.tare();

  pinMode(BOTON_TARA, INPUT_PULLUP);
}

void loop() {

  // ----------- TARA -----------
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

  // ----------- OLED -----------
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
´´´ 



