# printf vs scanf in C Programming

`printf` and `scanf` are the two workhorse I/O functions in C, and they're essentially opposites: one sends data out, the other brings data in.

## printf — output

Sends formatted data **from your program to the screen**.

```c
int age = 25;
printf("My age is %d\n", age);
```

- You pass **values directly** (not addresses).
- Uses format specifiers (`%d`, `%f`, `%s`, `%c`, ...) to convert data into readable text.
- Returns the number of characters printed.

## scanf — input

Reads formatted data **from the keyboard into your program's variables**.

```c
int age;
scanf("%d", &age);   // note the &
```

- You pass the **address** of each variable (`&age`), except for strings/char arrays, where the array name already *is* an address.
- Returns the number of items successfully read — worth checking, since bad input (like typing letters for `%d`) leaves the variable unset.

## Side by side

| | `printf` | `scanf` |
|---|---|---|
| Direction | Program → screen | Keyboard → program |
| Header | `stdio.h` | `stdio.h` |
| Needs `&`? | No | Yes (except strings) |
| Common bug | Mismatched specifier vs. argument type | Forgetting `&`, or leftover newline in the buffer after reading a number |

## Common format specifiers

| Specifier | Type |
|---|---|
| `%d` | int |
| `%f` | float (printf) |
| `%lf` | double (scanf) |
| `%c` | char |
| `%s` | string |
| `%u` | unsigned int |
| `%ld` | long |

## A quick example using both

```c
#include <stdio.h>

int main(void) {
    int n;
    printf("Enter a number: ");      // output
    scanf("%d", &n);                 // input
    printf("You entered: %d\n", n);  // output
    return 0;
}
```

## Practical tips

- `scanf("%d", ...)` leaves the newline character in the input buffer, which can trip up a `getchar()` or `scanf("%c", ...)` called right after it — a very common beginner bug. Fix it with a leading space: `scanf(" %c", &ch);`
- If you're reading full lines (especially strings), `fgets` is generally safer than `scanf("%s", ...)` since it won't overflow your buffer.
- Always check `scanf`'s return value (the number of items successfully matched) before trusting the variables it filled in.
