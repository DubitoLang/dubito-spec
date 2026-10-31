<!-- SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

*Referencia · anexo B*

# Fundamentos de diseño

*(Informativo)* Por qué existe cada invariante y qué alternativas se descartaron. Sigue el registro de decisiones de arquitectura de ISO/IEC/IEEE 42010:2022: cada entrada tiene la decisión, su justificación y las alternativas consideradas.

### <a id="fund-r1"></a>R1. Ninguna garantía depende del entorno de ejecución.

**Justificación.** Una comprobación en ejecución solo detecta el fallo cuando ya ocurrió y depende de que el entorno sea correcto. Verificar al compilar hace que la garantía viaje con el binario.

**Alternativas descartadas.** Comprobaciones dinámicas como mecanismo principal; contratos solo como documentación.

### <a id="fund-r2"></a>R2. Sin entorno de ejecución obligatorio.

**Justificación.** Un recolector, una máquina virtual o un intérprete amplían la TCB y excluyen kernels y firmware.

**Alternativas descartadas.** Una máquina virtual común a los seis lenguajes; recolección de basura opcional.

### <a id="fund-r3"></a>R3. La IR existe solo en compilación.

**Justificación.** Distribuir la IR crearía un segundo formato ejecutable que verificar y licenciar; el registro distribuye fuentes.

**Alternativas descartadas.** Distribuir Stela como formato portable.

### <a id="fund-r4"></a>R4. Las bibliotecas añaden capacidades, nunca garantías.

**Justificación.** Si una biblioteca pudiera añadir garantías, la verificación dependería de qué bibliotecas se usan y no del núcleo.

**Alternativas descartadas.** Garantías definidas por bibliotecas mediante anotaciones.

### <a id="fund-r5"></a>R5. Toda postcondición elimina al menos un mutante.

**Justificación.** Una especificación que no distingue el código de sus variantes no afirma nada; la mutación lo mide de forma objetiva.

**Alternativas descartadas.** Cobertura de código como métrica; revisión manual de contratos sin medida.

### <a id="fund-r6"></a>R6. Nada implícito en la IR.

**Justificación.** Lo que no está en la IR no puede verificarse ni revisarse en el diff de significado.

**Alternativas descartadas.** Abstracciones resueltas por el backend.

### <a id="fund-r7"></a>R7. Forma canónica única e identidad derivada.

**Justificación.** La identidad por contenido hace reproducibles la caché, las dependencias y las atestaciones.

**Alternativas descartadas.** Identidad por nombre y versión declarados.

### <a id="fund-r8"></a>R8. Ninguna construcción suspende garantías.

**Justificación.** Una sola vía de escape anula la garantía de todo programa que la use, y en la práctica de todo el ecosistema.

**Alternativas descartadas.** Bloques inseguros auditados, como excepción controlada.

### <a id="fund-r9"></a>R9. Confianza mínima, declarada y enumerada.

**Justificación.** Lo que no puede demostrarse debe al menos verse: un inventario explícito convierte la confianza en algo revisable.

**Alternativas descartadas.** Confianza implícita en el sistema y en las bibliotecas nativas.

### <a id="fund-r10"></a>R10. Tipado estático y explícito, sin inferencia.

**Justificación.** El código se revisa más de lo que se escribe; los tipos escritos son información para el revisor y no dependen de un algoritmo.

**Alternativas descartadas.** Inferencia local o global; tipado gradual.

### <a id="fund-r11"></a>R11. Todos los lenguajes en los tres perfiles.

**Justificación.** Si un paradigma solo existiera en algunos perfiles, habría lenguajes de primera y de segunda, contra el principio de igual rango.

**Alternativas descartadas.** Lenguajes restringidos a hosted o a perfiles con memoria dinámica.

---

← [Anexo A](27-anexo-a.md) · [Índice](README.md) · [Glosario](29-glosario.md) →
