#include<stdio.h>
#include<stdlib.h>
struct node
{
    int cof;
    int pow;
    struct node *link;
};

//DISPLAY POLYNOMIAL 
void disp(struct node *head){
    struct node*dis=head;
    while(dis!=NULL)
    {
        printf("%dx ^ %d",dis->cof,dis->pow);
        dis=dis->link;
        if(dis!=0)
            printf(" + ");
        else
            printf("\n");
    }
     //printf("%dx^%d+",dis->cof,dis->pow);
}

struct node*create_list(struct node*head,int cof,int pow)
{
  struct node*ptr;
  struct node*tem=malloc(sizeof(struct node));
        
  tem->cof=cof;
  tem->pow=pow;
  tem->link=NULL;
  
  if(head==NULL || head->pow < pow)
  {
    tem->link=head;
    head=tem;
  }
  else
  {
    ptr=head;
    while(ptr->link!=0 && ptr->link->pow > pow)
    {
      ptr=ptr->link;
    
    }
      tem->link=ptr->link;
      ptr->link=tem;
  }
    return(head);
}
struct node*create(struct node*head)
{
    int n,cof,pow;
    printf("Enter number of terms : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
    {
        printf("\nEnter coefficient : ");
        scanf("%d",&cof);
        printf("Enter power : ");
        scanf("%d",&pow);
        head=create_list(head,cof,pow);
    }
    return head;
}

// ADDITION 
void addition(struct node*head,struct node*head1,struct node*headadd){
    struct node*first=head;
    struct node*sec=head1;
    
    while(first!=NULL && sec!=NULL){
        
    if(first->pow > sec->pow)
    {  
        headadd=create_list(headadd,first->cof,first->pow);
        first=first->link;
        
    }else if(first->pow < sec->pow){
        headadd=create_list(headadd,sec->cof,sec->pow);
        sec=sec->link;
        
    }else if(first->pow == sec->pow){
        headadd=create_list(headadd,first->cof+sec->cof,first->pow);
        first=first->link;
        sec=sec->link;
    }
    }
    while(first!=NULL){
        headadd=create_list(headadd,first->cof,first->pow);
        first=first->link;
    }
    while(sec!=NULL){
        headadd=create_list(headadd,sec->cof,sec->pow);
        sec=sec->link;
    }
    printf("\n");
    disp(headadd);
}


int main()
{
    printf("\tPOLYNOMIAL ADDITION\n\n");
    printf("---Enter 1st polynomial---\n");
    struct node*head=NULL;
    struct node*headadd=NULL;
    struct node*head1=NULL;
    head=create(head);
    
    //print
    disp(head);

    printf("\n---Enter 2nd polynomial---\n");
    head1=create(head1);
    //PRINT 
    disp(head1);
    
    //PERFORMING ADDITION
    printf("\n\n+");
    disp(head);
    disp(head1);
    
    addition(head,head1,headadd);
    
    return 0;
}