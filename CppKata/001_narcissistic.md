# Does my number look big in this?
***
#### 2020.03.14

### Description:
A Narcissistic Number is a number which is the sum of its own digits, each raised to the power of the number
of digits in a given base. In this Kata, we will restrict ourselves to decimal (base 10).

For example, take 153 (3 digits):
```
    1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153
```
and 1634 (4 digits):
```
    1^4 + 6^4 + 3^4 + 4^4 = 1 + 1296 + 81 + 256 = 1634
```

### The Challenge:

Your code must return true or false depending upon whether the given number is a Narcissistic number in base 10.

Error checking for text strings or other invalid inputs is not required, only valid integers will be passed into the function.

### Test Cases:
```c++
#include <ctime>
#include <cstdlib>

using namespace std;

Describe(Narcissistic_function)
{
  It(small_numbers)
  {
    Assert::That(narcissistic(1), Equals(true));
    Assert::That(narcissistic(5), Equals(true));
    Assert::That(narcissistic(7), Equals(true));
  }
  It(larger_numbers)
  {
    Assert::That(narcissistic(153), Equals(true));
    Assert::That(narcissistic(370), Equals(true));
    Assert::That(narcissistic(371), Equals(true));
    Assert::That(narcissistic(1634), Equals(true));

  }
  It(randomized_test_1)
  {
    srand(time(NULL));
    for (int i = 0; i < 10; i++) {
      int num = (rand() % 5 + 5) * 60000 + (rand() % 99 + 1);
      Assert::That(narcissistic(num), Equals(false));
    }
  }
  It(randomized_test_2)
  {
    vector<int> bignums = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 153, 370, 371, 407, 1634, 8208, 9474, 54748, 92727, 93084, 548834, 1741725,
                                4210818, 9800817, 9926315, 24678050, 24678051 };
    for (int b : bignums)
      if (rand() % 11 > 5)
        Assert::That(narcissistic(b), Equals(true));
      else {
        int num = (rand() % 5 + 5) * 900000 + (rand() % 99 + 1);
        Assert::That(narcissistic(num), Equals(false));
      }
  }
};
```

### My Solutions
```c++
#include<math.h>
int steal(int num,int pos)
  {
  if(num==0)
  return 0;
  return pow(num%10,pos)+steal(num/10,pos);
  }
bool narcissistic( int value ){
  int i=0,temp=value;
  while(value>0){
  value=value/10;
  i++;
  }
  if (temp==steal(temp,i))
  return 1;
  else
  return 0;
}
```

### Best Practices
```c++
bool narcissistic(int value)
{
    int i = log10(value) + 1; //get the number of digits in "number"
  
    for (int n = value; n; n /= 10)
        value -= pow(n%10, i);
  
    return 0 == value;
}
