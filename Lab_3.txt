; Written by Akmal Alkanov
; This code is licensed under the license.
; Copyright 2024 Akmal Alkanov	
	AREA Count, CODE, READWRITE 
	ENTRY
    LDR R6, =countOfVowels  ; address in R6
    LDR R7, =countOfNotVowels  ; address in R7
	ADR R0, string ; Load address of string to R0
	MOV R1, #0 		; counter of vowels
	MOV R2, #0		; counter of not vowels

loop
	ADR R4, vowels	; load address of vowels to R4
	LDRB R3, [R0] 	; Load the character from the address R0 contains
	CMP R3, #0 		; Compare with 0
	BEQ THE_END		; end if string = 0

secondLoop				
	LDRB R5, [R4]	; load char from vowels
	CMP R5, #0		; check if vowels end
	BEQ NEXT_CHAR_IF_NOT_VOWEL
	CMP R3, R5		; check R3 == R5
	BEQ NEXT_CHAR_IF_VOWEL
	
	ADD R4, R4, #1	;for next char in vowels
	
	B secondLoop

NEXT_CHAR_IF_VOWEL				
	ADD R1, R1, #1		; ++count of vowels
	ADD R0, R0, #1 		; ++address of string
	B loop
	
NEXT_CHAR_IF_NOT_VOWEL
	ADD R2, R2, #1		; ++count of not vowels
	ADD R0, R0, #1      ; ++address of string
	B loop

THE_END
    STR R1, [R6]      	; store value of R1 to address R6
    STR R2, [R7] 		; store value of R2 to address R7
STOP B STOP

	AREA Count, CODE, READWRITE
string	DCB "ARM assembly language is important to learn!",0
vowels	DCB "A","O","E","I","U","Y","a","o","e","i","u","y",0
countOfVowels DCD 0
countOfNotVowels DCD 0
	END