#include <stdio.h>
#include<conio.h>
#include <stdlib.h>
#include <string.h>

#define BUFFER_SIZE 1000

char buff[BUFFER_SIZE];
 FILE * fPtr;
 FILE * fTemp;


void main()
{
     char *str[2000];
    char *str1[2000];
    char *oldWord=NULL, *newWord=NULL;

    FILE *fp = fopen("french_dictionary.csv","r");

     fPtr  = fopen("t8.shakespeare.txt", "r");
    fTemp = fopen("replace.txt", "w");

    if (fPtr == NULL || fTemp == NULL)
    {
        printf("\nUnable to open file.\n");
        printf("Please check whether file exists and you have read/write privilege.\n");
        exit(EXIT_SUCCESS);
    }



    if(!fp){
        printf("error occured");
        return 0;
    }
    else{
        char buffer[1024];
        int row = 0;
        int column = 0;
        int i=0;
        int j=0;

        while (fgets(buffer,
                     1024, fp)) {
            column = 0;
            row++;
            int i=0,j=0;
            if (row == 1)
                continue;
            char* value = strtok(buffer, ", ");
              int r;
             for(r=0;r<=999;r++){
                
            while (value) {

                if (column == 0) {

                    str[i] = value;
                    
                    oldWord=str[i];
}
                if (column == 1) {

                       str1[j] = value;
                       
                        newWord=str1[j];



                }
                   if(oldWord!=NULL && newWord!=NULL ){
                   replica(oldWord,newWord);
                   oldWord=NULL;
                   newWord=NULL;
                }


                  i++;
                  j++;
                value = strtok(NULL, ", ");
                column++;


            }
            
             }

              printf("\n");

        }

         fclose(fp);
    }
    
}
    int replica(char *oldWord,char *newWord)
    {


    while ((fgets(buff, BUFFER_SIZE, fPtr)) != NULL)
    {
        replaceAll(buff, oldWord, newWord);
        fputs(buff, fTemp);
    }

    fclose(fPtr);
    fclose(fTemp);
    remove("t8.shakespeare.txt");
    rename("replace.tmp", "t8.shakespeare.txt");

    printf("\nSuccessfully replaced all occurrences of '%s' with '%s'.", oldWord, newWord);

    return 0;

    }

    void replaceAll(char *str, const char *oldWord, const char *newWord)
{
    char *pos, temp[BUFFER_SIZE];
    int index = 0;
    int owlen;

    owdlen = strlen(oldWord);

    if (!strcmp(oldWord, newWord)) {
        return;
    }

    while ((pos = strstr(str, oldWord)) != NULL)
    {
        
        strcpy(temp, str);
        index = pos - str;
        str[index] = '\0';
        strcat(str, newWord);
        strcat(str, temp + index + owlen);
    }
}
