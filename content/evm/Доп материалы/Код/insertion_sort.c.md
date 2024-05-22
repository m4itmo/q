void InsertionSort(int *array_ptr, int n) {
    __asm__(
            "mov %[array_ptr], %%rdi;"
            "mov $1, %%ecx;"
            "cmp %[N], %%ecx;"
            "jge exit;"
            "main_loop_start:;"
            "mov (%%rdi, %%rcx, 4), %%eax;"
            "mov %%ecx, %%edx;"
            "dec %%edx;"
            "sub_loop:;"
            "mov (%%rdi, %%rdx, 4), %%ebx;"
            "cmp %%ebx, %%eax;"
            "jge sub_loop_exit;"
            "mov %%ebx, (%%rdi, %%rcx, 4);"
            "mov %%rdx, %%rcx;"
            "dec %%rdx;"
            "cmp $-1, %%rdx;"
            "jge sub_loop;"
            "sub_loop_exit:;"
            "lea 1(%%rdx), %%rdx;"
            "mov %%eax, (%%rdi, %%rdx, 4);"
            "inc %%ecx;"
            "cmp %[N], %%ecx;"
            "jl main_loop_start;"
            "end_sort:;"
            :
            : [array_ptr] "m"(array_ptr), [N] "r"(n)
    : "rax", "rbx", "rcx", "rdx", "rdi"
    );
}