; Written by Akmal Alkanov
; This code is licensed under the license.
; Copyright 2024 Akmal Alkanov
    	AREA SUM, CODE, READONLY
	ENTRY

    LDR R1, =POS_SUM  ; POS address in R1
    LDR R2, =NEG_SUM  ; NEG address in R2
    MOV R3, #0        ; for current element
    MOV R4, #0        ; for sum of POS
    MOV R5, #0        ; for sum of NEG

LOOP
    LDR R0, =NUMBERS  ; load address numbers in R0
    LDR R6, [R0, R7]  ; load addres R0+R7 in R6
    CMP R6, #0        ; check R6 == 0
    BEQ END_LOOP      ; end if R6 == 0
 
    ADDGT R4, R4, R6  ; if >0 POS+
    ADDLT R5, R5, R6  ; if <0 NEG+

    ADD R7, R7, #4    ; for next element
    B LOOP            ; for loop

END_LOOP
    STR R4, [R1]      ; store value of R4 to address R1
    STR R5, [R2]      ; store value of R5 to address R2

STOP B STOP

	AREA SUM, DATA, READWRITE
	ALIGN

NUMBERS DCD 20, -8, -35, 10, 15, -7, 0
POS_SUM DCD 0
NEG_SUM DCD 0

	END
