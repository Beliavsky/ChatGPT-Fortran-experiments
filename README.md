# ChatGPT-Fortran-experiments
Random experiments with ChatGPT to generate Fortran code. See also https://github.com/Beliavsky/Fortran-with-ChatGPT and https://github.com/Beliavsky/Optimization-Codes-by-ChatGPT

---
**Translate pseudocode to Fortran:**

```
for name in ["bob", "cathy", "dennis"]
   print "hello" + name
next
```

**ChatGPT-4 answer**<br>
In Fortran, strings can be managed using character arrays. However, there's no direct equivalent to a Python-style list of strings, so we have to define an array of fixed-length character strings. 

Here's a Fortran translation for your pseudocode:

```Fortran
program greeting
    implicit none
    character(len=6), dimension(3) :: names = [character(len=6) :: "bob", "cathy", "dennis"]
    integer :: i

    do i = 1, size(names)
        print*, 'hello ', trim(names(i))
    end do

end program greeting
```

In this program, `names` is an array of strings (represented as `character(len=6)` items), and each item is initialized with one of the names. The `do` loop iterates over each item in the array, and the `print*` statement prints out a greeting for each name. The `trim` function is used to remove trailing whitespace from each name.

Please note that in Fortran, strings (character variables) must have a fixed length which is set when the variable is declared. Here I have assumed a maximum length of 6 characters for the names. If you have names that are longer than this, you would need to increase the `len` value in the declaration of `names`.

---

**Translate to Fortran:**

```
f(x) = x^2
n = 10^6
fsum = 0
do i=1,n
   fsum = fsum + f(rand())
print "integral is", fsum/n
```

**ChatGPT-4 answer**

Your pseudocode appears to be implementing a Monte Carlo integration over the function f(x) = x^2 from 0 to 1. Here is the Fortran code that corresponds to your pseudocode:

```Fortran
program monte_carlo_integration
  implicit none
  integer, parameter :: n = 10**6
  real :: fsum, f, rand
  integer :: i

  ! Initialize seed for random number generator
  call random_seed()

  fsum = 0.0
  do i = 1, n
    call random_number(rand)
    fsum = fsum + f(rand)
  end do

  print *, 'Integral is ', fsum/n

contains

  real function f(x)
    real, intent(in) :: x
    f = x**2
  end function f

end program monte_carlo_integration
```

This code first initializes the random number generator using `call random_seed()`. Then it calculates the sum of f(x) for `n` random values of `x`, where `f(x) = x^2`. The final estimate for the integral is then `fsum/n`.

Please note that this is a Monte Carlo estimation, so the result can vary a bit between runs due to the random number generation. The larger the value of `n`, the more accurate the estimate will be, as per the Law of Large Numbers.

---

gfortran says

main.f90:20:17:

   20 |   real function f(x)
      |                 1
Error: Procedure ‘f’ at (1) has an explicit interface from a previous declaration
main.f90:21:25:

   21 |     real, intent(in) :: x
      |                         1
Error: Unexpected data declaration statement in CONTAINS section at (1)
main.f90:22:12:

   22 |     f = x**2
      |            1
Error: Unexpected assignment statement in CONTAINS section at (1)
main.f90:23:5:

   23 |   end function f
      |     1
Error: Expecting END PROGRAM statement at (1)

**ChatGPT-4 answer**<br>

I apologize for the confusion. There is a naming conflict because we're using "f" for the function as well as a variable. Let's correct that and also remove the declaration of `rand`, since `random_number` automatically declares it as a real. 

Here's the corrected code:

```Fortran
program monte_carlo_integration
  implicit none
  integer, parameter :: n = 10**6
  real :: sum_val, rand_val
  integer :: i

  ! Initialize seed for random number generator
  call random_seed()

  sum_val = 0.0
  do i = 1, n
    call random_number(rand_val)
    sum_val = sum_val + f(rand_val)
  end do

  print *, 'Integral is ', sum_val/real(n)

contains

  real function f(x)
    real, intent(in) :: x
    f = x**2
  end function f

end program monte_carlo_integration
```

This corrected code should work correctly in Fortran now.

**Note:** the code compiles and runs, with sample output `Integral is   0.332790285`.    



