BASIC CALCULATOR IN C++

#include<iostream>
using namespace std;
int main(){
    char op;
    double num1 , num2;
    cout<<"enter two numbers: ";
    cin>>num1>>num2;
    cout<<"enter operator(+,-,*,/): ";
    cin>>op;
    switch(op){
        case'+': cout<<num1+num2;
        break;
        case'-': cout<<num1-num2;
        break;
        case'*': cout<<num1*num2;
        break;
        case'/': 
        if (num2!=0){
            cout<<num1/num2;
        }
        else{
            cout<<"cannot divide";
        }
        break;
        default:
        cout<<"invalid";
    }
    return 0;
    
}

----------------------------------------------------------------------------------------------------------------------------------------------------------------------
LEX PROGRAM
1. COUNT WORDS
/lex program to count number of words/
%{ 
#include<stdio.h> 
#include<string.h> 
int i = 0; 
%} 
  
/* Rules Section*/
%% 
([a-zA-Z0-9])*    {i++;} /* Rule for counting  
                          number of words*/
  
"\n" {printf("%d\n", i); i = 0;} 
%% 
  
int yywrap(void){} 
  
int main() 
{    
    // The function that starts the analysis 
    yylex(); 
  
    return 0; 
}

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
2.LEX- POS NEG

/* Lex program to Identify and Count  
Positive and Negative Numbers */ 
%{ 
int positive_no = 0, negative_no = 0; 
%} 
   
/* Rules for identifying and counting  
positive and negative numbers*/
%% 
^[-][0-9]+ {negative_no++;  
            printf("negative number = %s\n", 
                  yytext);}  // negative number 
  
[0-9]+ {positive_no++; 
        printf("positive number = %s\n",  
                 yytext);} // positive number      
%%  
  
/*** use code section ***/
  
int yywrap(){} 
int main()                                               
{ 
   
yylex();  
printf ("number of positive numbers = %d,"
        "number of negative numbers = %d\n", 
                positive_no, negative_no); 
  
return 0;  
}

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
3.LEX-ODD EVEN
%{ 
#include<stdio.h> 
int i; 
%} 
  
%% 
  
[0-9]+     {i=atoi(yytext); 
          if(i%2==0)  
               printf("Even"); 
          else
         printf("Odd");} 
%% 
   
int yywrap(){} 
   
/* Driver code */
int main() 
{ 
   
    yylex(); 
    return 0; 
}

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. LEX-PRIME

%{ 
   /* Definition section */
   #include<stdio.h> 
   #include<stdlib.h> 
   int flag,c,j; 
%} 
  
/* Rule Section */
%% 
[0-9]+ {c=atoi(yytext); 
         if(c==2) 
         { 
           printf("\n Prime number"); 
         } 
         else if(c==0 || c==1) 
         { 
           printf("\n Not a Prime number"); 
         } 
         else
         { 
           for(j=2;j<c;j++) 
         {   
         if(c%j==0) 
           flag=1; 
         } 
         if(flag==1) 
           printf("\n Not a prime number"); 
         else if(flag==0) 
           printf("\n Prime number"); 
         } 
       } 
%% 
  
// driver code 
int main() 
 { 
  yylex(); 
  return 0; 
 }

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
FIRST FOLLOW

// C program to calculate the First and
// Follow sets of a given grammar
#include <ctype.h>
#include <stdio.h>
#include <string.h>

// Functions to calculate Follow
void followfirst(char, int, int);
void follow(char c);

// Function to calculate First
void findfirst(char, int, int);

int count, n = 0;

// Stores the final result
// of the First Sets
char calc_first[10][100];

// Stores the final result
// of the Follow Sets
char calc_follow[10][100];
int m = 0;

// Stores the production rules
char production[10][10];
char f[10], first[10];
int k;
char ck;
int e;

int main(int argc, char** argv)
{
	int jm = 0;
	int km = 0;
	int i, choice;
	char c, ch;
	count = 8;

	// The Input grammar
	strcpy(production[0], "X=TnS");
	strcpy(production[1], "X=Rm");
	strcpy(production[2], "T=q");
	strcpy(production[3], "T=#");
	strcpy(production[4], "S=p");
	strcpy(production[5], "S=#");
	strcpy(production[6], "R=om");
	strcpy(production[7], "R=ST");

	int kay;
	char done[count];
	int ptr = -1;

	// Initializing the calc_first array
	for (k = 0; k < count; k++) {
		for (kay = 0; kay < 100; kay++) {
			calc_first[k][kay] = '!';
		}
	}
	int point1 = 0, point2, xxx;

	for (k = 0; k < count; k++) {
		c = production[k][0];
		point2 = 0;
		xxx = 0;

		// Checking if First of c has
		// already been calculated
		for (kay = 0; kay <= ptr; kay++)
			if (c == done[kay])
				xxx = 1;

		if (xxx == 1)
			continue;

		// Function call
		findfirst(c, 0, 0);
		ptr += 1;

		// Adding c to the calculated list
		done[ptr] = c;
		printf("\n First(%c) = { ", c);
		calc_first[point1][point2++] = c;

		// Printing the First Sets of the grammar
		for (i = 0 + jm; i < n; i++) {
			int lark = 0, chk = 0;

			for (lark = 0; lark < point2; lark++) {

				if (first[i] == calc_first[point1][lark]) {
					chk = 1;
					break;
				}
			}
			if (chk == 0) {
				printf("%c, ", first[i]);
				calc_first[point1][point2++] = first[i];
			}
		}
		printf("}\n");
		jm = n;
		point1++;
	}
	printf("\n");
	printf("-----------------------------------------------"
		"\n\n");
	char donee[count];
	ptr = -1;

	// Initializing the calc_follow array
	for (k = 0; k < count; k++) {
		for (kay = 0; kay < 100; kay++) {
			calc_follow[k][kay] = '!';
		}
	}
	point1 = 0;
	int land = 0;
	for (e = 0; e < count; e++) {
		ck = production[e][0];
		point2 = 0;
		xxx = 0;

		// Checking if Follow of ck
		// has already been calculated
		for (kay = 0; kay <= ptr; kay++)
			if (ck == donee[kay])
				xxx = 1;

		if (xxx == 1)
			continue;
		land += 1;

		// Function call
		follow(ck);
		ptr += 1;

		// Adding ck to the calculated list
		donee[ptr] = ck;
		printf(" Follow(%c) = { ", ck);
		calc_follow[point1][point2++] = ck;

		// Printing the Follow Sets of the grammar
		for (i = 0 + km; i < m; i++) {
			int lark = 0, chk = 0;
			for (lark = 0; lark < point2; lark++) {
				if (f[i] == calc_follow[point1][lark]) {
					chk = 1;
					break;
				}
			}
			if (chk == 0) {
				printf("%c, ", f[i]);
				calc_follow[point1][point2++] = f[i];
			}
		}
		printf(" }\n\n");
		km = m;
		point1++;
	}
}

void follow(char c)
{
	int i, j;

	// Adding "$" to the follow
	// set of the start symbol
	if (production[0][0] == c) {
		f[m++] = '$';
	}
	for (i = 0; i < 10; i++) {
		for (j = 2; j < 10; j++) {
			if (production[i][j] == c) {
				if (production[i][j + 1] != '\0') {
					// Calculate the first of the next
					// Non-Terminal in the production
					followfirst(production[i][j + 1], i,
								(j + 2));
				}

				if (production[i][j + 1] == '\0'
					&& c != production[i][0]) {
					// Calculate the follow of the
					// Non-Terminal in the L.H.S. of the
					// production
					follow(production[i][0]);
				}
			}
		}
	}
}

void findfirst(char c, int q1, int q2)
{
	int j;

	// The case where we
	// encounter a Terminal
	if (!(isupper(c))) {
		first[n++] = c;
	}
	for (j = 0; j < count; j++) {
		if (production[j][0] == c) {
			if (production[j][2] == '#') {
				if (production[q1][q2] == '\0')
					first[n++] = '#';
				else if (production[q1][q2] != '\0'
						&& (q1 != 0 || q2 != 0)) {
					// Recursion to calculate First of New
					// Non-Terminal we encounter after
					// epsilon
					findfirst(production[q1][q2], q1,
							(q2 + 1));
				}
				else
					first[n++] = '#';
			}
			else if (!isupper(production[j][2])) {
				first[n++] = production[j][2];
			}
			else {
				// Recursion to calculate First of
				// New Non-Terminal we encounter
				// at the beginning
				findfirst(production[j][2], j, 3);
			}
		}
	}
}

void followfirst(char c, int c1, int c2)
{
	int k;

	// The case where we encounter
	// a Terminal
	if (!(isupper(c)))
		f[m++] = c;
	else {
		int i = 0, j = 1;
		for (i = 0; i < count; i++) {
			if (calc_first[i][0] == c)
				break;
		}

		// Including the First set of the
		// Non-Terminal in the Follow of
		// the original query
		while (calc_first[i][j] != '!') {
			if (calc_first[i][j] != '#') {
				f[m++] = calc_first[i][j];
			}
			else {
				if (production[c1][c2] == '\0') {
					// Case where we reach the
					// end of a production
					follow(production[c1][0]);
				}
				else {
					// Recursion to the next symbol
					// in case we encounter a "#"
					followfirst(production[c1][c2], c1,
								c2 + 1);
				}
			}
			j++;
		}
	}
}


--------------------------------------------------------------------------------------------------------------------------------------------------------------------
LEADING TRAILING

#include<stdio.h>
#include<string.h>

#define MAX_PRODUCTIONS 30
#define MAX_SYMBOLS 10
#define MAX_EXPRESSION_LENGTH 50

int nt, t, top = 0;
char s[MAX_SYMBOLS], NT[MAX_SYMBOLS], T[MAX_SYMBOLS], st[MAX_EXPRESSION_LENGTH], l[MAX_SYMBOLS][MAX_SYMBOLS], tr[MAX_SYMBOLS][MAX_SYMBOLS];

int searchnt(char a) {
    int count = -1, i;
    for (i = 0; i < nt; i++) {
        if (NT[i] == a)
            return i;
    }
    return count;
}

int searchter(char a) {
    int count = -1, i;
    for (i = 0; i < t; i++) {
        if (T[i] == a)
            return i;
    }
    return count;
}

void push(char a) {
    s[top] = a;
    top++;
}

char pop() {
    top--;
    return s[top];
}

void installl(int a, int b) {
    if (l[a][b] == 'f') {
        l[a][b] = 't';
        push(T[b]);
        push(NT[a]);
    }
}

void installt(int a, int b) {
    if (tr[a][b] == 'f') {
        tr[a][b] = 't';
        push(T[b]);
        push(NT[a]);
    }
}

int main() {
    int i, s, k, j, n;
    char pr[MAX_PRODUCTIONS][MAX_EXPRESSION_LENGTH], b, c;
   
    printf("Enter the no of productions:");
    scanf("%d", &n);
    printf("Enter the productions one by one\n");
    for (i = 0; i < n; i++)
        scanf("%s", pr[i]);

    nt = 0;
    t = 0;

    for (i = 0; i < n; i++) {
        if ((searchnt(pr[i][0])) == -1)
            NT[nt++] = pr[i][0];
    }

    for (i = 0; i < n; i++) {
        for (j = 3; j < strlen(pr[i]); j++) {
            if (searchnt(pr[i][j]) == -1) {
                if (searchter(pr[i][j]) == -1)
                    T[t++] = pr[i][j];
            }
        }
    }

    for (i = 0; i < nt; i++) {
        for (j = 0; j < t; j++)
            l[i][j] = 'f';
    }

    for (i = 0; i < nt; i++) {
        for (j = 0; j < t; j++)
            tr[i][j] = 'f';
    }

    for (i = 0; i < nt; i++) {
        for (j = 0; j < n; j++) {
            if (NT[(searchnt(pr[j][0]))] == NT[i]) {
                if (searchter(pr[j][3]) != -1)
                    installl(searchnt(pr[j][0]), searchter(pr[j][3]));
                else {
                    for (k = 3; k < strlen(pr[j]); k++) {
                        if (searchnt(pr[j][k]) == -1) {
                            installl(searchnt(pr[j][0]), searchter(pr[j][k]));
                            break;
                        }
                    }
                }
            }
        }
    }

    while (top != 0) {
        b = pop();
        c = pop();
        for (s = 0; s < n; s++) {
            if (pr[s][3] == b)
                installl(searchnt(pr[s][0]), searchter(c));
        }
    }

    for (i = 0; i < nt; i++) {
        printf("Leading[%c]\t{", NT[i]);
        for (j = 0; j < t; j++) {
            if (l[i][j] == 't')
                printf("%c,", T[j]);
        }
        printf("}\n");
    }

    top = 0;
    for (i = 0; i < nt; i++) {
        for (j = 0; j < n; j++) {
            if (NT[searchnt(pr[j][0])] == NT[i]) {
                if (searchter(pr[j][strlen(pr[j]) - 1]) != -1)
                    installt(searchnt(pr[j][0]), searchter(pr[j][strlen(pr[j]) - 1]));
                else {
                    for (k = (strlen(pr[j]) - 1); k >= 3; k--) {
                        if (searchnt(pr[j][k]) == -1) {
                            installt(searchnt(pr[j][0]), searchter(pr[j][k]));
                            break;
                        }
                    }
                }
            }
        }
    }

    while (top != 0) {
        b = pop();
        c = pop();
        for (s = 0; s < n; s++) {
            if (pr[s][3] == b)
                installt(searchnt(pr[s][0]), searchter(c));
        }
    }

    for (i = 0; i < nt; i++) {
        printf("Trailing[%c]\t{", NT[i]);
        for (j = 0; j < t; j++) {
            if (tr[i][j] == 't')
                printf("%c,", T[j]);
        }
        printf("}\n");
    }

    return 0;
}

_________________________________________________________________________________________________________________________________________________________________________
LEXICAL ANALYZER FOR REGULAR EXP
%{
#include <stdio.h>
#include <stdlib.h>
%}

%%

"+"             { printf("TOKEN: PLUS\n"); }
"-"             { printf("TOKEN: MINUS\n"); }
"*"             { printf("TOKEN: ASTERISK\n"); }
"/"             { printf("TOKEN: SLASH\n"); }
"("             { printf("TOKEN: LPAREN\n"); }
")"             { printf("TOKEN: RPAREN\n"); }
"|"             { printf("TOKEN: PIPE\n"); }
[a-zA-Z0-9]+    { printf("TOKEN: LITERAL (%s)\n", yytext); }
[ \t\n]         ;  // Skip whitespace

.               { printf("Invalid character: %s\n", yytext); exit(1); }

%%

int main(int argc, char* argv[]) {
    if (argc != 2) {
        printf("Usage: %s \"regular_expression\"\n", argv[0]);
        return 1;
    }

    yy_scan_string(argv[1]);
    yylex();
    yy_delete_buffer(YY_CURRENT_BUFFER);
    return 0;
}


OR
%{
#include <stdio.h>
%}

DIGIT [0-9]
WS [ \t\n]

%%

{DIGIT}+    { printf("NUMBER: %s\n", yytext); }
[-+*/()]   { printf("OPERATOR/PARENTHESIS: %c\n", yytext[0]); }
{WS}+       ;  // Ignore whitespace

.           { fprintf(stderr, "Invalid character: %c\n", yytext[0]); }

%%

int main() {
    yylex();
    return 0;
}

__________________________________________________________________________________________________________________________________________________________________

LEX PROGRAM FOR CALCULATOR

%{
#include <stdio.h>
#include <stdlib.h>

int op = 0;
float a, b;

// Forward declaration for the digi function
void digi();
%}

dig [0-9]+|([0-9]*)"."([0-9]+)
add "+"
sub "-"
mul "*"
div "/"
pow "^"
ln \n

%% 

{dig} { digi(); }  
{add} { op=1; } 
{sub} { op=2; } 
{mul} { op=3; } 
{div} { op=4; } 
{pow} { op=5; } 
{ln} { printf("\n The Answer : %f\n\n", a); } 
  
%% 

void digi() {
    int i; // Declaration moved inside the function

    if (op == 0) {
        a = atof(yytext);
    } else {
        b = atof(yytext);

        switch (op) {
            case 1: a = a + b; break;
            case 2: a = a - b; break;
            case 3: a = a * b; break;
            case 4: a = a / b; break;
            case 5: 
                for (i = 1; i < b; i++) // Changed loop control variable
                    a = a * a;
                break;
        }

        op = 0;
    }
}

int main(int argc, char *argv[]) {
    yylex();
    return 0;
}

int yywrap() {
    return 1;
}
[[[[[[[[[[[[[[[[[[[[[[[[[[[[[ YAHA INPUT 3+3 YA 6*8 AISE DENA MTLB 2 NUMBER AND BEECH ME OPERATOR]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]]] 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
JAVA FOR ADDITION OF NUM

import java.util.Scanner;

public class SumCalculator {
    public static void main(String[] args) {
        // Create a Scanner object to read input from the user
        Scanner scanner = new Scanner(System.in);
        
        // Prompt the user to enter the first number
        System.out.print("Enter the first number: ");
        int num1 = scanner.nextInt();
        
        // Prompt the user to enter the second number
        System.out.print("Enter the second number: ");
        int num2 = scanner.nextInt();
        
        // Calculate the sum
        int sum = num1 + num2;
        
        // Print the result
        System.out.println("The sum of " + num1 + " and " + num2 + " is: " + sum);
        
        // Close the Scanner object
        scanner.close();
    }
}

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
JAVA- REVRESE A NUM
import java.util.Scanner;

public class ReverseNumber{
    public static void main(String[] args) {
        Scanner inputScanner = new Scanner(System.in);
        System.out.print("Enter a positive integer: ");
        int number = inputScanner.nextInt();
        inputScanner.close();

        int reverse = 0;
        int originalNumber = number;

        while (number != 0) {
            int remainder = number % 10;
            reverse = reverse * 10 + remainder;
            number = number / 10;
        }

        System.out.println("Original Number: " + originalNumber);
        System.out.println("Reversed Number: " + reverse);
    }
}

_____________________________________________________________________________________________________________________________________________________________________


JAVA- FACTORIAL

import java.util.Scanner;
public class factorial{
    public static void main(String[] args){
        Scanner scanner= new Scanner(System.in);
        System.out.print("Enter num");
        int num1= scanner.nextInt();
        long factorial2= calculatefactorial(num1);
        System.out.println("factorial is"+factorial2);
        scanner.close();
    }
    public static long calculatefactorial(int n){
        if (n==0||n==1){
            return 1;
        }
        else{
            return n*calculatefactorial(n-1);
        }
    }
}

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
JAVA-EVEN ODD

import java.util.Scanner;
public class evenodd{
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        System.out.print("Enter a num ");
        int num= scanner.nextInt();
        if(num%2==0){
            System.out.println("even");
        }else{
            System.out.println("odd");
        }
        scanner.close();
    }
}

_______________________________________________________________________________________________________________________________________________________________________________

JAVA- SUM OF ALL ELEMENTS OF AN ARRAY 
import java.util.Scanner;

public class ArraySumCalculator {
    public static void main(String[] args) {
        // Create a Scanner object to read input from the user
        Scanner scanner = new Scanner(System.in);
        
        // Prompt the user to enter the size of the array
        System.out.print("Enter the size of the array: ");
        int size = scanner.nextInt();
        
        // Create an array of the specified size
        int[] array = new int[size];
        
        // Prompt the user to enter the elements of the array
        System.out.println("Enter the elements of the array:");
        for (int i = 0; i < size; i++) {
            System.out.print("Element " + (i + 1) + ": ");
            array[i] = scanner.nextInt();
        }
        
        // Calculate the sum of all elements in the array
        int sum = calculateArraySum(array);
        
        // Print the result
        System.out.println("The sum of all elements in the array is: " + sum);
        
        // Close the Scanner object
        scanner.close();
    }
    
    // Method to calculate the sum of all elements in an array
    public static int calculateArraySum(int[] array) {
        int sum = 0;
        for (int num : array) {
            sum += num;
        }
        return sum;
    }
}


________________________________________________________________________________________________________________________________________________________________________
JAVA QUOTIENT REMAINDER
public class QuotientAndRemainder { 

	public static void main(String[] args) 
	{ 

		int dividend = 556, divisor = 9; 

		int quotient = dividend / divisor; 
		int remainder = dividend % divisor; 

		System.out.println("The Quotient is = " + quotient); 
		System.out.println("The Remainder is = " + remainder); 
	} 
}


_____________________________________________________________________________________________________________________________________________________________________________
BISON
%{
#include<stdio.h>

int regs[26];
int base;

%}

%start list

%union { int a; }


%token DIGIT LETTER

%left '|'
%left '&'
%left '+' '-'
%left '*' '/' '%'
%left UMINUS  /*supplies precedence for unary minus */

%%                   /* beginning of rules section */

list:                       /*empty */
         |
        list stat '\n'
         |
        list error '\n'
         {
           yyerrok;
         }
         ;
stat:    expr
         {
           printf("%d\n",$1);
         }
         |
         LETTER '=' expr
         {
           regs[$1.a] = $3.a;
         }

         ;

expr:    '(' expr ')'
         {
           $$ = $2;
         }
         |
         expr '*' expr
         {

           $$.a = $1.a * $3.a;
         }
         |
         expr '/' expr
         {
           $$.a = $1.a / $3.a;
         }
         |
         expr '%' expr
         {
           $$.a = $1.a % $3.a;
         }
         |
         expr '+' expr
         {
           $$.a = $1.a + $3.a;
         }
         |
         expr '-' expr
         {
           $$.a = $1.a - $3.a;
         }
         |
         expr '&' expr
         {
           $$.a = $1.a & $3.a;
         }
         |
         expr '|' expr
         {
           $$.a = $1.a | $3.a;
         }
         |

        '-' expr %prec UMINUS
         {
           $$.a = -$2.a;
         }
         |
         LETTER
         {
           $$.a = regs[$1.a];
         }

         |
         number
         ;

number:  DIGIT
         {
           $$ = $1;
           base = ($1.a==0) ? 8 : 10;
         }       |
         number DIGIT
         {
           $$.a = base * $1.a + $2.a;
         }
         ;

%%
main()
{
 return(yyparse());
}

yyerror(s)
char *s;
{
  fprintf(stderr, "%s\n",s);
}

yywrap()
{
  return(1);
}

________________________________________________________________________________________________________________________________________________________________________


LEXICAL ANALYZER IN BISON
%{

#include <stdio.h>
#include "y.tab.h"
int c;
%}
%%
" "       ;
[a-z]     {
            c = yytext[0];
            yylval.a = c - 'a';
            return(LETTER);
          }
[0-9]     {
            c = yytext[0];
            yylval.a = c - '0';
            return(DIGIT);
          }
[^a-z0-9\b]    {
                 c = yytext[0];
                 return(c);
              }
%%

