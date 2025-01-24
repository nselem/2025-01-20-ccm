---

## **Clase: Manejo Avanzado de Archivos de Texto para Bioinformática**

### **Objetivos:**
1. Aprender a utilizar comandos avanzados de **Perl** para manipular archivos de texto.
2. Conocer y practicar herramientas avanzadas de edición con **VI**.
3. Aprender utilidades avanzadas de **Bash** para procesar archivos de texto.

---
### **Ejercicio Final: Mini Proyecto**
UTiliza el archivo FASTA con errores y el archivo tabulado (`genes.tsv`). 
1. Eliminen retornos de carro del archivo FASTA.
2. Sustituyan todos los IDs de secuencias para añadir un prefijo "Sample_".
3. Extraigan la primera y la tercera columna del archivo `genes.tsv`.
4. Combinen estos datos en un archivo llamado `final_output.tsv`.

---
### ** Parte 0: Prepara tu ambiente
- Crea una carpeta "PracticandoMiBash"
- Descarga los archivos  
https://raw.githubusercontent.com/nselem/2025-01-20-ccm/refs/heads/gh-pages/_episodes/problematic.fasta  
https://raw.githubusercontent.com/nselem/2025-01-20-ccm/refs/heads/gh-pages/_episodes/problematic_genes.tsv  
- Cambia permisos para que no se puedan escribir  
- Haz una copia y trabaja con tu copia  

### **Parte 1: Perl - Manipulación de Archivos de Texto**
#### **Ejemplo práctico: Limpiar archivos FASTA**
En bioinformática, a menudo necesitamos limpiar formatos de archivos. Por ejemplo, eliminar caracteres innecesarios como retornos de carro (`\r`), que pueden aparecer al mover archivos entre sistemas (Windows y Linux).

1. **Ejercicio con Perl:**
   - **Problema:** Tienes un archivo llamado `sequences.fasta` con retornos de carro (`\r`) que causan problemas.
   - **Solución con Perl:**
     ```bash
     perl -p -i -e 's/\r//g' sequences.fasta
     ```

   - **Explicación del comando:**
     - `perl`: Llama al intérprete de Perl.
     - `-p`: Procesa línea por línea.
     - `-i`: Edita el archivo directamente (in-place).
     - `-e`: Ejecuta el código Perl proporcionado entre comillas.
     - `'s/\r//g'`: Sustituye todos los retornos de carro (`\r`) por nada (`//`), de forma global (`g`).

   - **Práctica para los estudiantes:**
     - Proporciona un archivo `test.fasta` con líneas que incluyan caracteres `\r`.
     - Pídeles que ejecuten el comando y revisen el archivo modificado.

2. **Otros ejemplos útiles de Perl:**
   - Eliminar líneas vacías:
     ```bash
     perl -p -i -e 's/^\s*$//g' sequences.fasta
     ```
   - Añadir un prefijo a los IDs de un archivo FASTA:
     ```bash
     perl -p -i -e 's/^>(.+)$/>\|prefix_\1/g' sequences.fasta
     ```

---

### **Parte 2: Edición Avanzada con VI**
#### **Introducción rápida a VI:**
- Comandos básicos (repaso rápido):
  - Modo insertar: `i`
  - Guardar y salir: `:wq`
  - Salir sin guardar: `:q!`

#### **Comandos avanzados:**
1. **Sustituir texto:**
   - **Ejemplo:** Reemplazar todas las ocurrencias de "ACTG" por "NNNN":
     ```bash
     :%s/ACTG/NNNN/g
     ```
     - `%`: Aplica el cambio en todo el archivo.
     - `s/ACTG/NNNN/`: Sustituye "ACTG" por "NNNN".
     - `g`: Hace el cambio global (todas las ocurrencias).

2. **Eliminar varias líneas:**
   - **Ejemplo:** Borrar las líneas 10 a 20:
     ```bash
     :10,20d
     ```
     - `:10,20`: Selecciona líneas 10 a 20.
     - `d`: Borra las líneas seleccionadas.

3. **Visualizar y copiar texto:**
   - Activar modo visual y seleccionar varias líneas: `Shift + V`.
   - Copiar las líneas seleccionadas: `y`.
   - Pegar las líneas copiadas: `p`.

#### **Práctica:**
- Proporciona un archivo `example.fasta`.
- Pide a los estudiantes:
  1. Sustituir todos los espacios en blanco por guiones bajos.
  2. Eliminar las líneas que empiezan con `#`.
  3. Copiar y mover un bloque de texto.

---

### **Parte 3: Utilidades Avanzadas de Bash**
#### **Ejemplo 1: Procesar columnas en archivos tabulados**
1. **Extraer una columna específica (ejemplo con `cut`):**
   - **Archivo:** `genes.tsv`
     ```
     gene_id    sequence    length
     geneA      ATCG        100
     geneB      GCTA        200
     ```
   - **Comando para extraer la primera columna:**
     ```bash
     cut -f1 genes.tsv
     ```
   - **Explicación:**
     - `-f1`: Extrae la primera columna (separada por tabulación).

2. **Ordenar un archivo por una columna específica (`sort`):**
   ```bash
   sort -k3,3n genes.tsv
   ```
   - Ordena por la tercera columna (número de longitud).

3. **Contar líneas en un archivo (`wc`):**
   ```bash
   wc -l genes.tsv
   ```

---

#### **Ejemplo 2: Concatenar y dividir archivos**
1. **Combinar múltiples archivos FASTA en uno solo:**
   ```bash
   cat *.fasta > combined.fasta
   ```

2. **Dividir un archivo grande en partes más pequeñas:**
   ```bash
   split -l 1000 combined.fasta part_
   ```
   - Divide el archivo `combined.fasta` en archivos de 1000 líneas, con prefijo `part_`.

---

#### **Ejemplo 3: Buscar patrones específicos**
1. **Buscar un gen específico (`grep`):**
   ```bash
   grep "geneA" genes.tsv
   ```

2. **Buscar líneas que contengan una secuencia específica en un archivo FASTA:**
   ```bash
   grep -B 1 "ATCG" sequences.fasta
   ```
   - `-B 1`: Muestra también la línea anterior (por ejemplo, el encabezado FASTA).

---


### **Conclusión**
Esta clase les proporcionará herramientas clave para trabajar con archivos de texto de manera avanzada y eficiente. La combinación de **Perl**, **VI**, y utilidades avanzadas de **Bash** los prepara para tareas comunes en bioinformática, como limpiar, transformar, y procesar grandes cantidades de datos biológicos.

---
