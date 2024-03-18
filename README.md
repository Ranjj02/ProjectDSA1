#include<stdio.h>
#include<string.h>
#include<stdlib.h>

#define max_size 100

struct Patient
{
    int priority;
    char name[20];
    char gender[7];
    char bloodgroup[3];
    long int mobno;
    int age;
    char condition[70];
    int token;
};

struct queue
{
    struct Patient patient;
    struct queue *next;
}*front=NULL, *rear = NULL;

int n=0;

void insert(char n[],char g[],int pr,int a,char ca[],char bg[],int phno)
{
    struct queue *temp,*new;
    new = (struct queue *)malloc(sizeof(struct queue));
    strcpy(new->patient.name,n);
    strcpy(new->patient.gender,g);
    strcpy(new->patient.bloodgroup,bg);
    new->patient.age=a;
    new->patient.priority=pr;
    new->patient.mobno=phno;
    strcpy(new->patient.condition,ca);
    new->next = NULL;

    if (rear == NULL)
    {
        front = rear = new;
        return;
    }

    if ((new->patient.priority) < (front->patient.priority)) {
        new->next = front;
        front = new;
        return;
    }

    if ((new->patient.priority) >= (rear->patient.priority)) {
        rear->next = new;
        rear = new;
        return;
    }

    struct queue *prev = front, *curr = front->next;
    while (curr != NULL) {
        if ((new->patient.priority) < (curr->patient.priority)) {
     	   prev->next = new;
     	   new->next = curr;
     	   return;
        }
        prev = prev->next;
        curr = curr->next;
    }
}

void delete()
{
    struct queue *temp;
    if(front==NULL)
    {
        printf("\nNO PATIENT LEFT");
        return;
    }
    else
    {
        temp=front;
        printf("\n Deleted Record is : ");
        printf("\nName of the patient  	            : %s",temp->patient.name);
        printf("\nPatient's age        	            : %d",temp->patient.age);
        printf("\nGender  		      	    : %s",temp->patient.gender);
        printf("\nCondition   	      	            : %s",temp->patient.condition);
        printf("\nPatient's Blood group	            : %s",temp->patient.bloodgroup);
        printf("\n\n");
        front=front->next;
        free(temp);
    }
}

void print_patientdetails()
{
	int tokena=1;
	struct queue *temp;
	temp=front;
	if(front==NULL)
	{
    	printf("\nTHERE IS NO PATIENT");
	}
	else
	{
    	while(temp!=NULL)
    	{
         	temp->patient.token=tokena;
         	printf("\nName of the patient: 	%s",temp->patient.name);
         	printf("\nPatient's age  	: 	%d",temp->patient.age);
         	printf("\nGender         	: 	%s",temp->patient.gender);
         	printf("\nCondition      	: 	%s",temp->patient.condition);
         	printf("\nBlood Group    	: 	%s",temp->patient.bloodgroup);
         	printf("\nPriority       	: 	%d",temp->patient.token);
         	printf("\n\n");
         	tokena+=1;
         	temp=temp->next;
    	}
	}
}
int prioritise(char ca[])
{
    int p;
    if(strcmp(ca,"Heart attack")==0)
        return 1;
    if(strcmp(ca,"Cancer")==0)
        return 2;
    if(strcmp(ca,"Kidney Failure")==0)
        return 3;
    if(strcmp(ca,"Stroke")==0)
        return 4;
    if(strcmp(ca,"Asthma")==0)
        return 5;
    if(strcmp(ca,"Pneumonia")==0)
        return 6;
    if(strcmp(ca,"Trauma")==0)
        return 7;
    if(strcmp(ca,"Respiratory distress")==0)
        return 8;
    if(strcmp(ca,"Gastro intestinal bleeding")==0)
        return 9;
    if(strcmp(ca,"Allergic reactions")==0)
        return 10;
    if(strcmp(ca,"Drug overdose")==0)
        return 11;
    if(strcmp(ca,"Mental health")==0)
        return 12;
    return 13;
}

int main()
{
    int choice;
    char na[20],gend[7],ch,ca[50],bg[3];
    int ag,prior;
    long int phno;
    do{
   // 	system("COLOR 47");
  	   printf("\t\t\t-------------------------------\n");
        printf("\t\t\t\t\t\t\t\t\t\t\t\n");
        printf("\t\t\t\t\t\t\t\t\t\t\n");
        printf("\t\t\t WELCOME TO RVV HOSPITAL!\n");
        printf("\t\t\t\t\t\t\t\t\t\t\n");
        printf("\t\t\t\t\t\t\t\t\t\t\n");
        printf("\t\t\t-------------------------------\n");
        printf("\t\t\t1.ADD A PATIENT\n");
        printf("\t\t\t2.DELETE A RECORD\n");
        printf("\t\t\t3.DISPLAY ALL APPOINTMENTS\n");
        printf("\t\t\t4.EXIT\n");
        printf("\t\t\tEnter your choice:");
        scanf("%d",&choice);
        system("cls");
        switch(choice)
        {
        case 1:
   		 while(1)
  		  {
			  printf("\nEnter patient's name : ");
			  scanf("%s",na);
			   begin:
              printf("\nEnter Age : ");
			  scanf("%d",&ag);
			     if(ag>130)
          	{
              	printf("\nEnter a valid age");
              	goto begin;
          	}

			  printf("\nEnter gender : ");
			  scanf("%s",gend);
			  printf("\nEnter condition : ");
			  fflush(stdin);
			  gets(ca);
			  prior=prioritise(ca);
			  printf("\nEnter patient's bloodgroup : ");
			  scanf("%s",bg);
			  printf("\nEnter a contact number : ");
			  scanf("%d",&phno);
			  printf("\nDo you want to insert another record (Y/N)? : ");
			  scanf(" %c",&ch);
			  insert(na,gend,prior,ag,ca,bg,phno);
			  system("cls");
			  if(ch=='N' || ch=='n')
    			  break;
  		  }
  		  break;
        case 2:
   		   delete();
           system("pause");
           system("cls");

   		   break;
        case 3:
   		   print_patientdetails();
           system("pause");
           system("cls");

   		   break;
        case 4:
   		   exit(0);
   		   break;
        }

    }while(choice!=4);
    return 0;
}








