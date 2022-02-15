#include<stdio.h>

#include<stdlib.h>

typedef struct tree *node;

node insert(int, node T);

node Findmin(node T);

node del(int, node T);

void display(node T);

struct tree

{

int data;

struct tree *right,*left;

}*root;

int main()

{

 node T = NULL;

 int data,n,i=0;

 char c;

 clrscr ();

 printf("enter the number of elements in the tree\n");

 scanf("%d",&n);

 printf("\n enter the elements\n");

 while(i<n)

 {

  scanf("%d",&data);

  T=insert(data,T);

  i++;

  }

  printf("\n elements isplayed in inorder format\n");

  display(T);

  printf("\n enter the element to delete\n");

  scanf("%d",&data);

  T=del(data,T);

  printf("\n contents after deletion\n");

  display(T);

  return(1);

  }

  node insert(int X,node T)

  {

   struct tree *newnode;

   newnode = malloc(sizeof(struct tree));

   if(newnode==NULL)

      printf("out of space\n");

   else

     if(T==NULL)

      {

       newnode->data=X;

       newnode->left=NULL;

       newnode->right=NULL;

       T=newnode;

       }

     else

     {

      if(X<T->data)

       T->left=insert(X,T->left);

       else

       T->right=insert(X,T->right);

       }

       return T;

       }

    node del(int X,node T)

    {

     node Tmpcell;

     if(T== NULL)

       printf("element not found");

       //exit(0);

     else

       if(X<T->data)

 T->left=del(X,T->left);

       else

 if(X>T->data)

  T->right=del(X,T->right);

 else

  if(T->left && T->right)

   {

    Tmpcell = Findmin(T->right);

    T->data = Tmpcell->data;

    T->right=del(T->data,T->right);

    }

   else

    {

    Tmpcell=T;

    if(T->left==NULL)

     T=T->right;

    else if(T->right==NULL)

    T=T->left;

    free(Tmpcell);

    }

    return T;

    }

   node Findmin(node T)

   {

    if(T!=NULL)

     {

      if(T->left==NULL)

        return T;

      else

       return Findmin(T->left);

       }

    return(0);

    }

  void display(node T)

   {

    if(T!=NULL)

     {

      display(T->left);

      printf("%d\t",T->data);

      display(T->right);

      }

        }
