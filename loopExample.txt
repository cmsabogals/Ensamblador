; loopExample.asm - generate a number sequence till the value user define.

.386
.model flat,stdcall
.stack 4096
ExitProcess proto,dwExitCode:dword

INCLUDE irvine32.inc
INCLUDE macros.inc

.data
;Declaracion de variables con mensajes y variables auxiliares
iNum BYTE "Ingresa un numero entero de 0 a 10: ", 0
result BYTE "La secuencia de numeros es: ", 0
stopNum SDWORD ?
i SDWORD ? 

.code
main PROC
	mov edx, OFFSET iNum   ; Imprimir mensaje en consola
	call WriteString 
	call ReadInt		   ; Leer entrada de usuario
	mov stopNum, eax
	mov i, 1
	mov edx, OFFSET result ; Imprimir mensaje de resultado en consola
	call WriteString
again:					 ; etiqueta con bloque de instrucciones
	cmp i, eax			 ; Instruccion de comparacion
	jg done				 ; Si la i es mayor que el registro eax, entonces se realiza interrupcion
	mov eax, i
	call WriteInt         ; Imprimir resultado de i, variable acumuladora
	mov al,' '
	call WriteChar		  ; Imprimir espacio (Proceso de libreria Irvine)
	inc i				  ; Instruccion de incremento para la variable i
	mov eax, stopNum		
	jmp again
done:					 ; etiqueta con bloque de instrucciones para finalizar programa
	call Crlf
	call waitMsg		 ; Muestra en consola el mensjae "Press [Enter] to continue...", al presionar una tecla interrumpe el programa
	exit
main ENDP
END main