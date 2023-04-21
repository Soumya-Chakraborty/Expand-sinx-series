# Write a C function to evaluate the series to 'n' significant digits sin(x)=x-(x/3!)+(x+/5!)-(x/7!) +......
#include <stdio.h>
#include <math.h>

// A function to calculate the factorial of a positive integer
int factorial (int n) {
  int i, fact = 1;
  for (i = 1; i <= n; i++) {
    fact = fact * i;
  }
  return fact;
}

// A function to evaluate the series sin(x) = x - x^3/3! + x^5/5! - x^7/7! + ...
double sin_series (double x, int n) {
  double sum = 0; // The variable to store the sum of the series
  int i, sign = 1; // The variables to control the loop and the sign of each term
  for (i = 1; i <= n; i += 2) { // Loop from 1 to n with step size of 2
    sum = sum + sign * pow (x, i) / factorial (i); // Add the current term to the sum
    sign = -sign; // Flip the sign for the next term
  }
  return sum; // Return the sum as the result
}

int main () {
  double x; // The variable to store the value of x in radians
  int n; // The variable to store the number of significant digits
  printf ("Enter the value of x in radians: "); // Prompt the user for input
  scanf ("%lf", &x); // Read the input and store it in x
  printf ("Enter the number of significant digits: "); // Prompt the user for input
  scanf ("%d", &n); // Read the input and store it in n
  printf ("The value of sin(%lf) using the series is %.*lf\n", x, n, sin_series (x, n)); // Print the result using the series function with n digits after decimal point
  printf ("The value of sin(%lf) using the library function is %.*lf\n", x, n, sin (x)); // Print the result using the library function with n digits after decimal point
  return 0; // Exit the program
}
