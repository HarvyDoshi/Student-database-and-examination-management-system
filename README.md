# Student-database-and-examination-management-system
-It's a C language student database management system
-It's is a software developed for eligibility in examinations in schools & colleges.
-It has facilities like login system , accessing the attendance and fees paid of each student  of particular class ; roll-number wise.
-It has additional facilities like adding , deleting student’s data , setting up and reseting new eligibility criteria.
The concepts included are:
    i) Arrays
    ii) Functions
    iii) Structures


-----------   Code ------------


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include<conio.h>
int option = 0;
int i = 0;
int n = 0;
int j = 0;
float present = 80.00;
char money = 'P';
float totaldays = 1;
struct studentInfo {
	char name[20];
	int rno;
	char fees;
	float days;
	float attend;
} s[50];
void add(struct studentInfo s[]);
void login();
void eligibleStudents(struct studentInfo s[]);
void execution();
void printStudents(struct studentInfo s[]);
void deleterecord(struct studentInfo s[]);
void login()
{
	int a=0,i=0;
    char uname[10],c=' ';
    char pword[10],code[10];
    char user[10];
    char pass[10];
    do
{

printf("\n  =========================================  LOGIN FORM  ==========================================\n  ");
printf(" \n                                  ENTER USERNAME:-");
scanf("%s", &uname);
printf(" \n                                  ENTER PASSWORD:-");
	while(i<10)
	{
	    pword[i]=getch();
	    c=pword[i];
	    if(c==13) break;
	    else printf("*");
	    i++;
	}
	pword[i]='\0';
	i=0;
		if(strcmp(uname,"admin")==0 && strcmp(pword,"pass")==0)
	{
	printf("  \n\n\n       WELCOME TO OUR  STUDENT DATABASE & EXAMINATION MANAGEMENT SYSTEM !! YOUR LOGIN IS SUCCESSFUL");
	printf("\n\n\n\t\t\t\tPress any key to continue...");
	getch();
	break;
	}
	else
	{
		printf("\n        SORRY !!!!  LOGIN IS UNSUCESSFUL");
		a++;
        getch();
		system("cls");
	}
}
	while(a<=2);
	if (a>2)
	{
printf("\nSorry you have entered the wrong username and password for four times!!!");
getch();
}
		system("cls");
}
void execution()
{

printf("\n");
printf("                Enter the number to select the option \n");
printf("------------------------------------------------------------------------------------------------------\n");
printf("                       1.Eligible candidates \n");
printf("\n");
printf("                       2.Delete the student record \n");
printf("\n");
printf("                       3.Change the eligibility criteria \n");
printf("\n");
printf("                       4.Reset the eligibility criteria \n");
printf("\n");
printf("                       5.Print the list of all the student \n");
printf("\n");
printf("                                 ->Enter 0 to exit \n");
scanf("%d", &option);
printf("\n");
	switch (option) {
	case 1:
		eligibleStudents(s);
		execution();
		break;
case 2:
		deleterecord(s);
		execution();
		break;
case 3:
printf("Old Attendance required = %f",present);
printf("\n");
printf("\n Enter the updated attendance required \n");
printf("\n");
scanf("%f", &present);
printf("Eligibility Criteria updated \n");
printf("\n");
execution();
break;
case 4:
		present = 80.00;
		money = 'P';
		printf("Eligibility criteria reset \n");
		execution();
		break;

	case 5:
		printStudents(s);
		execution();
		break;

	case 6:
		execution();
		break;

	case 0:
		exit(0);

	default:
		printf("Enter number only from 0-4 \n");
		execution();
	}
}
void printStudents(struct studentInfo s[])
{
	for (i = 0; i < n; i++)
{
      if(s[i].rno != 0){
printf("Name of student %s \n",s[i].name);
printf("\n");
printf("Student roll number = %d \n",s[i].rno);
printf("\n");
printf("Student fees status = %c \n",s[i].fees);
printf("\n");
printf("Student number of days present = %f \n",s[i].days);
printf("\n");
printf("Student attendance = %f%%\n",s[i].attend);
printf("\n");}
else{
    printf("No student record is present right now.\n");
    break;
}
}
}
void deleterecord(struct studentInfo s[])
{
	int a = 0;
	printf("Enter the roll number of the student to delete it ");
	scanf("%d", &a);
	for (i = 0; i <= n; i++) {
		if (s[i].rno == (a)) {
			for (j = i; j < n; j++) {
				strcpy(s[j].name, s[j + 1].name);
				s[j].rno = s[j + 1].rno;
				s[j].fees = s[j + 1].fees;
				s[j].days = s[j + 1].days;
				s[j].attend = s[j + 1].attend;
			}
printf("                            Student Record deleted");
printf("\n");
		}
	}
}
void eligibleStudents(struct studentInfo s[])
{
	printf("____________________________________________________________ \n");
	printf("                       Qualified student are = \n");

	for (i = 0; i < n; i++) {
		if (s[i].fees == money || 'B' == money) {
			if (s[i].attend >= present) {
printf("Student name = %s \n",s[i].name);
printf("\n");
printf("Student roll no. = %d \n",s[i].rno);
printf("\n");
printf("Student fees = %c \n",s[i].fees);
printf("\n");
printf("Student attendance = %f%% \n",s[i].attend);
printf("\n");
			}
			else{
                printf("No students are eligible to give examination by the criteria.\n");
			}
		}
	}
}
void add(struct studentInfo s[50])
{
printf("\n");
printf("Enter the total number of working days: \n");
scanf("%f", &totaldays);
printf("\n");
printf("Enter the number of students: \n");
scanf("%d", &n);
printf("\n");
for (i = 0; i < n; i++)
{
printf("        Student number- %d \n",(i + 1));
printf("        ------------------\n");
printf("\n");
printf("Enter the name of the student: \n");
scanf("%s", s[i].name);
printf("\n");
printf("Enter the roll number: \n");
scanf(" %d", &s[i].rno);
printf("\n");
printf("Enter the fees of the student 'P' for paid , 'N' for not paid: \n");
scanf(" %c", &s[i].fees);
printf("\n");
printf("Enter the number of days the student was present: \n");
scanf("%f", &s[i].days);
printf("\n");
s[i].attend = (s[i].days/ totaldays)* 100;
printf("student attendance = %f%% \n",s[i].attend);
printf("\n");
	}
	execution();
}
int main()
{
    system("COLOR 0A");
    login();
    printf("------------*---------------*--------------*------------------------*---------------*-----------------\n");
	printf("                          Welcome to Student database registration \n");
	printf("======================================================================================================\n");
    printf("                               Press 0->Exit \n");
    printf("\n");
	printf("                               Press 1->Add student record \n");
	printf("======================================================================================================\n");
printf("------------*---------------*--------------*------------------------*---------------*-----------------\n");
scanf("%d", &option);
	switch (option) {
case 0:
		exit(0);
case 1:
		add(s);
		break;
default:
		printf("Only enter 0 or 1");
		execution();
	}
	return 0;
}
