---
title: Множество операторов ветвления
---
В языке ассемблера для архитектуры ARM существует множество операторов ветвления, которые позволяют управлять потоком выполнения программы на основе различных условий. Вот основные операторы ветвления, используемые в ARM ассемблере:

1. **`b` (Branch):**
   Безусловный переход к указанной метке.

   ```assembly
   b target_label
   ```

2. **`bal` (Branch Always):**
   Всегда выполняет переход. Это синоним команды `b`.

   ```assembly
   bal target_label
   ```

3. **`bx` (Branch and Exchange):**
   Переход к адресу, указанному в регистре, с возможностью смены режима исполнения (Thumb или ARM).

   ```assembly
   bx r0
   ```

4. **`blx` (Branch with Link and Exchange):**
   Переход к подпрограмме с сохранением адреса возврата и возможностью смены режима исполнения.

   ```assembly
   blx r0
   ```

5. **`cbz` (Compare and Branch on Zero):**
   Сравнивает регистр с нулем и выполняет переход, если значение регистра равно нулю.

   ```assembly
   cbz r0, target_label
   ```

6. **`cbnz` (Compare and Branch on Non-Zero):**
   Сравнивает регистр с нулем и выполняет переход, если значение регистра не равно нулю.

   ```assembly
   cbnz r0, target_label
   ```

7. **`tbb` (Table Branch Byte):**
   Выполняет переход, используя значение таблицы байтов как смещение.

   ```assembly
   tbb [r0, r1]
   ```

8. **`tbh` (Table Branch Halfword):**
   Выполняет переход, используя значение таблицы полуслов как смещение.

   ```assembly
   tbh [r0, r1, lsl #1]
   ```

9. **Условные переходы на основе флагов процессора:**

   - **`beq` (Branch if Equal):** Переход, если результат предыдущей операции был равен нулю (Zero flag).
     ```assembly
     beq target_label
     ```

   - **`bne` (Branch if Not Equal):** Переход, если результат предыдущей операции не был равен нулю.
     ```assembly
     bne target_label
     ```

   - **`bcs` (Branch if Carry Set) или `bhs` (Branch if Higher or Same):** Переход, если установлен флаг переноса (Carry flag).
     ```assembly
     bcs target_label
     bhs target_label
     ```

   - **`bcc` (Branch if Carry Clear) или `blo` (Branch if Lower):** Переход, если флаг переноса не установлен.
     ```assembly
     bcc target_label
     blo target_label
     ```

   - **`bmi` (Branch if Minus):** Переход, если результат предыдущей операции был отрицательным (Negative flag).
     ```assembly
     bmi target_label
     ```

   - **`bpl` (Branch if Plus):** Переход, если результат предыдущей операции был положительным или нулевым.
     ```assembly
     bpl target_label
     ```

   - **`bvs` (Branch if Overflow Set):** Переход, если установлен флаг переполнения (Overflow flag).
     ```assembly
     bvs target_label
     ```

   - **`bvc` (Branch if Overflow Clear):** Переход, если флаг переполнения не установлен.
     ```assembly
     bvc target_label
     ```

   - **`bhi` (Branch if Higher):** Переход, если unsigned значение больше.
     ```assembly
     bhi target_label
     ```

   - **`bls` (Branch if Lower or Same):** Переход, если unsigned значение меньше или равно.
     ```assembly
     bls target_label
     ```

   - **`bge` (Branch if Greater or Equal):** Переход, если signed значение больше или равно.
     ```assembly
     bge target_label
     ```

   - **`blt` (Branch if Less Than):** Переход, если signed значение меньше.
     ```assembly
     blt target_label
     ```

   - **`bgt` (Branch if Greater Than):** Переход, если signed значение больше.
     ```assembly
     bgt target_label
     ```

   - **`ble` (Branch if Less or Equal):** Переход, если signed значение меньше или равно.
     ```assembly
     ble target_label
     ```

Эти команды ветвления позволяют создавать сложные логические конструкции и контролировать выполнение программ в ассемблере ARM. Понимание и умение использовать эти команды является ключевым для эффективного программирования на низком уровне.