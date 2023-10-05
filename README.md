# AdM

Arquitectura de microcontroladores

Alumno: Jesus Eduardo Gonzales Davila

# Preguntas orientadoras
## 1. Describa brevemente los diferentes perfiles de familias de microprocesadores/microcontroladores de ARM. Explique alguna de sus diferencias características.
La empresa ARM se dedica a desarrollar arquitecturas de microcontroladores para diferentes usos e industrias. A pesar de contar con varias familias a través de los años, desde sus origenes, en la actualidad la familia de microcontroladores con mayor uso es la familia Cortex. Dentro de esta familia tenemos variantes, como se aprecia en la imagen inferior.
![image](https://github.com/jegd/AdM/assets/105693319/8863d09a-ecf2-4c44-876d-e8897fe7b01c)
- Cortex-A: Microcontrolares para sistemas que necesiten un alto desempeño. La mayoria en la página de ARM utiliza la arquitectura ARMv9. Frecuentemente se usa con Linux.
- Cortex-M: Microcontroladores utilizados para aplicaciones que requieren pequeños usos de energía. Encontramos aquí los microcontroladores Cortex-M0, Cortex-M0+, Cotex-M1, Cortex-M3 y Cortex-M4 que utilizan mayormente la arquitectura ARMv7 y ARMv6.
- Cortex-R: Son microcontroladores robustos con muy buen desempeño en procesamiento en tiempo real. Suelen usarse en la industria automotriz.
# Cortex M
## 1. Describa brevemente las diferencias entre las familias de procesadores Cortex M0, M3 y M4.
- Los microcontroladores Cortex-M3 y Cortex-M4 son microcontroladores que utilizan la arquitectura ARMv7. Ambos son microncontroladores de alto desempeño. Sin embargo algunos microcontroladores Cortex-M4 tienen añadidos que los Cortex-M3 no tienen como por ejemplo SIMD (Single instruction, multiple data), fast MAC e intrucciones de saturación aritmética, por lo que pueden ser utilizados en procesamiento de señales.
- Los microcontroladores Cortex-M0, Cortex-M0+ y Cortex-M1 son microcontroladores basados en al arquitectura ARMv6 que tienen un set de instrucciones más pequeño. Los Cortex-M0 y Cortex-M0+ son muy pequeños en tamaño. Los Cortex-M0+ tienen la mejor optimización de baja energía. Los microcontroladores Cortex-M1 son diseñados específicamente para aplicaiones de FPGA.
