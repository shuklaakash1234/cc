# cc merge two sting
#include<stdio.h>
#include<stdlib.h>

struct node{
  int data;
  struct node*next;
};

int length(struct node *head){
  int len = 0;
  while(head != NULL){
    len++;
    head = head->next;
  }
  return len;
}

struct node* findMergepoint(struct node* A, struct node* B){
  int m= length(A);
  int n= length(B);
  int d= n-m;
  if(m>n){
    struct node *temp = A;
    A=B;
    B=temp;
    d=m-n;
  }
  
  for(int i=0; i<d; i++){
    B = B->next;
  }
  
  while(A != NULL && B != NULL){
    if(A == B){
      return A;
    }
    A = A->next;
    B = B->next;
  }
    return NULL;
  }

int main(){
  struct node *head1 = NULL, *head2 = NULL;
  struct node *temp[7];
  for(int i =0; i<7; i++){
    temp[i] = (struct node *) malloc(sizeof(struct node));
  }
  temp[0]->data = 4;
  temp[0]->next=temp[1];
  temp[2]->data = 7;
  temp[1]->data = 6;
  temp[1]->next=temp[2];
  temp[2]->next=temp[3];
  temp[3]->data = 1;
  temp[3]->next=NULL;
  temp[4]->data = 9;
  temp[4]->next=temp[5];
  temp[5]->data = 3;
  temp[5]->next=temp[6];
  temp[6]->data = 4;
  temp[6]->next=temp[2];
  
  head1 = temp[0];
  head2 = temp[4];
  
  struct node *intersection = findMergepoint(head1, head2);
  if(intersection == NULL){
    printf("No merge point");
  }else{
    printf("Merge point found at node : %d",intersection->data);
  }
  return 0;
}
