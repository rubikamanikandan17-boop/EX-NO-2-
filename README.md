## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




Program:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char key[] = "MONOPOLY";
    char text[] = "Rubikamanikandan";
    char matrix[5][5], cipher[100], plain[100];
    int used[26] = {0};
    int i, j, l, k = 0, r1, c1, r2, c2;
    char a, b, ch;

    for (i = 0; key[i]; i++)
    {
        ch = tolower(key[i]);
        if (ch == 'j')
            ch = 'i';

        if (!used[ch - 'a'])
        {
            matrix[k / 5][k % 5] = ch;
            used[ch - 'a'] = 1;
            k++;
        }
    }

    used['j' - 'a'] = 1;

    for (ch = 'a'; ch <= 'z'; ch++)
    {
        if (!used[ch - 'a'])
        {
            matrix[k / 5][k % 5] = ch;
            k++;
        }
    }

    strcpy(plain, text);

    for (i = 0; text[i]; i++)
    {
        text[i] = tolower(text[i]);
        if (text[i] == 'j')
            text[i] = 'i';
    }

    printf("Key text : Monopoly\n");
    printf("Plain text : Rubikamanikandan\n");

    k = 0;

    for (i = 0; text[i]; i += 2)
    {
        a = text[i];

        if (text[i + 1] == '\0')
            b = 'x';
        else if (text[i] == text[i + 1])
        {
            b = 'x';
            i--;
        }
        else
            b = text[i + 1];

        for (j = 0; j < 5; j++)
        {
            for (l = 0; l < 5; l++)
            {
                if (matrix[j][l] == a)
                {
                    r1 = j;
                    c1 = l;
                }

                if (matrix[j][l] == b)
                {
                    r2 = j;
                    c2 = l;
                }
            }
        }

        if (r1 == r2)
        {
            cipher[k++] = matrix[r1][(c1 + 1) % 5];
            cipher[k++] = matrix[r2][(c2 + 1) % 5];
        }
        else if (c1 == c2)
        {
            cipher[k++] = matrix[(r1 + 1) % 5][c1];
            cipher[k++] = matrix[(r2 + 1) % 5][c2];
        }
        else
        {
            cipher[k++] = matrix[r1][c2];
            cipher[k++] = matrix[r2][c1];
        }
    }

    cipher[k] = '\0';

    printf("Cipher text: %s\n", cipher);
    printf("Decrypted text: %s\n", plain);

    return 0;
}
```



Output:
<img width="1920" height="1080" alt="Screenshot 2026-10-23 144117" src="https://github.com/user-attachments/assets/f02653f1-4f58-45f2-9a9a-f4f5ce6bf895" />

