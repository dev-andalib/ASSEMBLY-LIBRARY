.MODEL SMALL
.STACK 100H
.DATA
    ; DEFINE YOUR VARIABLES   
    
    ; GREETINGS VAR
    GREET_1 DB "----------------------------------------------------------------------------", 0DH, 0AH, "$"
    GREET   DB "X                    WELCOME TO OUR ONLINE BOOK STORE                      X", 0DH, 0AH, "$"
    GREET_2 DB "----------------------------------------------------------------------------", 0DH, 0AH, "$" 
    THANKU  DB "X----------------------THANK YOU FOR SHOPPING WITH US-------------------------X", 0DH, 0AH, "$"
    GREET_3 DB "!!!SUMMER DISCOUNT GOING ON RIGHT NOW!!!$"
    GREET_4 DB "ADD MINIMUM 3 BOOKS AND GET 10% DISCOUNT!!!$"
    GREET_5 DB "ADD 5 AND MORE TO GET FLAT 20% DISCOUNT!!!$"
    
    
    
    
    ; GENRE VARS
    
    CGEN DB 31H
    GL DB 0
    GR DB ? 
    GENRE_FLAG DB ?
    
    ;HEADING
    A DB "GENRE : ACTION$"
    D DB "GENRE : DRAMA$"
    M DB "GENRE : MYSTERY$"
    R DB "GENRE : ROMANCE$"
    
    ;loop var  FOR GENRE
    LA DW 4
    LD DW 4
    LM DW 4
    LR DW 4
    
    ; array of genres
    
    ACTION DB "ALLEGIANT___50$", "DIVERGENT___60$", "INSURGENT___60$","JACKSON_____80$"
    
    DRAMA DB "HAMLET_____200$", "MACBETH____250$", "OTHELO_____100$","TEMPEST____200$"

    MYSTERY DB  "BLUEBIRD___200$", "DEAD TIME__130$", "GONE GIRL___90$", "THE WOODS__290$"
    
    ROMANCE DB "BOOK LOVERS_40$", "CLUELESS____40$", "JANE EYRE__400$", "OUTLANDER___80$" ,    

    ;INPUT PROMPT
    I1 DB "GIVE YOUR INPUT: $"
    I2 DB "YOUR PREVIOUS INPUT WAS WRONG$"
    
    ; array prompt
    
    
    G1 db "CHOOSE A GENRE BY PRESSING THE CORRECT NUM KEYS$"
    G2 db "1.ACTION  2.DRAMA   3.MYSTERY   4.ROMANCE$" 
    
    
    ;SELECT DIFFERENT GENRE OR SPECIFIC BOOK
    P1 DB "PRESS 1 TO CHOOSE A DIFFERENT GENRE OR 2 TO ADD A BOOK TO CART OR 3 TO SEARCH A BOOK BY TITLE$"
    
    ;SEARCH INTRUCTIONS
    S2 DB "TYPE THE TITLE OF THE BOOK IN BLOCK LETTERS WITH SPACE WHERE NECESSARY, THE     TITLE MUST BE AN EXACT MATCH AND YOU MUST END IT WITH AN UNDERSCORE / _ $"

    
    
    ;SEARCHING STUFF
    GM DB ?
    SCON DW 0
    SKEY DB ?
    MAT DB 0 ; IF THERE IS A MATCHING SUBSTIRNG OR NOT
    SK DB ? ; IF WE ARE SEARCHING OR NOT
    
    SP1 DB "IS THIS THE BOOK YOU ARE LOOKING?$"
    SP2 DB "SORRY THE BOOK IS NOT AVAILABLE$"
    SP3 DB "PRESS 1 TO ADD TO ADD THE BOOK TO THE CART$"
    SP4 DB "PRESS 2 TO SEARCH AGAIN OR 3 TO GO BACK TO GENRE SELECTION$"
    
    CG DB ?  ; CHOSEN GENRE LATER NEEDED FOR SEARCHING
    
    
    ;CART VARS
    
    ;MESSAGES FOR CART
    MSG0 DB "PRESS THE NUMBER BEFORE THE BOOK THAT YOU WANT TO ENTER$"
    MSG1 DB "YOUR ITEM SUCCESSFULLY ADDED TO CART!!!$"
    MSG2 DB "TO ADD ANOTHER BOOK PRESS 1, TO CHANGE GENRE PRESS 2, FOR PAYSLIP PRESS 3$"
    MSG3 DB "YOUR ADDED ITEMS:$"
    MSG4 DB "YOUR TOTAL PRICE IS:$"
    MSG5 DB "YOU GOT A 10% DISCOUNT!!!$"
    MSG6 DB "YOU GOT A 20% DISCOUNT!!!$"
    MSG7 DB "FINAL PRICE:$" 
    MSG8 DB "TO ADD ANOTHER BOOK BY SEARCH PRESS 1, TO CHANGE GENRE PRESS 2, FOR PAYSLIP PRESS 3$"
    
    ;CART ADDITION FUNCTIONALITY VARS
    CART DB 100 DUP(?)
    ADDI DB ?
    VAR_1 DW ?
    VAR_CART DW 0
    
    
    DIS1 DW 10
    DIS2 DW 20
    FINAL_PRICE DW ? 
    RES DB 10 DUP ('$') 
    
    
    ; SORTING VARIABLES
    TOTAL_PRICE DW 0000H
    LCOUNT DW 0
    COUNTER DW ?
    len DW 0h
    index1 dw ?
    index2 dw ? 

    lastIndex dw ? 

    PRICE1  DW 0
    PRICE2  DW 0
    PRICE DW 0
    NCON DW 0
    MARK DW 0
    PIDX DW 0

    SWAPTEMP DB 0EH DUP(?)
    IDX DW 0000H
    SI2 DW 0000H
    OFFSET DW 0000H 
    
    ;DEC TO HEXADECIMAL
      
    TOTAL_P DW 0000H
    
    INNER DW ? 
    OUTER DW ?
    CALC DW 0010H
    
    
    
   
.CODE  
    MAIN PROC
        
        MOV AX, @DATA
        MOV DS, AX
        
        ; YOUR CODE STARTS HERE
        
        ; WELCOME STATEMENT START
        ; Display the first decorative line
        MOV AH, 09H
        MOV DX, OFFSET GREET_1
        INT 21H
    
        ; Display the welcome message
        MOV AH, 09H
        MOV DX, OFFSET GREET
        INT 21H
    
        ; Display the second decorative line
        MOV AH, 09H
        MOV DX, OFFSET GREET_2
        INT 21H 
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 09H
        MOV DX, OFFSET GREET_3
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 09H
        MOV DX, OFFSET GREET_4
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 09H
        MOV DX, OFFSET GREET_5
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        ; WELCOME STATEMENT END
        
        JMP BEGIN
        
        GEN:
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        BEGIN:
        MOV SK, 00H
                               
         
        
        ;initial code to search by genre
         
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, G1
        INT 21H
                                 
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        ;PRINTING THE OPTIONS TO SELECT FROM
        MOV AH, 9
        LEA DX, G2
        INT 21H
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        ;TAKE INPUT 
        
        JMP GOTO1
        
        INPUTAGAIN1:
       
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 9
        LEA DX, I2
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
       
        
        
        GOTO1: 
        MOV AH, 9   
        LEA DX, I1
        INT 21H
        
        MOV AH, 1
        INT 21H
        
        MOV CG, AL
        
        CMP AL, '1'
        
        JE ACT
        
        CMP AL, '2'
        JE DRA
        
        CMP AL, '3'
        JE MYS
             
        CMP AL, '4'
        JE ROM
        
        JMP INPUTAGAIN1         
        
        
                           ; TO PRINT EACH BOOKS OF GENRE
        ACT:
        MOV GR, 0
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 9
        LEA DX, A
        INT 21H
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV SI, 0
        MOV CX, LA
        
        START:
        MOV AH, 2
        MOV DL, CGEN ; GENRE COUNTER
        INT 21H
        INC CGEN
        
        MOV AH, 2
        MOV DL, "."
        INT 21H
        
        MOV AH, 9
        LEA DX, ACTION[SI]
        INT 21H        
        ADD SI, 000FH
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        LOOP START
        
        MOV CGEN, 31H
        JMP NP
        
        
        
        DRA:
        MOV GR, 0
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, D
        INT 21H 
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV SI, 0
        MOV CX, LD
        
        START2:
        MOV AH, 2
        MOV DL, CGEN ; GENRE COUNTER
        INT 21H
        INC CGEN
        
        MOV AH, 2
        MOV DL, "."
        INT 21H
        
        MOV AH, 9
        LEA DX, DRAMA[SI]
        INT 21H        
        ADD SI, 000FH
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
                 
        LOOP START2
        
        MOV CGEN, 31H
        JMP NP
        
        
        MYS:
        MOV GR, 0
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, M
        INT 21H
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV SI, 0
        MOV CX, LM
        
        START3:
        MOV AH, 2
        MOV DL, CGEN ; GENRE COUNTER
        INT 21H
        INC CGEN
        
        MOV AH, 2
        MOV DL, "."
        INT 21H
        
        MOV AH, 9
        LEA DX, MYSTERY[SI]
        INT 21H        
        ADD SI, 000FH
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        LOOP START3
        
        
        MOV CGEN, 31H
        JMP NP
        
        ROM:
        MOV GR, 0
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, R
        INT 21H
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV SI, 0
        MOV CX, LR
        
        START4:
        MOV AH, 2
        MOV DL, CGEN ; GENRE COUNTER
        INT 21H
        INC CGEN
        
        MOV AH, 2
        MOV DL, "."
        INT 21H
        
        MOV AH, 9
        LEA DX, ROMANCE[SI]
        INT 21H        
        ADD SI, 000FH
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
         
        LOOP START4
        
        
        MOV CGEN, 31H
        JMP NP
        
        
        ;PROMT TO SEE DIFFERENT GENRE OR SELECT BOOKS
        NP:
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, P1
        INT 21H
        
        ;NEXT LINE
        
        JMP GOTO2
        INPUTAGAIN2:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, I2
        INT 21H
        
        
        GOTO2:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, I1
        INT 21H
        
        MOV AH, 1
        INT 21H
        
        
        
        CMP AL, '1'
        JE GEN  ; START FROM THE BEGINNIG OF NEW GENRE SELECTION
        
        CMP AL, '2'
        JE CARTSTART
         
        CMP AL, '3'
        JE SEARCH
        
        JMP INPUTAGAIN2
        
        ; BINARY SEARCH FUNCTIONALITY FOR ACTION
         SEARCH:
        
        MOV SK, 01H 
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
       
        MOV AH, 9
        LEA DX, S2
        INT 21H
                                 
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        
        
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AH,9
        LEA DX, I1
        INT 21H
         
        
        
        
        
        
        
        
        ; CORE SEARCH METHOD
        MOV GL, 0000H 
        
        CMP CG, '1'
        JE ACT6
        
        CMP CG, '2'
        JE DRA6
        
        CMP CG, '3'
        JE MYS6
        
        CMP CG, '4'
        JE ROM6
        
        ACT6:
        MOV AX, LA
        MOV GR, AL
        JMP S 
        
        DRA6:
        MOV AX, LD
        MOV GR, AL
        JMP S
        
        MYS6:
        MOV AX, LM
        MOV GR, AL
        JMP S
        
        ROM6:
        MOV AX, LR
        MOV GR, AL
        JMP S
        
        
        
        S:
        DEC GR
        
         
        INPUT1:
        MOV AH, 1
        INT 21H
        MOV SKEY, AL
        
        CMP SKEY, ' '
        JE INPUT1
        
        CMP SKEY, '_'
        JE ENDLOOP1
        
        CMP M, 1
        JE SKIP1
        
        
        
        MOVE1:
        MOV CL, GR
        MOV CH, GL
        CMP CH, CL
        JG ENDLOOP1
        
        
        ;SEARCH PART
        MOV AH, GR
        MOV AL, GL
        ADD AL, AH
        MOV AH, 00H
        MOV BL, 02H
        DIV BL
        MOV GM, AL
        
        MOV AL, GM
        MOV AH, 00H
        MOV BL, 10H
        MUL BL
        
        MOV AH, 00H
        MOV SI, AX
        MOV BL, GM
        MOV BH, 00H
        SUB SI, BX
        ADD SI, SCON
        
        
        
        SKIP1:
        
        CMP CG, '1'
        JE ACT2
        
        CMP CG, '2'
        JE DRA2
        
        CMP CG, '3'
        JE MYS2
        
        CMP CG, '4'
        JE ROM2
        
        ACT2:
        MOV DL, ACTION[SI]
        JMP CON
        
        DRA2:
        MOV DL, DRAMA[SI]
        JMP CON
        
        MYS2:
        MOV DL, MYSTERY[SI]
        JMP CON
        
        
        ROM2:
        MOV DL, ROMANCE[SI]
        JMP CON
        
        
        CON:
        CMP DL, ' '
        JE HANDLESPACE1
        
        
        CMP SKEY, DL 
        JG INCL1
        
        CMP SKEY, DL 
        JL DECR1
        
        CMP SKEY, DL 
        JE INCFLAG1
        
        
        INCL1:
        MOV CL, GM
        MOV GL, CL
        INC GL
        MOV MAT, 0
        
        JMP MOVE1
        
        
        DECR1:
        MOV CL, GM
        MOV GR, CL
        DEC GR
        MOV MAT, 0
        
        JMP MOVE1
        
        
        INCFLAG1:
        MOV MAT, 1
        INC SI
        INC SCON
        ; TAKE INPUT AGAIN
        JMP INPUT1              
        
        HANDLESPACE1:
        INC SCON
        INC SI
        JMP SKIP1
               

        
        
        
        
        
        
        ENDLOOP1:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        
        
        MOV DL, 01H
        CMP MAT, DL
        JE HYPHEN
        JNE NOTMATCH1
        
        HYPHEN:
        
        
        
        CMP CG, '1'
        JE ACT4
        
        CMP CG, '2'
        JE DRA4
        
        CMP CG, '3'
        JE MYS4
        
        CMP CG, '4'
        JE ROM4
        
        ACT4:
        MOV CL, ACTION[SI]
        JMP CON3
        
        DRA4:
        MOV CL, DRAMA[SI]
        JMP CON3
        
        MYS4:
        MOV CL, MYSTERY[SI]
        JMP CON3
        
        
        ROM4:
        MOV CL, ROMANCE[SI]
        JMP CON3
        
        CON3:
        
        
        CMP CL, '_'
        JE MATCH1
        JNE NOTMATCH1
        
        
        
        MATCH1:
        MOV AH, 9
        SUB SI, SCON
        
        
        CMP CG, '1'
        JE ACT3
        
        CMP CG, '2'
        JE DRA3
        
        CMP CG, '3'
        JE MYS3
        
        CMP CG, '4'
        JE ROM3
        
        ACT3:
        LEA DX, ACTION[SI]
        JMP CON2
        
        DRA3:
        LEA DX, DRAMA[SI]
        JMP CON2
        
        MYS3:
        LEA DX, MYSTERY[SI]
        JMP CON2
        
        
        ROM3:
        LEA DX, ROMANCE[SI]
        JMP CON2
        
        
        CON2: 
        INT 21H
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, SP1
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV SCON, 0
        MOV MAT, 0
        JMP NEXT_INSTRUCTIONS:
        
        
        NOTMATCH1:
        MOV AH, 9
        LEA DX, SP2
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        MOV SCON, 0
        MOV MAT, 0
        JMP NEXT_INSTRUCTIONS2
        
        NEXT_INSTRUCTIONS:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, SP3
        INT 21H  
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, SP4
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, I1
        INT 21H
        
        MOV AH, 2
        MOV DL, ' '
        INT 21H
        
        MOV AH, 1
        INT 21H
        
        
        
        CMP AL, '1'
        JE  SEARCH_ADD
        
        CMP AL, '2'
        JE  SEARCH
        
        
        CMP AL, '3'
        JE  BEGIN
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, I2
        INT 21H
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        JMP NEXT_INSTRUCTIONS  
        
        
        NEXT_INSTRUCTIONS2:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, SP4
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, I1
        INT 21H
        
        MOV AH, 2
        MOV DL, ' '
        INT 21H
        
        MOV AH, 1
        INT 21H
        
        
        
        
        
        CMP AL, '2'
        JE  SEARCH
        
        
        CMP AL, '3'
        JE  BEGIN
        
        
        
        
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 9
        LEA DX, I2
        INT 21H
        
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H 
        MOV DL, 0AH
        INT 21H
        
        JMP NEXT_INSTRUCTIONS2    
        
        
        
        
        
        
        ; CART FUNCTIONALITY UTILIZED
        CARTSTART:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        ;INPUT FOR ADDING IN CART
        JMP GOTO3
        
        INPUTAGAIN3:
       
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 9
        LEA DX, I2
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
       
        
        
        GOTO3: 
        MOV AH, 9   
        LEA DX, MSG0
        INT 21H 
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        CART_ADDING:
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        MOV AH, 1
        INT 21H
        
        CMP AL, 30H
        JLE INPUTAGAIN2 
        
        CMP AL, 39H
        JG INPUTAGAIN2
        
        SUB AL, 30H ;CONVERTING TO DECI NUMBER
        
        SUB AL, 1H
        
        MOV ADDI, AL
        
        MOV BL, 10H
        MUL BL
        SUB AL, ADDI
        
        
        
        
        MOV SI, AX
        
        SEARCH_ADD:
         
        MOV CX, 15
        
        
        ARRAYS:
        
        
        
        CMP CG, '1'
        JE ACT5
        
        CMP CG, '2'
        JE DRA5
        
        CMP CG, '3'
        JE MYS5
        
        CMP CG, '4'
        JE ROM5 
        
        
        ACT5:
        MOV DL, ACTION[SI]
        JMP ADDING:
        
        DRA5:
        MOV DL, DRAMA[SI]
        JMP ADDING:
        
        
        MYS5:
        MOV DL, MYSTERY[SI]
        JMP ADDING:
        
        ROM5:
        MOV DL, ROMANCE[SI]
        JMP ADDING:
        
        
        ADDING:
        MOV VAR_1, SI
        
        MOV BX, VAR_CART
        MOV SI, BX    
        MOV CART[SI], DL
        INC BX
        MOV VAR_CART, BX
        
        MOV SI, VAR_1
        INC SI
        
        LOOP ARRAYS 
        
        INC len ; FOR TRACKING HOW MANY BOOKS BEEN ADDED TO CART  
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H
        
        ;;MSG FOR SUCCESSFULL ADDING TO CART
        MOV AH, 9
        LEA DX, MSG1
        INT 21H 
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H
        
        
        CMP SK, 01H
        JE SKK
        
            
        
        ;;MSG FOR GIVING OPTION TO ADD ANOTHER BOOK OR ELSE
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H 
        
        
        MOV AH, 9
        LEA DX, MSG2
        INT 21H
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H
        
        
        MOV AH, 1
        INT 21H  ;USER INPUT FOR ADDING ANOTHER BOOK OR OTHER ACTION
        
        
        CMP AL, '1'
        JE CART_ADDING
       
        CMP AL, '3'
        JE PAYSLIP
        
        CMP AL, '2'
        JE BEGIN
        
        
        
        SKK: ; TO HANDLE AFTER WORK OF CART IN SEARCHING CASE
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H 
        
        
        MOV AH, 9
        LEA DX, MSG8
        INT 21H
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H
        
        
        MOV AH, 1
        INT 21H  ;USER INPUT FOR ADDING ANOTHER BOOK OR OTHER ACTION
        
        
        CMP AL, '1'
        JE SEARCH
       
        CMP AL, '3'
        JE PAYSLIP
        
        CMP AL, '2'
        JE BEGIN
        
        
        
        PAYSLIP:
        
        ;SORTING IN DECENDING ORDER
        
        MOV CX, 0001H
        CMP len, CX
        JLE SORT_END
        
        mov cx , len
        sub cx , 0001h

        mov index1 , 0000h
        MOV LCOUNT, 0000H

        loop1:
        mov bx , index1
        MOV BX, INDEX1
        add bx , 0001h
        mov index2 , bx
    
        mov dx, len
        DEC DX 
        SUB DX, LCOUNT
    
        mov lastIndex , dx
        MOV COUNTER, CX
    
        loop2:
    
        MOV MARK, 0000H; PRICE CALCULATION FOR PRICE 1
        MOV BX, index1
        JMP TAKEPRICE
        PRICEDONE:
        MOV AX, PRICE
        MOV PRICE1, AX
         
        MOV MARK, 0001H     ; PRICE CALCULATION FOR PRICE 2
        MOV BX, index2
        JMP TAKEPRICE
        PRICEDONE2:
        MOV AX, PRICE
        MOV PRICE2, AX 
         
         
        MOV AX, PRICE1                                
        cmp AX , PRICE2                                 
         
        
        jl swap
        jmp not_swap 
         
        swap:
         
            ;CALCULATING SI VALUE FOR FIRST LETTER
            mov AX , index1
            MOV BL, 10H
            MUL BL
            SUB AX, index1
            MOV SI, AX
            
                
            MOV CX, 000EH
            

            
            COPY:
            MOV AL, CART[SI]
            MOV BX, SI
            MOV SI, IDX
            MOV SWAPTEMP[SI], AL 
            INC SI
            MOV IDX, SI
            MOV SI, BX
            INC SI          
            LOOP COPY
            MOV IDX, 0000H
            
            ;CALCULATING SI VALUE FOR FIRST LETTER OF INDEX 1 AND INDEX 2
            mov AX , index2
            MOV BL, 10H
            MUL BL
            SUB AX, index2
            MOV SI2, AX
            
            
            
            mov AX , index1
            MOV BL, 10H
            MUL BL
            SUB AX, index1
            MOV SI, AX 

            MOV CX, 000EH 
            
            
            COPY2:
            MOV BX, SI
            MOV SI, SI2
            ADD SI, OFFSET
            MOV AL, CART[SI]
            MOV SI, BX
            MOV CART[SI], AL
            INC SI
            INC OFFSET       
            LOOP COPY2            
            MOV OFFSET, 0000H
            

            
            
            
            mov AX , index2
            MOV BL, 10H
            MUL BL
            SUB AX, index2
            MOV SI, AX
               
            MOV CX, 000EH
            
            COPY3:
            MOV BX, SI
            MOV SI, IDX
            MOV AL, SWAPTEMP[SI]
            MOV SI, BX
            MOV CART[SI], AL 
            INC SI
            INC IDX          
            LOOP COPY3
            MOV IDX, 0000H
            
              
            
         not_swap:
            mov bx , lastIndex
            sub bx , 0001h
            mov lastIndex , bx
            
            cmp bx , 0000H
            jle end 
            
            mov bx , index2
            add bx , 0001h
            mov index2 , bx
            
                        
            jmp loop2
            
    end:
        mov bx , index1
        add bx , 0001h
        mov index1 , bx
        MOV CX,COUNTER
        INC LCOUNT
        loop loop1
        
        
        JMP SORT_END
        
        
        TAKEPRICE:
        MOV PRICE, 0000H

        INC BX
        MOV PIDX, BX
        MOV AX, BX
        MOV BL, 10H
        MUL BL
        INC PIDX
        SUB AX, PIDX
        MOV BX, PIDX
        SUB BX, 0002H
        MOV PIDX, BX

        MOV SI, AX
        DEC SI

     PRICECALC:
        MOV AL, CART[SI]
        MOV AH, 00H
        SUB AL, 30H
        ADD PRICE, AX

     BACKTEN:
        DEC SI
        MOV DL, CART[SI]
        CMP DL, '_'
        JNE PRICEMUL
        JE UNDER

     PRICEMUL:
        INC NCON
        MOV CX, NCON
        MOV BL, 10H
        MOV AL, CART[SI]
        SUB AL, 30H
        MOV AH, 00H

     TEN:
        MUL BL
        LOOP TEN

        ADD PRICE, AX
        JMP BACKTEN
           
           
     UNDER:
        MOV NCON, 0H
        
        


        CMP MARK, 0000H
        JE PRICEDONE

        CMP MARK, 0001H
        JE PRICEDONE2
        
        
        
        ; SORTING END
        
        SORT_END:
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H
        
        MOV AH, 9
        LEA DX, MSG3, ;MSG FOR ADDED ITEMS
        INT 21H
        
        MOV AH, 2
        MOV DL,0DH   ;NEXT LINE
        INT 21H 
        MOV DL,0AH 
        INT 21H
        
        PRINTCART:
        MOV CX, len

        MOV SI, 0000H

        PC:
        ;ADD A PAYSLIP COMMENT
        MOV AH, 9
        LEA DX, CART[SI]
        INT 21H

        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H

        ADD SI, 000FH

        LOOP PC
        
        ; TOTAL PRICE CALC 
        
    MOV CX, len
    MOV SI, 0000H
    
    
    
    
    TOTALPRICE:
    MOV BX, CX
    MOV AX, BX
    MOV DX, 0010H
    MUL DL
    SUB AX,BX
    MOV SI, AX
    
    MOV COUNTER, CX
    SUB SI, 0002H

    
        MOV AL, CART[SI]
        MOV AH, 00H
        SUB AL, 30H
        ADD TOTAL_PRICE, AX
         

     BACKTEN2:
        DEC SI
        MOV DL, CART[SI]
        CMP DL, '_'
        JNE PRICEMUL2
        JE UNDER2

     PRICEMUL2:
        INC NCON
        MOV CX, NCON
        MOV BL, 10
        MOV AL, CART[SI]
        SUB AL, 30H
        MOV AH, 00H

     TEN2:
        MUL BL
        LOOP TEN2

        ADD TOTAL_PRICE, AX
        JMP BACKTEN2
           
           
     UNDER2:
        MOV NCON, 0H
        MOV CX, COUNTER 
        MOV BX, TOTAL_PRICE
        ADD TOTAL_P, BX
        
       
         
        
    
    
    LOOP TOTALPRICE
    
       
                     

CONVERT:       
    MOV AX, DATA
    MOV DS, AX
   
    MOV AX, TOTAL_PRICE
      
    LEA SI, RES
    CALL HEX_2_DEC
    ; RETURN HERE
    JMP DIS 
    
   
           



HEX_2_DEC:
    MOV CX, 0
    MOV BX, 10
   
L1: 
    MOV DX, 0
    DIV BX
    ADD DL, 30H
    PUSH DX
    INC CX
    CMP AX, 9
    JG L1
     
    ADD AL, 30H
    MOV [SI], AL
     
L2: 
    POP AX
    INC SI
    MOV [SI], AL
    LOOP L2
    RET
        
        ;;PRICE
        
        DIS:
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        CMP len, 03H
        JE DISCOUNT1

        CMP len, 04H
        JE DISCOUNT1

        CMP len, 05H
        JGE DISCOUNT2

        JMP NODISCOUNT:
        
        DISCOUNT1:
        
        MOV AH, 9
        LEA DX, MSG5, ;MSG FOR 10 PERCENT DISCOUNT
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        MOV AX, TOTAL_PRICE      ; LOAD PRICE INTO AX REGISTER
        MOV BX, DIS1        ; LOAD DISCOUNT RATE INTO BX REGISTER

        MOV CX, AX         ; MOVE THE PRICE TO CX REGISTER FOR SAFETY
        MUL BX             ; MULTIPLY PRICE BY DISCOUNT RATE
        MOV BX, 100        ; LOAD 100 INTO BX
        DIV BX
        
        MOV BX, TOTAL_PRICE
        SUB BX, AX         ; FINAL PRICE IS IN BX
        MOV FINAL_PRICE, BX
        
       
        
        
        
        MOV AH, 9
        LEA DX, MSG7, ;MSG FOR FINAL PRICE
        INT 21H
        
        ;;CONVERTER FOR HEXA TO DEC TO PRINT FINAL PRICE TO USER
        
        CONVERT_1:       
    
   
        MOV AX, FINAL_PRICE
      
        LEA SI, RES
        CALL HEX_2_DEC_1
   
        LEA DX, RES
        MOV AH, 9
        INT 21H 
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        
        ;EXIT MESSGES
        
        ;Display the "Thank you" message
        MOV AH, 09H
        MOV DX, OFFSET THANKU
        INT 21H
            
        MOV AH, 4CH
        INT 21H        



        HEX_2_DEC_1:
        MOV CX, 0
        MOV BX, 10
   
        LOOP1_1: 
        MOV DX, 0
        DIV BX
        ADD DL, 30H
        PUSH DX
        INC CX
        CMP AX, 9
        JG LOOP1_1
     
        ADD AL, 30H
        MOV [SI], AL
     
        LOOP2_1: 
        POP AX
        INC SI
        MOV [SI], AL
        LOOP LOOP2_1 
    
        RET
        
        
        
        
        
        DISCOUNT2:
        
        MOV AH, 9
        LEA DX, MSG6, ;MSG FOR 20 PERCENT DISCOUNT
        INT 21H
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        MOV AX, TOTAL_PRICE      ; LOAD PRICE INTO AX REGISTER
        MOV BX, DIS2        ; LOAD DISCOUNT RATE INTO BX REGISTER

        MOV CX, AX         ; MOVE THE PRICE TO CX REGISTER FOR SAFE
        MUL BX             ; MULTIPY PRICE BY DISCOUNT RATE
        MOV BX, 100        ; LOAD 100 INTO BX
        DIV BX
        
        MOV BX, TOTAL_PRICE
        SUB BX, AX         ;FINAL PRICE IN BX
        MOV FINAL_PRICE, BX
        
        MOV AH, 9
        LEA DX, MSG7, ;MSG FOR FINAL PRICE
        INT 21H
        
        ;;CONVERTER FOR HEXA TO DEC TO PRINT FINAL PRICE TO USER
        
        CONVERT_2:       
    
   
        MOV AX, FINAL_PRICE
      
        LEA SI, RES
        CALL HEX_2_DEC_2
   
        LEA DX, RES
        MOV AH, 9
        INT 21H
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        
        ;EXIT MESSGES
        
        ;Display the "Thank you" message
        MOV AH, 09H
        MOV DX, OFFSET THANKU
        INT 21H
        
            
        MOV AH, 4CH
        INT 21H        



        HEX_2_DEC_2:
        MOV CX, 0
        MOV BX, 10
   
        LOOP1_2: 
        MOV DX, 0
        DIV BX
        ADD DL, 30H
        PUSH DX
        INC CX
        CMP AX, 9
        JG LOOP1_2
     
        ADD AL, 30H
        MOV [SI], AL
     
        LOOP2_2: 
        POP AX
        INC SI
        MOV [SI], AL
        LOOP LOOP2_2 
    
        RET
        
         
        
        NODISCOUNT:
        
        MOV AH, 9
        LEA DX, MSG7, ;MSG FOR FINAL PRICE
        INT 21H
        
        
        
        
        ;;CONVERTER FOR HEXA TO DEC TO PRINT FINAL PRICE TO USER
        
        
        
        CONVERT_3:       
    
   
        MOV AX, TOTAL_PRICE
      
        LEA SI, RES
        CALL HEX_2_DEC_3
   
        LEA DX, RES
        MOV AH, 9
        INT 21H
        
        ;NEXT LINE
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H 
        
        MOV AH, 2
        MOV DL, 0DH
        INT 21H
        MOV DL, 0AH
        INT 21H
        
        
        
        ;EXIT MESSGES
        
        ;Display the "Thank you" message
        MOV AH, 09H
        MOV DX, OFFSET THANKU
        INT 21H
         
            
        MOV AH, 4CH
        INT 21H        



        HEX_2_DEC_3:
        MOV CX, 0
        MOV BX, 10
   
        LOOP1_3: 
        MOV DX, 0
        DIV BX
        ADD DL, 30H
        PUSH DX
        INC CX
        CMP AX, 9
        JG LOOP1_3
     
        ADD AL, 30H
        MOV [SI], AL
     
        LOOP2_3: 
        POP AX
        INC SI
        MOV [SI], AL
        LOOP LOOP2_3 
    
        RET
        
        
        
        
        
       
        
       
        EXIT: 
        
        
                
        ; YOUR CODE ENDS HERE
        
        MOV AX, 4C00H
        INT 21H 
        
    MAIN ENDP
    END MAIN                   