# SDCC Keyboard MSX ROM Functions Library (object type)

Author: mvac7

Architecture: MSX

Programming language: C

Format: .rel (SDCC object file)
 
mail: mvac7303b@gmail.com




## 1. Introduction

This project is an Open Source library with basic functions for reading the 
keyboard of MSX computers.

It uses the functions from the MSX BIOS, so it is designed to create 
applications in ROM format.
  
Use them for developing MSX applications using Small Device C Compiler (SDCC).

Includes an application for test and learning purposes.



## 2. Acknowledgments
  
Thanks for Info & help, to:

* Avelino Herrera > http://msx.atlantes.org/index_es.html
* Nerlaska > http://albertodehoyonebot.blogspot.com.es
* Fubu > http://www.gamerachan.org/fubu/
* Marq/Lieves!Tuore > http://www.kameli.net/lt/
* Sapphire/Z80ST > http://z80st.auic.es/
* Pentacour > http://pentacour.com/
* JamQue/TPM > http://www.thepetsmode.com/
* Andrear > http://andrear.altervista.org/home/msxsoftware.php
* Konamiman > https://www.konamiman.com
* MSX Assembly Page > http://map.grauw.nl/resources/msxbios.php
* Portar MSX Tech Doc > http://nocash.emubase.de/portar.htm
* MSX Resource Center > http://www.msx.org/
* Karoshi MSX Community > http://karoshi.auic.es/
* BlueMSX >> http://www.bluemsx.com/
* OpenMSX >> http://openmsx.sourceforge.net/
* Meisei  >> ?



## 3. Requirements

* Small Device C Compiler (SDCC) v3.6 http://sdcc.sourceforge.net/
* Hex2bin v2.2 http://hex2bin.sourceforge.net/ 



## 4. Functions

* void KillBuffer() - Clear keyboard buffer.
* char INKEY() - One character input (waiting) and return its code.
* char GetKeyMatrix(line) - Returns the value of the specified line from the keyboard matrix.



## 5. Keyboard Matrix

  Info by MSX Assembly Page 
  http://map.grauw.nl/articles/keymatrix.php
  
  
### 5.1 International
```  
Row  7      6      5      4      3      2      1      0    <-- bit
-----------------------------------------------------------
  0  7      6      5      4      3      2      1      0  
  1  ;      ]      [      \      =      -      9      8  
  2  B      A      acent  /      .      ,      `      '  
  3  J      I      H      G      F      E      D      C
  4  R      Q      P      O      N      M      L      K
  5  Z      Y      X      W      V      U      T      S
  6  F3     F2     F1     CODE   CAPS   GRAPH  CTRL   SHIFT
  7  RETURN SELECT BS     STOP   TAB    ESC    F5     F4
  8  Right  Down   Up     Left   DEL    INS    HOME   SPACE
```


### 5.2 Numeric pad
```
Row  7      6      5      4      3      2      1      0    <-- bit
----------------------------------------------------------- 
  9  4      3      2      1      0      /      +      *
 10  .      ,      -      9      8      7      6      5
```

 
## 6. A bit of code
 
This code contains the basis for controlling any key with pressure control.

You can add it to your program and adapt it with the keyboard rows and keys that 
your program uses.

Uncomment the lines of the keys you need and add the code to be executed, after 
setting the pressure control variable to true.

Example:
```
    if (!(keyPressed&Bit5)) {Row6pressed=true;KonamisPause();}; // [F1]
    if (!(keyPressed&Bit6)) 
    {
        Row6pressed=true;
        score++;
        ShowValue(score);
    }; // [F2]
```


The code:
```
#include "../include/keyboard.h"


// boolean
#ifndef _BOOLEAN
#define _BOOLEAN
  typedef enum {false = 0, true = 1} boolean;
#endif


#define  HALT __asm halt __endasm

 

// define in golbal variables: 
boolean Row0pressed;
boolean Row1pressed;
boolean Row2pressed;
boolean Row3pressed;  
boolean Row4pressed;
boolean Row5pressed;
boolean Row6pressed;
boolean Row7pressed;
boolean Row8pressed;


void main(void) 
{
  Row0pressed=false;
  Row1pressed=false;
  Row2pressed=false;
  Row3pressed=false;  
  Row4pressed=false;
  Row5pressed=false;
  Row6pressed=false;
  Row7pressed=false;
  Row8pressed=false;

  
  while(isOut==0)
  {
    HALT;
    
    
    
    // Keyboard row 0
    keyPressed = GetKeyMatrix(0);
    if (keyPressed!=0xFF)
    {
      if(Row0pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row0pressed=true;}; // [0]
        //if (!(keyPressed&Bit1)) {Row0pressed=true;}; // [1] 
        //if (!(keyPressed&Bit2)) {Row0pressed=true;}; // [2]
        //if (!(keyPressed&Bit3)) {Row0pressed=true;}; // [3] 
        //if (!(keyPressed&Bit4)) {Row0pressed=true;}; // [4]
        //if (!(keyPressed&Bit5)) {Row0pressed=true;}; // [5]
        //if (!(keyPressed&Bit6)) {Row0pressed=true;}; // [6]
        //if (!(keyPressed&Bit7)) {Row0pressed=true;}; // [7]
      }      
    }else Row0pressed=false;
  
    // Keyboard row 1 
    keyPressed = GetKeyMatrix(1);
    if (keyPressed!=0xFF)
    {
      if(Row1pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row1pressed=true;}; // [8]
        //if (!(keyPressed&Bit1)) {Row1pressed=true;}; // [9] 
        //if (!(keyPressed&Bit2)) {Row1pressed=true;}; // [-]
        //if (!(keyPressed&Bit3)) {Row1pressed=true;}; // [=] 
        //if (!(keyPressed&Bit4)) {Row1pressed=true;}; // [\]
        //if (!(keyPressed&Bit5)) {Row1pressed=true;}; // [[]
        //if (!(keyPressed&Bit6)) {Row1pressed=true;}; // []]
        //if (!(keyPressed&Bit7)) {Row1pressed=true;}; // [;]
      }      
    }else Row1pressed=false;
    
    
    // Keyboard row 2
    keyPressed = GetKeyMatrix(2);
    if (keyPressed!=0xFF)
    {
      if(Row2pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row2pressed=true;}; // [']
        //if (!(keyPressed&Bit1)) {Row2pressed=true;}; // [&] 
        //if (!(keyPressed&Bit2)) {Row2pressed=true;}; // [,]
        //if (!(keyPressed&Bit3)) {Row2pressed=true;}; // [.] 
        //if (!(keyPressed&Bit4)) {Row2pressed=true;}; // [/]
        //if (!(keyPressed&Bit5)) {Row2pressed=true;}; // [Dead key]
        //if (!(keyPressed&Bit6)) {Row2pressed=true;}; // [A]
        //if (!(keyPressed&Bit7)) {Row2pressed=true;}; // [B]
      }      
    }else Row2pressed=false;
    
    
    // Keyboard row 3
    keyPressed = GetKeyMatrix(3);
    if (keyPressed!=0xFF)
    {
      if(Row3pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row3pressed=true;}; // [C]
        //if (!(keyPressed&Bit1)) {Row3pressed=true;}; // [D]
        //if (!(keyPressed&Bit2)) {Row3pressed=true;}; // [E]
        //if (!(keyPressed&Bit3)) {Row3pressed=true;}; // [F]
        //if (!(keyPressed&Bit4)) {Row3pressed=true;}; // [G]
        //if (!(keyPressed&Bit5)) {Row3pressed=true;}; // [H]
        //if (!(keyPressed&Bit6)) {Row3pressed=true;}; // [I]
        //if (!(keyPressed&Bit7)) {Row3pressed=true;}; // [J]
      }      
    }else Row3pressed=false;
    
    
    // Keyboard row 4
    keyPressed = GetKeyMatrix(4);
    if (keyPressed!=0xFF)
    {
      if(Row4pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row4pressed=true;}; // [K]
        //if (!(keyPressed&Bit1)) {Row4pressed=true;}; // [L]
        //if (!(keyPressed&Bit2)) {Row4pressed=true;}; // [M]
        //if (!(keyPressed&Bit3)) {Row4pressed=true;}; // [N]
        //if (!(keyPressed&Bit4)) {Row4pressed=true;}; // [O]
        //if (!(keyPressed&Bit5)) {Row4pressed=true;}; // [P]
        //if (!(keyPressed&Bit6)) {Row4pressed=true;}; // [Q]
        //if (!(keyPressed&Bit7)) {Row4pressed=true;}; // [R]
      }      
    }else Row4pressed=false;    
   
   
    
    // Keyboard row 5
    keyPressed = GetKeyMatrix(5);
    if (keyPressed!=0xFF)
    {
      if(Row5pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row5pressed=true;}; // [S]
        //if (!(keyPressed&Bit1)) {Row5pressed=true;}; // [T]
        //if (!(keyPressed&Bit2)) {Row5pressed=true;}; // [U]
        //if (!(keyPressed&Bit3)) {Row5pressed=true;}; // [V]
        //if (!(keyPressed&Bit4)) {Row5pressed=true;}; // [W]
        //if (!(keyPressed&Bit5)) {Row5pressed=true;}; // [X]
        //if (!(keyPressed&Bit6)) {Row5pressed=true;}; // [Y]
        //if (!(keyPressed&Bit7)) {Row5pressed=true;}; // [Z]
      }      
    }else Row5pressed=false;
    
    
    // Keyboard row 6
    keyPressed = GetKeyMatrix(6);
    if (keyPressed!=0xFF)
    {
      if(Row6pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row6pressed=true;}; // [SHIFT]
        //if (!(keyPressed&Bit1)) {Row6pressed=true;}; // [CTRL]
        //if (!(keyPressed&Bit2)) {Row6pressed=true;}; // [GRAPH]
        //if (!(keyPressed&Bit3)) {Row6pressed=true;}; // [CAPS]
        //if (!(keyPressed&Bit4)) {Row6pressed=true;}; // [CODE]
        //if (!(keyPressed&Bit5)) {Row6pressed=true;}; // [F1]
        //if (!(keyPressed&Bit6)) {Row6pressed=true;}; // [F2]
        //if (!(keyPressed&Bit7)) {Row6pressed=true;}; // [F3]
      }      
    }else Row6pressed=false;
    
    
    // Keyboard row 7
    keyPressed = GetKeyMatrix(7);
    if (keyPressed!=0xFF)
    {
      if(Row7pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row7pressed=true;}; // [F4]
        //if (!(keyPressed&Bit1)) {Row7pressed=true;}; // [F5]
        //if (!(keyPressed&Bit2)) {Row7pressed=true;}; // [ESC]
        //if (!(keyPressed&Bit3)) {Row7pressed=true;}; // [TAB]
        //if (!(keyPressed&Bit4)) {Row7pressed=true;}; // [STOP]
        //if (!(keyPressed&Bit5)) {Row7pressed=true;}; // [BS]
        //if (!(keyPressed&Bit6)) {Row7pressed=true;}; // [SELECT]
        //if (!(keyPressed&Bit7)) {Row7pressed=true;}; // [RETURN]
      }      
    }else Row7pressed=false;
    
    
    // Keyboard row 8
    keyPressed = GetKeyMatrix(8);
    if (keyPressed!=0xFF)
    {
      if(Row8pressed==false)
      {
        //if (!(keyPressed&Bit0)) {Row8pressed=true;}; // [SPACE]
        //if (!(keyPressed&Bit1)) {Row8pressed=true;}; // [HOME]
        //if (!(keyPressed&Bit2)) {Row8pressed=true;}; // [INS]
        //if (!(keyPressed&Bit3)) {Row8pressed=true;}; // [DEL]
        //if (!(keyPressed&Bit4)) {Row8pressed=true;}; // [LEFT]
        //if (!(keyPressed&Bit5)) {Row8pressed=true;}; // [UP]
        //if (!(keyPressed&Bit6)) {Row8pressed=true;}; // [DOWN]
        //if (!(keyPressed&Bit7)) {Row8pressed=true;}; // [RIGHT]
      }      
    }else Row8pressed=false;



  } //END while



}
```