; Written by Akmal Alkanov
; This code is licensed under the license.
; Copyright 2024 Akmal Alkanov
	AREA Fahrenheit, CODE, READWRITE ; C = 5 * (F - 32) / 9
	ENTRY
	MOV r0, #95
	SUB r1, r0, #32 ; this F - 32
	MOV r2, #5		; 5 to r2
	MUL r3, r1, r2	; this 5 * (F-32)
	MOV r0, #9		; 9 to r0
	MOV r9, #0	; counter
		
substract			; this block of code replace division
	SUBS r3, r3, r0
	ADD r9, r9, #1
	BHI substract
	
	MOV r1, r9
	MOV r2, #32		; 32 to r2 		; F = (9 * C / 5) + 32
	MOV r0, #9		; 9 to r0
	MUL r3, r2, r0	; 9 * 32 to r3
	MOV r2, #5		; 5 to r2
	MOV r8, #0   ; counter
		
substract2			; this block of code replace division
	SUBS r3, r3, r2
	ADD r8, r8, #1
	BHI substract2
	
	MOV r4, r8
	
	MOV r2, #32		; 32 to r2
	ADD r3, r4, r2	; 9*32/5 + 32

Stop B Stop

	END