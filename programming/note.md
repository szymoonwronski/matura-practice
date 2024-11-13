# Matura - Programming - C++

- [Matura - Programming - C++](#matura---programming---c)
- [Base conversions](#base-conversions)
  - [Conversion algorithms](#conversion-algorithms)
    - [Convert positive number from any base to decimal](#convert-positive-number-from-any-base-to-decimal)
    - [Convert number from any base to decimal](#convert-number-from-any-base-to-decimal)
    - [Convert positive decimal number to any base](#convert-positive-decimal-number-to-any-base)
    - [Convert decimal number to any base](#convert-decimal-number-to-any-base)
  - [Changing a base used for input/output](#changing-a-base-used-for-inputoutput)
    - [Reading values in octal, decimal or hexadecimal](#reading-values-in-octal-decimal-or-hexadecimal)
    - [Printing values in octal, decimal or hexadecimal](#printing-values-in-octal-decimal-or-hexadecimal)
  - [Converting numbers using built-in functions](#converting-numbers-using-built-in-functions)
    - [Function `stoi()` - (string to int)](#function-stoi---string-to-int)
    - [Function `to_string()`](#function-to_string)
    - [Library `Bitset`](#library-bitset)
- [Must know algoritms](#must-know-algoritms)
  - [GCD - Greatest Common Divisor](#gcd---greatest-common-divisor)
  - [LCM - Least Common Multiple](#lcm---least-common-multiple)

# Base conversions

Only for bases smaller than or equal to 10 as only they use digits.

## Conversion algorithms

Once you understand them they are pretty easy.

### Convert positive number from any base to decimal

```cpp
int convertToBase10OnlyPositives(string num, int base) {
  int result = 0;

  for(char c : num) {
    result = result * base + c - '0';
  }

  return result;
}
```

### Convert number from any base to decimal

```cpp
int convertToBase10WithSign(string num, int base) {
  int result = 0, sign = 1, i = 0;

  if(num[0] == '-') {
    sign = -1;
    i = 1;
  }

  for(; i < num.size(); i++) {
    result = result * base + num[i] - '0';
  }

  return sign * result;
}
```

> [!TIP]
> There is a function that does the same for you and it's called [`stoi`](#function-stoi---string-to-int).

### Convert positive decimal number to any base

```cpp
string convertToAnyBaseOnlyPositives(int num, int base) {
  string result = "";

  while(num > 0) {
    char r = '0' + num % base;
    result = r + result;
    num /= base;
  }

  return result;
}
```

### Convert decimal number to any base

```cpp
string convertToAnyBaseWithSign(int num, int base) {
  string result = "", sign = "";

  if(num < 0) {
    sign = '-';
    num *= -1;
  }

  while(num > 0) {
    char r = '0' + num % base;
    result = r + result;
    num /= base;
  }

  return sign + result;
}
```

## Changing a base used for input/output

### Reading values in octal, decimal or hexadecimal

```cpp
int x, x2, y, z;
cin >> oct >> x; // octal
cin >> x2; // octal as well, base remains unchanged!
cin >> dec >> y; // decimal
cin >> hex >> z; // hexadecimal
```

All of those are stored as decimal values, they are just read using different bases.

> [!WARNING]
> Changing a base once changes it for all the future calls!

### Printing values in octal, decimal or hexadecimal

```cpp
int x = 12;
cout << oct << x; // 14
cout << x; // 14 as well, base remaing unchanged!
cout << dec << x; // 12
cout << hex << x; // C
```

The value of `x` never changes. It is only printed using different bases.

> [!NOTE]
> There is no similar way to use binary as a base in input/output. You need to convert it other way.

## Converting numbers using built-in functions

### Function `stoi()` - (string to int)

```cpp
string s = "123";
int x = stoi(s); // x = 123
```

Additionaly, you can specify the base of a number.

```cpp
string s = "123";
int x = stoi(s, 0, 4); // using base 4, then x = 27
```

### Function `to_string()`

Helpful when you need to change a base of a number.

```cpp
int x = 12;
string s = to_string(x); // s = "12"
```

### Library `Bitset`

```cpp
int x = 12;
string s = bitset<8>(x).to_string(); // s = "00001100"
```

> [!IMPORTANT]
> Remember to include `bitset` library.

# Must know algoritms

## GCD - Greatest Common Divisor

```cpp
int gcd(int a, int b) {
  return b == 0 ? a : gcd(b, a % b);
}
```

> [!TIP]
> There is a built-in function.

```cpp
int x = 12, y = 8;
int res = gcd(x, y); // res = 4
```

> [!IMPORTANT]
> Remember to include `numeric` library for C++17.  
> For C++14 use `algorithm` library with the function called `__gcd()`.

## LCM - Least Common Multiple

```cpp
int lcm(int a, int b) {
  return (a / gcd(a, b)) * b; // function gcd() as described above
}
```

> [!TIP]
> There is a built-in function.

```cpp
int x = 12, y = 8;
int res = lcm(x, y); // res = 24
```

> [!IMPORTANT]
> Remember to include `numeric` library for C++17.
