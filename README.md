# TP-INFOII-2023
Trabajop Práctico 2023
#ifndef MY_LIB
#define MY_LIB

#include <stdio.h>

typedef enum {
  espera = 0,
  cargar = 1
} estados_c;

typedef struct {
  int n;          // Nivel actual (cambiado a tipo int para mayor nivel)
  int n_set;      // Nivel seteado
  int deltaN;     // Delta de nivel
} nivel_c;

nivel_c f_inicio(void); // Lee el archivo de configuración y carga las variables.
estados_c f_espera(nivel_c);
estados_c f_cargar(nivel_c);

#endif


•	Archivo main.c
con Switch case

#include "mylib.h"

int main() {
    nivel_c config;
    estados_c estado = espera; // primer estado

    config = inicio();
    while(1){
      switch (estado) {
        case espera: estado = f_espera(config);
                     break;
        case cargar: estado = f_cargar(config);
                       break;
      }
    }
  return 0;
}



•	Con Punteros a funciones








•	Archivo config.conf

# Nivel de carga
c_set 50 cm
# Delta de carga
deltaC 20 cm

// mylib.c
#include "mylib.h"
nivel_c f_inicio(void) {
  nivel_c config;
  config.n = 0;
  config.n_set = 50;
  config.deltaN = 20;
  return config;
}
estados_c f_espera(nivel_c config) {
  
    if (config.n < config.n_set) {
    // Si se cumple la condición, retornamos el estado de carga.
    return cargar;
  } else {
    // Si no se cumple la condición, permanecemos en el estado de espera.
    return espera;
  }
}
estados_c f_cargar(nivel_c config) {
    config.n = config.n + config.deltaN

  // Después de realizar la carga, verificamos si el nivel alcanzó el nivel seteado.
  if (config.n >= config.n_set) {
    // Si se cumple la condición, volvemos al estado de espera.
    return espera;
  } else {
    // Si no se cumple la condición, permanecemos en el estado de carga.
    return cargar;
  }
}
