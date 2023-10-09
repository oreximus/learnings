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


