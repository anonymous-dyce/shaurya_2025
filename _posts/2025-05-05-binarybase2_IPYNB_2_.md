---
layout: page
title: Binary Base 2 HW
toc: True
permalink: /binary_history/bb2hw
categories: ['CSP Classwork']
---

### Homework:

``` python
def decimal_to_binary(n):
    if n == 0:
        return "0"
    binary = ""
    while n > 0:
        binary = str(n % 2) + binary
        n = n // 2
    return binary

def binary_to_decimal(b):
    decimal = 0
    b = b[::-1]
    for i in range(len(b)):
        if b[i] == '1':
            decimal += 2 ** i
    return decimal

def add_binary(a, b):
    dec_a = binary_to_decimal(a)
    dec_b = binary_to_decimal(b)
    return decimal_to_binary(dec_a + dec_b)

def subtract_binary(a, b):
    dec_a = binary_to_decimal(a)
    dec_b = binary_to_decimal(b)
    result = dec_a - dec_b
    if result < 0:
        return "-" + decimal_to_binary(-result)
    return decimal_to_binary(result)

def and_binary(a, b):
    dec_a = binary_to_decimal(a)
    dec_b = binary_to_decimal(b)
    return decimal_to_binary(dec_a & dec_b)

def or_binary(a, b):
    dec_a = binary_to_decimal(a)
    dec_b = binary_to_decimal(b)
    return decimal_to_binary(dec_a | dec_b)

def xor_binary(a, b):
    dec_a = binary_to_decimal(a)
    dec_b = binary_to_decimal(b)
    return decimal_to_binary(dec_a ^ dec_b)

def not_binary(a):
    # NOT using 8-bit fixed width
    return ''.join('1' if bit == '0' else '0' for bit in a.zfill(8))

def calculator():
    print("Binary Calculator (No `bin()` used!)")
    print("1. Add\n2. Subtract\n3. AND\n4. OR\n5. XOR\n6. NOT\n7. Binary to Decimal\n8. Decimal to Binary")
    choice = input("Choose an option (1-8): ")

    if choice in ['1', '2', '3', '4', '5']:
        a = input("Enter first binary number: ")
        b = input("Enter second binary number: ")
        if choice == '1':
            print("Result:", add_binary(a, b))
        elif choice == '2':
            print("Result:", subtract_binary(a, b))
        elif choice == '3':
            print("Result:", and_binary(a, b))
        elif choice == '4':
            print("Result:", or_binary(a, b))
        elif choice == '5':
            print("Result:", xor_binary(a, b))
    elif choice == '6':
        a = input("Enter binary number: ")
        print("Result:", not_binary(a))
    elif choice == '7':
        a = input("Enter binary number: ")
        print("Decimal:", binary_to_decimal(a))
    elif choice == '8':
        a = int(input("Enter decimal number: "))
        print("Binary:", decimal_to_binary(a))
    else:
        print("Invalid choice.")

# Run the calculator
calculator()
```
