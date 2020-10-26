---
layout: post
title:  "A minimal Bootloader"
date:   2020-08-15 02:30:00
categories: os
---

Below is the full code of our Bootloader.

```
org 0x7c00             ; Location of bootloader as per BIOS
bits 16                ; 16 bit mode
start: jmp boot        ; What to do at start - jump to boot function
; Assembly do not have functions, for simplicity, we will call the blocks as functions

msg db "Hi High", 0ah, 0dh, 0h 
; msg shows output on screen 
; db prints the message in dbl quotes
boot:
	cli            ; Clear Interrupts
	cld            ; Clear direction flag
	hlt            ; Halt
  
times 510 - ($-$$) db 0     ; fill the rest of binary boot space with zeroes

dw 0xAA55                   ; The magic number
```
save it in a file named boot.asm

Compile this with ```nasm -f boot.asm -0 boot.bin```

Run in QEMU ```qemu-system-i386 -fda boot.bin```
