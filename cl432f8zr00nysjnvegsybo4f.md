## Write a program for a school grading system in C

During a peer learning day discussion amongst myself and my colleagues in the ALX Software Engineering (May 2022 cohort), we tasked ourselves with this project to help us understand the implementation of conditional statements in C programming.

The question was:

A school has approached you to develop a program in C that will help them determine the grades for their student based on their score in each examination. Below is a table of the ranges and respective grades

<table>
<thead>
<th>Range of scores</thd>
<th>Grade</th>
</thead>
<tbody>

<tr>
<td>80 - 100</td>
<td>A</td>
</tr>

<tr>
<td>70 - 79</td>
<td>B</td>
</tr>

<tr>
<td>65 - 69</td>
<td>C</td>
</tr>

<tr>
<td>60 - 64</td>
<td>D</td>
</tr>

<tr>
<td>50 - 59</td>
<td>E</td>
</tr>

<tr>
<td>Below 40</td>
<td>F</td>
</tr>
</tbody>
</table>

With just your basic knowledge in C, write a program that solves this problem for them:
a. using if statements
b. using switch statements

We met as a group to discuss conditional statements including `if` and `switch` to enable us solve this problem. Here is a link to the recorded session of our group discussion. You can watch it to understand the solution presented below in details.

%[https://youtu.be/VsLnwRIYNZE]

Here are the solutions.

## Using `if` statements to make a grading system
```
#include <stdio.h>

/**
  * main - solving our assignment
  * description - A program for school grading system
  * 80 - 100 == A
  * 70 - 79  == B
  * 65 - 69  == C
  * 60 - 64  == D
  * 50 - 59  == E
  * Below 50 == F
  * return 0
  */


int main(void) {
  int score;

  /* Tell your user to type their score */
  printf("What was your score:\n");
    
  /* Accept the user's input */
  scanf("%d", &score);

  /* check if the score is between 80 and 100 then print the 
   * grade if it is   
   */

  if (score >= 80 && score <= 100 )
  {
    printf("A");
  }
  /* check if the score is between 70 and 79 then print the 
   * grade if it is   
   */
   else if (score >= 70 && score <= 79 )
   {  
     printf("B");
   }  

  /* check if the score is between 65 and 69 then print the 
   * grade if it is   
   */
   else if (score >= 65 && score <= 69)
   {
     printf("C");
   }
  /* check if the score is between 60 and 64 then print the 
   * grade if it is   
   */

  else if (score >= 60 && score <=64)
  {
    printf("D");
  }
  /* check if the score is between 50 and 59 then print the 
   * grade if it is   
   */
  else if (score >= 50 && score <= 59)
    printf("E");

    /* check if the score is below 50 then print the 
   * grade if it is   
   */
  else if (score >= 0 && score <= 50)
  {
    printf("F");
  }

  else
  {
    printf("You entered an invalid score");
  }
  return 0;
}
```

## Using `switch` statements to make a grading system
```
#include <stdio.h>

/**
 * main - solving our assignment
 * description - A program for school grading system
 * 80 - 100 == A
 * 70 - 79  == B
 * 65 - 69  == C
 * 60 - 64  == D
 * 50 - 59  == E
 * Below 50 == F
 * return 0
 */

int main(void) {
  int score;

  /* Tell your user to type their score */
  printf("What was your score:\n");

  /* Accept the user's input */
  scanf("%d", &score);

  switch (score)
  {
    case 80 ... 100:
      printf("A \n");
      break;
    case 70 ... 79:
      printf("B \n");
      break;
    case 65 ... 69:
      printf("C \n");
      break;
    case 60 ... 64:
       printf("D \n");
       break;
    case 50 ... 59: 
       printf("E \n");
      break;
    case 0 ... 49:
       printf("F \n");
       break;
    default:
       printf("Invalid score");
       break;
}
  
  
  return 0;
}
```