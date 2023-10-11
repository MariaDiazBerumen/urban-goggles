
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12222481&assignment_repo_type=AssignmentRepo)
![](https://s3.amazonaws.com/videos.pentesteracademy.com/videos/badges/low/arm-assembly.png)


<pre>

	<p align=center>

Tecnológico Nacional de México
Instituto Tecnológico de Tijuana

Departamento de Sistemas y Computación
Ingeniería en Sistemas Computacionales

Semestre:
Febrero - Junio 2022

Materia:
Lenguajes de interfaz

Docente:
M.C. Rene Solis Reyes 

Unidad:
2

Título del trabajo:
2.3 Corrida de programas ARM32 (apoyados en  KERNEL de Linux)

Estudiante:
Díaz Berumen María de los Ángeles 21210368

	</p>

</pre>

<pre>



	//Nombre:Diaz Berumen Maria de los Angeles 21210368
//Objetivo: Usar la recursividad con ejemplo del factorial
//Fecha:09/octubre/2023
/*
#include <stdio.h>  // Including the standard input-output header file for functions like printf.

/**
 * Recursive function that prints the numbers from 1 to n in ascending order.
 *
 * @param n: The number up to which the numbers should be printed.
 */
void printNumbers(int n) {
    if (n > 1) {
        printNumbers(n - 1);  // Recursive call with n-1.
    }
    printf("%d ", n);  // Printing the current number.
}

int main() {
    int n;

    printf("Enter a positive integer: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Invalid input. Please enter a positive integer.\n");
        return 1;  // Returning a non-zero value to indicate an error.
    }

    printf("Numbers from 1 to %d: ", n);
    printNumbers(n);
    printf("\n");

    return 0;
}
*/

-----------------------------ARM----------------
.section .data

.section .bss
.comm n, 4

.section .text
.global _start

_start:
    @ Establece el valor de n a 0
    mov r3, #0
    str r3, [n]

    @ Solicita al usuario que ingrese un número positivo
    ldr r0, =prompt
    bl printf

    @ Lee el número ingresado por el usuario
    ldr r0, =format
    ldr r1, =n
    bl scanf

    @ Comprueba si el número ingresado es positivo
    ldr r1, [n]
    cmp r1, #0
    ble exit

    @ Llama a la función printNumbers
    ldr r0, =format
    ldr r1, [n]
    bl printf

    @ Imprime un salto de línea
    ldr r0, =newline
    bl printf

exit:
    @ Sal de la aplicación
    mov r7, #1        @ Código de salida 1
    swi 0             @ Llamada al sistema para salir

printNumbers:
    @ Subrutina recursiva para imprimir números
    push {lr}         @ Guarda el enlace de retorno en la pila

    @ Comprueba si n es igual a 1
    ldr r1, [n]
    cmp r1, #1
    beq print_one

    @ Llama recursivamente con n - 1
    ldr r0, [n]
    sub r0, r0, #1
    str r0, [n]
    bl printNumbers

print_one:
    @ Imprime el número actual
    ldr r0, =number_format
    ldr r1, [n]
    bl printf

    pop {lr}          @ Restaura el enlace de retorno
    bx lr             @ Retorna

.section .data

prompt:
    .asciz "Enter a positive integer: "
newline:
    .asciz "\n"
format:
    .asciz "%d"
number_format:
    .asciz "%d "




	<p align=left>




