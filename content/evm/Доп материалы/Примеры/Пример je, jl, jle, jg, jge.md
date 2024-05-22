Конечно! Давайте рассмотрим примеры использования условных переходов `je`, `jl`, `jle`, `jg`, `jge` после команды сравнения [[cmp]]. Эти команды используются для выполнения условных переходов в зависимости от результатов сравнения.

### Подготовительный код
Прежде чем использовать условные переходы, давайте установим значения в регистрах и выполним сравнение:

```asm
section .data
msg_equal db "AX is equal to BX", 0
msg_less db "AX is less than BX", 0
msg_less_equal db "AX is less than or equal to BX", 0
msg_greater db "AX is greater than BX", 0
msg_greater_equal db "AX is greater than or equal to BX", 0

section .bss
section .text
global _start

_start:
    mov ax, 5     ; загрузить 5 в регистр AX
    mov bx, 3     ; загрузить 3 в регистр BX
    cmp ax, bx    ; сравнить AX с BX

    ; Примеры использования условных переходов
```

### Использование `je` (Jump if Equal)
Команда `je` выполняет переход, если операнды равны (ZF = 1).

```asm
    je equal_label

equal_label:
    ; Код выполняется, если AX == BX
    ; Например, вывести сообщение "AX is equal to BX"
    ; (здесь предполагается, что есть процедура для вывода строки)
    ; call print_string
    ; jmp end_program
```

### Использование `jl` (Jump if Less)
Команда `jl` выполняет переход, если первый операнд меньше второго (SF ≠ OF).

```asm
    jl less_label

less_label:
    ; Код выполняется, если AX < BX
    ; Например, вывести сообщение "AX is less than BX"
    ; call print_string
    ; jmp end_program
```

### Использование `jle` (Jump if Less or Equal)
Команда `jle` выполняет переход, если первый операнд меньше или равен второму (ZF = 1 или SF ≠ OF).

```asm
    jle less_equal_label

less_equal_label:
    ; Код выполняется, если AX <= BX
    ; Например, вывести сообщение "AX is less than or equal to BX"
    ; call print_string
    ; jmp end_program
```

### Использование `jg` (Jump if Greater)
Команда `jg` выполняет переход, если первый операнд больше второго (ZF = 0 и SF = OF).

```asm
    jg greater_label

greater_label:
    ; Код выполняется, если AX > BX
    ; Например, вывести сообщение "AX is greater than BX"
    ; call print_string
    ; jmp end_program
```

### Использование `jge` (Jump if Greater or Equal)
Команда `jge` выполняет переход, если первый операнд больше или равен второму (SF = OF).

```asm
    jge greater_equal_label

greater_equal_label:
    ; Код выполняется, если AX >= BX
    ; Например, вывести сообщение "AX is greater than or equal to BX"
    ; call print_string
    ; jmp end_program
```

### Полный пример с условными переходами
```asm
section .data
msg_equal db "AX is equal to BX", 0
msg_less db "AX is less than BX", 0
msg_less_equal db "AX is less than or equal to BX", 0
msg_greater db "AX is greater than BX", 0
msg_greater_equal db "AX is greater than or equal to BX", 0

section .bss

section .text
global _start

_start:
    mov ax, 5     ; загрузить 5 в регистр AX
    mov bx, 3     ; загрузить 3 в регистр BX
    cmp ax, bx    ; сравнить AX с BX

    je equal_label
    jl less_label
    jle less_equal_label
    jg greater_label
    jge greater_equal_label

equal_label:
    ; Код выполняется, если AX == BX
    ; Например, вывести сообщение "AX is equal to BX"
    call print_equal
    jmp end_program

less_label:
    ; Код выполняется, если AX < BX
    ; Например, вывести сообщение "AX is less than BX"
    call print_less
    jmp end_program

less_equal_label:
    ; Код выполняется, если AX <= BX
    ; Например, вывести сообщение "AX is less than or equal to BX"
    call print_less_equal
    jmp end_program

greater_label:
    ; Код выполняется, если AX > BX
    ; Например, вывести сообщение "AX is greater than BX"
    call print_greater
    jmp end_program

greater_equal_label:
    ; Код выполняется, если AX >= BX
    ; Например, вывести сообщение "AX is greater than or equal to BX"
    call print_greater_equal
    jmp end_program

print_equal:
    ; Ваша функция печати сообщения msg_equal
    mov edx, len_equal
    mov ecx, msg_equal
    call print_string
    ret

print_less:
    ; Ваша функция печати сообщения msg_less
    mov edx, len_less
    mov ecx, msg_less
    call print_string
    ret

print_less_equal:
    ; Ваша функция печати сообщения msg_less_equal
    mov edx, len_less_equal
    mov ecx, msg_less_equal
    call print_string
    ret

print_greater:
    ; Ваша функция печати сообщения msg_greater
    mov edx, len_greater
    mov ecx, msg_greater
    call print_string
    ret

print_greater_equal:
    ; Ваша функция печати сообщения msg_greater_equal
    mov edx, len_greater_equal
    mov ecx, msg_greater_equal
    call print_string
    ret

print_string:
    ; Функция печати строки (зависит от используемой платформы)
    ; В Linux можно использовать системный вызов write
    mov eax, 4          ; syscall number for sys_write
    mov ebx, 1          ; file descriptor 1 (stdout)
    int 0x80            ; make kernel call
    ret

end_program:
    mov eax, 1          ; syscall number for sys_exit
    xor ebx, ebx        ; exit code 0
    int 0x80            ; make kernel call
```

Этот пример демонстрирует использование различных условных переходов после команды `cmp`. Каждая метка обрабатывает соответствующее условие, и в каждой из них вызывается функция для печати соответствующего сообщения.

