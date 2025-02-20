#  Регистр EDX: Основы и Применение в Ассемблере

##  Введение

Регистр EDX (Extended Data Register) является одним из ключевых регистров общего назначения в архитектуре x86 и x86-64 процессоров Intel. Он часто используется вместе с другими регистрами для выполнения различных операций, включая арифметические и логические действия. В этой статье мы рассмотрим основные характеристики и применение регистра EDX в ассемблерном программировании.

##  Основы регистра EDX

Регистр EDX является 32-битным регистром, который представляет собой расширенную версию 16-битного регистра DX. Подобно регистру EAX, регистр DX делится на два 8-битных регистра: DH (старший байт) и DL (младший байт).

- **EDX (32 бита)**: Регистр данных общего назначения.
- **DX (16 бит)**: Нижняя половина регистра EDX.
- **DH (8 бит)**: Старший байт регистра DX.
- **DL (8 бит)**: Младший байт регистра DX.

##  Основные функции регистра EDX

1. **Расширенные арифметические операции**: Регистр EDX часто используется для хранения старшей части результата при умножении и делении.
   
2. **Взаимодействие с операндами**: EDX используется в сочетании с другими регистрами для выполнения операций с данными и адресации.
   
3. **Вызовы функций и передачи параметров**: В некоторых соглашениях о вызовах регистр EDX используется для передачи второго параметра функции.

##  Примеры использования регистра EDX

###  Расширенные арифметические операции

При умножении и делении регистр EDX используется для хранения старшей части результата.

```assembly
section .data
    num1 dd 123456
    num2 dd 654321

section .text
    global _start

_start:
    mov eax, [num1]  ; загрузить значение num1 в EAX
    mov ecx, [num2]  ; загрузить значение num2 в ECX
    mul ecx          ; умножить EAX на ECX, результат в EDX:EAX
    ; Теперь EDX содержит старшую часть результата, а EAX - младшую часть
```

###  Логические операции

```assembly
section .data
    value dd 0xFF00FF00

section .text
    global _start

_start:
    mov edx, [value]  ; загрузить значение value в EDX
    or edx, 0x0000FFFF  ; применить побитовое ИЛИ с маской
    ; Теперь EDX содержит 0xFF00FFFF
```

###  Вызовы функций

```assembly
section .text
    global _start

extern _printf

_start:
    mov eax, 42        ; первый параметр для printf
    mov edx, 84        ; второй параметр для printf
    call print_values  ; вызов функции для печати значений
    ; завершение программы

print_values:
    ; передача значений EAX и EDX в _printf
    push edx
    push eax
    push message
    call _printf
    add esp, 12
    ret

section .data
message db "Values: %d, %d", 0
```

##  Заключение

Регистр EDX играет важную роль в ассемблерном программировании, обеспечивая дополнительные возможности для работы с данными и выполнения расширенных арифметических операций. Знание особенностей и способов использования регистра EDX позволяет программистам более эффективно управлять данными и оптимизировать код.