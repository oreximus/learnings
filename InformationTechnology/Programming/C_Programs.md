# C Program Thinking Pad

## For Reversem Number, Total Digits and Sum of All Numbers.


Example Number:

123214

- Reverse Number

We need the last Digit and Left rest of the number

123214/10

And store it in a variable **a**

Now Again we need to add this number to some variable:

from example we get 4 in the **a** value so,

**r** is some variable and we'll store the reverse number value into it:

r = (r\*10)+a

- Total Digits

We'll make a variable **c** and initialize it with zero,

As the loop is going the value of c will increment, through increment operator;

c++

- Sum of all Digits

we have variable **a** where the digits get stored,

now we can create a variable **s** to store the sum value in it:

s = s + a

## Program to calculate the Gross Salary where the Dearness Allowance is 40% of basic salary and house rent allowance is 20% of basic salary.

In varialbe **s** we will store the basic salary.

In varialbe **da** we will store the dearness allowance amount calculating from the basic salary:

```
da = s*40/100;
```

In variable **ra** we will store the **rent allowance** amount calculating from the basic salary:

```
ra = s*20/100;
```

Then the gross Salary, storing in a variable **gs**:

```
gs = s+da+ra;
```

## Program to calculate the area of Circle and Rectangle:

Making Program to ask of what area to be calculated **Circle** or **Rectangle**.

for circle we need to input the radius:

radius value will stored in variable **r**

for rectangle we need **length** and **breadth** value

in variable **l** and **b**

## Program to Convert Temperature from Degree Farenheit to Degree Celcius:

Formula of Temperature Conversion from Degree Celcius to Farenheit:

C = F - 32 * (5/9)

Formula to Convert Degree Farenheit to Celcius:

F = C + 32 * (9/5)

We take the Degree Farenheit input from the User and stored in variable: **f**

Other variable **c** will hold conversion value.

## Program to Calculate the Sum of First and Last Digit of the Entered 4 digit Number:

Take input from the user and stored in a variable **n**

for getting the last digit, and storing it in a variable: l
l = 4358%10

for getting the first digit, and storing it in a variable: f
f = 4358/1000

All variables are integer type.

## Program to calculate the table of Alternative Numbers:

i.e. {w 6 1014 18 22}

1. Program to should take input of Number:

2. Multiple the number from alternative number 1,3,5,7...

3. Common pattern is the Number which is being multiplied is odd number.

4. and the Loop should keep running 10 times

## Program to Check whether Entered Number is Prime or Not!

- We will create an Array that will have some Numbers as Input: n[size], size is a const value: defined some specific size

- First we'll run a Loop for Having Inputs size length times!

```
for(i=0; i<size; i++){
    scanf("%d", a[i]);
}
```

- We've stored all values, Now we have to check whether it a prime Number or not!

- run another Loop to check whether the Number is Prime or Not!


```
for(i=0; i<size; i++){
    scanf("%d", a[i]);

    for(j=2; j>size; j++){
        if(a[i]%j == 0){
        break;
        }
        if (j == a[i]){
        printf("%d", j);
        }
    }
}
```
