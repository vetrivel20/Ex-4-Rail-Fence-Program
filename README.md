# Ex-4 Rail-Fence-Program

## Name: M.Vetrivel
## Register Number: 212225040487

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```c
#include <stdio.h>
#include <string.h>

void encryption(char PT[], int key, char CT[])
{
    int i, j, k = 0;
    int len = strlen(PT);
    char rail[key][len];

    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    for (i = 0; i < len; i++)
        rail[i % key][i] = PT[i];

    for (i = 0; i < key; i++)
    {
        for (j = 0; j < len; j++)
        {
            if (rail[i][j] != '\n')
                CT[k++] = rail[i][j];
        }
    }

    CT[k] = '\0';
}

void decryption(char CT[], int key, char DT[])
{
    int i, j, k = 0;
    int len = strlen(CT);
    char rail[key][len];

    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    for (i = 0; i < len; i++)
        rail[i % key][i] = '*';

    for (i = 0; i < key; i++)
    {
        for (j = 0; j < len; j++)
        {
            if (rail[i][j] == '*')
                rail[i][j] = CT[k++];
        }
    }

    for (i = 0; i < len; i++)
        DT[i] = rail[i % key][i];

    DT[len] = '\0';
}

int main()
{
    char PT[100], CT[100], DT[100];
    int key;

    printf("Enter the plaintext: ");
    scanf("%99s", PT);

    printf("Enter the key: ");
    scanf("%d", &key);

    if (key < 1 || key > strlen(PT))
    {
        printf("Invalid key.\n");
        return 1;
    }

    encryption(PT, key, CT);
    printf("Encrypted text: %s\n", CT);

    decryption(CT, key, DT);
    printf("Decrypted text: %s\n", DT);

    return 0;
}

```

# OUTPUT

![alt text](OUTPUT.png)

# RESULT

The C program to implement the rail fence transposition technique is executed sucessfully.
