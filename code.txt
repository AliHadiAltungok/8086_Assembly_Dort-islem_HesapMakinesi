org 100h 

.data

    a      db  "Yapacaginiz islem: $"
    ai     db  "Toplam=t, Cikarma=c, Bolme=b, Carpma=p$"
    x1     db  "ilk sayiyi gir:$"
    x2     db  "ikinci sayiyi gir:$"
    x3     db  "islem sonucu=:$" 
    x4     db  "Devam etmek icin d cikmac icin q a basiniz$" 
    b      db  0ah,0dh,"MICRO$" 
    c      db  0ah,0dh,"LAB8$"
    d      db  0ah,0dh,"$" 
    
    
    
    S    dw  ?,"$"
    lbk    db 13,10,'$'   
    numstr db '$$$$$$'      



                
.code

bas:   
lea dx,d    ;
mov ah,9h   
int 21h

mov ax,0
mov bx,0
mov cx,0
mov dx,0

mov ax,@data
mov ds,ax

    
    
lea dx,a    ;
mov ah,9h   
int 21h
lea dx,d    ;
mov ah,9h   
int 21h 
lea dx,ai    ;
mov ah,9h   
int 21h    
lea dx,d    ;
mov ah,9h   
int 21h

mov ah,01   
int 21h      
mov bl,al

lea dx,d    ;
    mov ah,9h   
    int 21h   
            
            
Tmi:
    cmp bl,'t'
    jne Cmi
    jmp tIleBitir

Cmi:
    cmp bl,'c'
    jne Bmi
    jmp cIleBitir
    
Bmi:
    cmp bl,'b'
    jne Pmi
    jmp bIleBitir        
                    
Pmi:
    cmp bl,'p'
    jne bas
    jmp pIleBitir 
    
             
             
       
tIleBitir: 
    
    lea dx,x1    ;
    mov ah,9h   
    int 21h    
    lea dx,d    ;
    mov ah,9h   
    int 21h
             
    mov ah,01   ;
    int 21h      
    mov cl,al
    mov ch,0 
    sub cl,30h
             
              
    lea dx,d    ;
    mov ah,9h   
    int 21h          
             
    lea dx,x2    ;
    mov ah,9h   
    int 21h  
    lea dx,d    ;
    mov ah,9h   
    int 21h  
    
    mov ah,01   ;
    int 21h 
    mov bl,al
    mov bh,0
    sub bl,30h
    
    lea dx,d    ;
    mov ah,9h   
    int 21h
   
    add cx,bx
    
    
    
    jmp bitir    
           
cIleBitir:
    lea dx,x1    ;
    mov ah,9h   
    int 21h    
    lea dx,d    ;
    mov ah,9h   
    int 21h
             
    mov ah,01   ;
    int 21h      
    mov cl,al
    mov ch,0 
    sub cl,30h
             
              
    lea dx,d    ;
    mov ah,9h   
    int 21h          
             
    lea dx,x2    ;
    mov ah,9h   
    int 21h  
    lea dx,d    ;
    mov ah,9h   
    int 21h  
    
    mov ah,01   ;
    int 21h 
    mov bl,al
    mov bh,0
    sub bl,30h
    
    lea dx,d    ;
    mov ah,9h   
    int 21h
   
    sub cx,bx
    
    
    jmp bitir 
    

bIleBitir:
    lea dx,x1    ;
    mov ah,9h   
    int 21h    
    lea dx,d    ;
    mov ah,9h   
    int 21h
             
    mov ah,01   ;
    int 21h      
    mov cl,al
    mov ch,0 
    sub cl,30h
             
              
    lea dx,d    ;
    mov ah,9h   
    int 21h          
             
    lea dx,x2    ;
    mov ah,9h   
    int 21h  
    lea dx,d    ;
    mov ah,9h   
    int 21h  
    
    mov ah,01   ;
    int 21h 
    mov bl,al
    mov bh,0
    sub bl,30h
    
    lea dx,d    ;
    mov ah,9h   
    int 21h
    
    mov ax,0
    mov ax,cx
    div bl  
    
    mov cx,0
    mov cx,ax
    
    
    jmp bitir    

pIleBitir:
    lea dx,x1    ;
    mov ah,9h   
    int 21h    
    lea dx,d    ;
    mov ah,9h   
    int 21h
             
    mov ah,01   ;
    int 21h      
    mov cl,al
    mov ch,0 
    sub cl,30h
             
              
    lea dx,d    ;
    mov ah,9h   
    int 21h          
             
    lea dx,x2    ;
    mov ah,9h   
    int 21h  
    lea dx,d    ;
    mov ah,9h   
    int 21h  
    
    mov ah,01   ;inputted number from the keyboard
    int 21h 
    mov bl,al
    mov bh,0
    sub bl,30h
    
    lea dx,d    ;
    mov ah,9h   
    int 21h
    
    mov ax,0
    mov ax,cx
    
    mul bx  
    mov cx,0
    mov cx,ax
    
    
    jmp bitir    
      
          
bitir:
lea dx,x3    ;
mov ah,9h   
int 21h

mov S,cx 



sonucuYaz:                       
    mov  si, offset numstr
    mov  ax, S
    call numToString 
    mov  ah, 9
    mov  dx, offset numstr
    int 21h     
    mov  ah, 9
    mov  dx, offset lbk
    int 21h     
    INC S             
                            

lea dx,x4    
mov ah,9h   
int 21h
lea dx,d    
mov ah,9h   
int 21h

mov ax,0
mov ah,01   
int 21h      
mov bl,al  

cmp bl,'d'
    jne qmi
    jmp bas         
         

qmi:
cmp bl,'q'
jne bitir2
jmp bitir2


                 
numToString proc 
      call dll 
      mov  bx, 10  
      mov  cx, 0   
    c1:       
      mov  dx, 0   
      div  bx      
      push dx      
      inc  cx      
      cmp  ax, 0   
      jne  c1   
    c2:  
      pop  dx        
      add  dl, 48  
      mov  [ si ], dl
      inc  si
      loop c2  
      ret
numToString endp   

proc dll                 
      mov  cx, 5
      mov  di, offset numstr
    d1:      
      mov  bl, '$'
      mov  [ di ], bl
      inc  di
      loop d1
      ret      
endp




bitir2:
ret                                      
