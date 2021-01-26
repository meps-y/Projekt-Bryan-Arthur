# Projekt-Bryan-Arthur
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

    int mode; // Was für ein Spiel?? Spieler gegen Spieler oder Spieler gegen Computer
    int i,j; // i-Zeile und j-Spalte
    int k,m; // k-n-te Zug, insgesamt 9
             // m
    char Spieler, Gewinner; // Spieler: der Spieler, der am Zug ist
                            // Gewinner: der Spieler, der am Ende gewonnen hat
    char Name[15]; // Name des Spielers
    char PlayerX[15];
    char PlayerO[15];

    char a[3][3]={"   ","   ","   "};

    void diplay(i,j);
    void gameMode(i,j,k);


void display(i,j) //das Tictoe ausgeben
{
    printf("\r\n");
    printf("   0  |  1 |  2 |\n");
    printf("-----------------\n");
    for(i=0;i<3;i++){
        printf("%d|", i);
            printf("  ");
        for(j=0;j<3;j++){
            printf("%c |  ", a[i][j]);
        }
        printf("\n");
        printf("-----------------\n");
    }
}

int sameRow(i) //Überprüfen, ob Bauer gleicher Art in derselben Zeile liegen
{
    for(i=0;i<3;i++){
        if((a[i][0] == a[i][1]) && (a[i][1] == a[i][2])){
                Gewinner=a[i][1];
            return 1;
        }
    }
    return 0;
}

int sameColumn(j) //Überprüfen, ob Bauer gleicher Art in derselben Spalte liegen
{
    for(j=0;j<3;j++){
        if((a[0][j] == a[1][j]) && (a[1][j] == a[2][j])){
                Gewinner=a[1][j];
            return 1;
        }
    }
    return 0;
}

int sameDiagonal() //Überprüfen, ob Bauer gleicher Art in einer Diagonal liegen
{
    if(((a[0][0] == a[1][1]) && (a[1][1]==a[2][2])) || ((a[2][0]==a[1][1]) &&(a[1][1]==a[0][2]))){
            Gewinner=a[1][1];
        return 1;
    }
    return 0;
}

void ende()
{
    printf("Was moechten Sie tun??\n");
    printf("1. Weiterspielen\n");
    printf("2. Das Spiel beenden\n\n");
    scanf("%d", &m);
        switch(m){
            case 1: gameMode(i,j,k);
                break;
            case 2: return 0;
                break;
        }
}
void name(){

}
void gegenFreund(i,j,k)
{

    for(k=1;k<=9;k++){
        Spieler = (k%2!=0) ? 'X' : 'O';
        strcpy(Name,((k%2!=0) ? PlayerX : PlayerO));

        printf("\n\n%s, Enter row and column: ", Name);
            scanf("%d %d", &i,&j);
            if(a[i][j]==' '){
                            a[i][j]=Spieler;
                            display(i,j);
            }
            else{
                printf("\nFeld schon besetzt\nBitte nur im Freiraum eintragen\n");
                k=k-1;
            }
            if(k>5){
                if(sameRow(i)||sameColumn(j)||sameDiagonal()){
                    if(Gewinner != ' '){
                        if(Gewinner == 'X'){
                            strcpy(Name,PlayerX);
                        }else{
                            strcpy(Name,PlayerO);
                        }
                        printf("%s, du hast gewonnen \n\n", Name);
                    }
                return ende();
                }
            }
    }

    printf("Das Spiel ist unentschieden\n\n");
    return ende();

}
void gegenComputer(i,j,k)
{
    i=0;
}

void gameMode(i,j,k)
{
    printf("\nWas moechtest du??\n1)Gegen einen Freund spielen oder\n2)gegen den Computer\n\n");
    scanf("%d", &mode);
    printf("\n");

    switch(mode){
    case 1:
        printf("PlayerX Enter your name: %s", PlayerX);
        scanf("%s", PlayerX);
        printf("\n");
        printf("PlayerO Enter your name: %s", PlayerO);
        scanf("%s", PlayerO);
        printf("\n°°°°°Das Spiel beginnt°°°°°° ^^ ** ##\n");
        gegenFreund(i,j,k);
        break;
    case 2: gegenComputer(i,j,k);
    }

}



int main()
{
    printf("Willkommen beim Tic-tac-toe Spiel\n");
    gameMode(i,j,k);
}



    /*int i,j,feld;
    char board[feld], a[i][j];
    feld=1;
    for(i=0;i<3;i++){
        for(j=0;j<3;j++){
            board[feld]=a[i][j];
            feld++;
        }
    }
    int i; //das Feld
    int k; //Anzahl der zu
    char board[10]={         };

void displayBoard(i)
{
    printf("\n");
    for(i=0;i<9;i++){
        printf(" | %c ", board[i]);
        if((i+1)%3==0){
            printf(" |\n");
            printf(" ----------------\n");
        }
    }
}


void gegenComputer(i,j,k)
{
    int k; //n-te Zug, insgesamt 9
    int x; // benutzt um zu bestimmen, wer am Zug ist, Spieler oder Computer??
    int w; // benutzt um zu bestimmen, wer das Spiel anfaengt, Spieler oder Computer??

    printf("Moechtest du anfangen??\nTipp 1 wenn ja, und 0 wenn nicht\n");
    scanf("%d", &w);
    for(k=w;k<w+9;k++){
        x = (k%2!=0) ? 1 : 0;
        if(x){      //Spieler ist am Zug
            printf("\n\nGib das Feld ein: "); //{ 1 | 2 | 3
                                              //  4 | 5 | 6
                                              //  7 | 8 | 9}
            int j;
            scanf("%d", &j);
            i=j-1;
            if(board[i]==' '){
                        board[i]='X';
                        displayBoard(i);
            }
            else{
                printf("\nFeld schon besetzt\nBitte nur im Freiraum eintragen\n");
                k=k-1;
            }
        }
        else{       //Computer spielt
            for(int n=0;n<9;n++){
                i=(rand()%10)+1; // wir versuchen ein Feld durch rand() zufällig zu bekommen
                if(board[i]==' '){
                        board[i]='O';
                        diplayBoard(i);
                        break;
                }
            }
        }
        if(k>5){
            if(sameRow(i)||sameColumn(j)||sameDiagonal()){
                if(Gewinner != 'X'){
                    printf("Spieler %c hat gewonnen\n\n", );
                }
            return ende();
            }
        }
    }
    printf("Das Spiel ist unentschieden\n\n");
    return ende();

}*/
