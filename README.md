# ChatGPT-Fortran-experiments
random experiments with ChatGPT to generate Fortran code

**Translate pseudocode to Fortran:**

```
for name in ["bob", "cathy", "dennis"]
   print "hello" + name
next
```

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
