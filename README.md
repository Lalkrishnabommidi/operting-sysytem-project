# operting-sysytem-project
cse-316 operating system CA-3 K22ZC
//NAME: B.LAL KRISHNA
//ROLL NO: 41
//SECTION: K22ZC
#include <stdio.h>
#include<math.h>
#include<stdbool.h>
struct process
{
    int A,B,C;
};
void input(int a,int b,int c,struct process* k)
{
   k->A=a;
    k->B=b;
    k->C=c;
}
void findsafesequence(struct process available[],struct process allocation[],struct process max[])
{
    printf("Safe sequence : \n");
    int n=5;
    struct process remaining;
    struct process need[n];
    for(int i=0;i<n;i++)
    {
        need[i].A=fabs(allocation[i].A-max[i].A);
        need[i].B=fabs(allocation[i].B-max[i].B);
        need[i].C=fabs(allocation[i].C-max[i].C);
    }
    int count=0;
    while(true)
    {
        for(int i=0;i<n;i++)
        {
            if(((need[i].A<=available[0].A)&&(need[i].B<=available[0].B)&&(need[i].C<=available[0].C)) && (need[i].A!=-1))
            {
                remaining.A=(available[0].A-need[i].A);
                remaining.B=(available[0].B-need[i].B);
                remaining.C=(available[0].C-need[i].C);
                available[0].A=max[i].A+remaining.A;
                available[0].B=max[i].B+remaining.B;
                available[0].C=max[i].C+remaining.C;
                printf("Process[%d]",i);
                need[i].A=-1;
                printf("->");
            }
        }
        int kkk=0;
        for(int i=0;i<n;i++)
        {
            if(need[i].A==-1)
            {
                kkk++;
            }
        }
        if(kkk==n)
        {
            printf("|\nCompleted every process");
            return;
        }
    }
}
int main() {
    int n = 5;  // Number of processes
    int m = 3;  // Number of resource types
    
    struct process available[1];
    struct process max[n];
    struct process allocation[n];
    input(3,3,2,&available[0]);
    input(0,1,0,&allocation[0]);
    input(2,0,0,&allocation[1]);
    input(3,0,2,&allocation[2]);
    input(2,1,1,&allocation[3]);
    input(0,0,2,&allocation[4]);
    input(7,5,3,&max[0]);
    input(3,2,2,&max[1]);
    input(9,0,2,&max[2]);
    input(2,2,2,&max[3]);
    input(4,3,3,&max[4]);
    findsafesequence(available,allocation,max);
    return 0;
}
