# coal-lab
codes

Write  a  program  to  make  macro  to  calculate  the  product  of  two  numbers.  The  program  will continuously ask user to enter two numbers from user and find their product unless user enters both numbers zero.

.model small

.data
s db 10,13,"$" 
pro db 0 
n1 db ?
n2 db ? 
str db 10,13,"Product=$"  
str1 db 10,13,"******** END ********$"

.code    
mov ax,@data
mov ds,ax 


product MACRO p1,p2 


   
mov al,p1
mov bl,p2

mul bl

mov pro,al 

ENDM

mov cx,100 

L1:

mov ah,01
int 21h

sub al,48 
mov n1,al

mov ah,01
int 21h

sub al,48 
mov n2,al

cmp n1,0
JE equal 
jmp notZero


equal: 
cmp n2,0
JE E 

notZero:
product n1,n2

lea dx,str
mov ah,09
int 21h

mov dl,pro
add dl,48
mov ah,02
int 21h 

lea dx,s
mov ah,09
int 21h



loop L1  

E:   
lea dx,str1
mov ah,09
int 21h

Write a program to make macro for taking input of 5 numbers and printing their sum. Call the macro 5 times using the loop and each time change one value and keep rest for values same.

.model small
.data   
a db ?
.code
mov ax,@data
mov ds,ax  

sum MACRO  d
mov al,01
int 21h 
sub al,48
add bl,al

ENDM
sum 2,2
mov dl,10
mov ah,02
int 21h
mov dl,13
mov ah,02
int 21h
sum 4,2
mov dl,10
mov ah,02
int 21h
mov dl,13
mov ah,02
int 21h
mov dl,a
mov ah,02
int 21h

 l1:
 sum cl 
 loop l1
 ENDM

Write  a  program  to  print  the  triangle  pattern.  Use  loops  to  print  pattern  and  print  code  should  be written as macro. Call the macro repeatedly to print the pattern.


.model small

.data
str db " $"
str1 db "*$"
s db 1

.code
mov ax,@data
mov ds,ax




star MACRO

lea dx,str1
mov ah,09
int 21h

ENDM


mov cl,5

Outer:
mov bl,cl




L2:
star

loop L2

add s,1

mov dl,10
mov ah,02
int 21h

mov dl,13
mov ah,02
int 21h

mov cl,bl


Write  a  program  to  print  the  triangle  pattern.  Use  loops  to  print  pattern  and  print  code  should  be written as macro. Call the macro repeatedly to print the triangle.

.model small

.data 
str db " $"
str1 db "*$" 
s db 1

.code    
mov ax,@data
mov ds,ax

space MACRO 
    
lea dx,str
mov ah,09
int 21h

ENDM 


star MACRO 
    
lea dx,str1
mov ah,09
int 21h

ENDM 


mov cl,5

Outer:
mov bl,cl


L1:
space

loop L1 

mov cl,s

L2:
star 

loop L2

add s,2 

mov dl,10
mov ah,02
int 21h

mov dl,13
mov ah,02
int 21h         
         
mov cl,bl


loop Outer


Write an assembly code that arrange the numbers in array in ascending order using procedure.

.model small
.data       
arr db 9,2,1,4,8,5,7
str db "after sorting","$" 
temp db 0
.code                  
mov ax,@data
mov ds,ax

call sort

jmp end

sort proc
    
mov si,0
mov cx,7

outer:  
mov si,0
mov bx,cx
mov cx,7

inner:
mov al,[arr+si]
cmp al,[arr+si+1]
jg swap     
jmp incr

swap:  
mov dl,temp
mov dl,[arr+si+1]
mov [arr+si+1],al
mov [arr+si],dl  

incr:  
inc si
loop inner

mov cx,bx
loop outer

ret
sort endp  

end:
  lea dx,str
  mov ah,09
  int 21h
  
  mov cx,7
  mov si,0

l:    

mov dl,10
mov ah,02
int 21h
mov dl,13
mov ah,02
int 21h

mov dl,[arr+si]
add dl,48
mov ah,02
int 21h

inc si
loop l


Write an assembly language program using the Loop instruction to print following pattern by using procedure.

.model small
.data 

num db 1 
spc db " ","$"
nxt db 10,13,"$"
.code
mov ax,@data
mov ds,ax

call display

jmp end

display proc
    
mov cl,5

l1:
mov bl,cl
mov cl,5 
mov num,1

  l2: 
  
  mov dl,num  
  mov ah,02
  int 21h
  inc num  
  
    lea dx,spc
    mov ah,09
    int 21h
  loop l2:

lea dx,nxt
mov ah,09
int 21h

mov cl,bl
inc bl
loop l1

ret
display endp  

end:


Swapping Code:

.model small
.data
  num1 db 5
  num2 db 2    
  temp db 0
.code
  mov ax , @data 
  mov ds , ax
 
call swap 

jmp end 

swap proc 

  mov bl , num1 
  mov cl , num2   

  mov num2 , bl 
  mov num1 , cl  

  
ret
swap endp 

end:
    
  mov dl,num1 
  add dl,48    
  mov ah , 02  
  int 21h   
  
  mov al,num2  
  add al,48
  mov ah , 02  
  int 21h  


Taking input and then reading 
 
.model small .data
v1 db ? 
.code 
      
mov cx,5     
mov si,0 
  L1:  
    mov ah,01 
    int 21h
    mov [v1+si],al
    sub [v1+si],48 
    inc si     
    loop L1 
     
    
 
    mov ah,02
    mov dl,10d     
    int 21h 
    mov dl,13d 
    
int 21h    
      
    mov cx,5
    mov si,0 
  L2:  
    mov dl,[v1+si]
    add dl,48   
    mov ah,02 
    int 21h 
    inc si    
   loop L1 


Reverse display 
 
.model small .data 
v1 db ? 
     
.code 
 
mov cx,5
mov si,0   
L1:  
mov ah,01     
int 21h     
mov [v1+si],al     
sub [v1+si],48 
     
inc si     
loop L1
     
 
mov ah,02     
mov dl,10d 
int 21h 
mov dl,13d 
int 21h    
      
mov cx,5     
mov si,4 
  L2:  
    mov dl,[v1+si]
    add dl,48 
    mov ah,02 
    int 21h 
     
    dec si     
    loop L2 




Finding Max 
 
 
 
 
.model small .data    
 num1 db ?   
  max db ? 
     
.code     
mov ax,@data     
mov ds,ax 
     
mov cx,10     
mov si,0  
     
  
  L1: 
     
    mov ah,01 
    int 21h     
mov [num1+si],al     
sub [num1+si],48 
     
inc si 
loop L1 
       
       
mov al,[num1+0]
mov max,al 
     
mov si,0     
mov cx,10   
       l2: 
    cmp [num1+si],al 
    jbe e 
     
mov al,[num1+si]     
mov max,al 
     
  e:     
inc si     
loop l2   




Finding Min 
 
 
 
.model small .data    
 num1 db ?     
min db ? 
     
.code     
mov ax,@data     
mov ds,ax 
     
mov cx,10     
mov si,0  
     
    L1: 
     
    mov ah,01 
    int 21h 
    mov [num1+si],al 
    sub [num1+si],48 
     
    inc si 
    loop L1 
       
       
mov al,[num1+0]     
mov min,al 
     
mov si,0     
mov cx,10   
       l2: 
    cmp [num1+si],al 
    jae e 
     
    mov al,[num1+si] 
    mov min,al 
     
  e:
    inc si 
    loop l2   
      
