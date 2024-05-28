#include<stdio.h>
#define MAX 20
int nv;
struct vertex{
        char color;
        int d;
        int pi;
}V[MAX];
int Q[MAX];
int front=0,rear=-1;
void BFS(int [][8],int);
void printpath(int,int);
void enqueue(int);
int dequeue();
void main(){
        int G[8][8];
        int s,i,j,end;
        printf("Enter the number of vertices:\n");
        scanf("%d",&nv);
        printf("Enter the graph:\n");
        for(i=0;i<nv;i++){
                for(j=0;j<nv;j++){
                        scanf("%d",&G[i][j]);
                }
        }
        printf("Enter the starting vertex:\n");
        scanf("%d",&s);
        BFS(G,s);
        printf("Enter the destination vertex:\n");
        scanf("%d",&end);
        printf("PATH:\n");
        printpath(s,end);
}
void enqueue(int x){
        if(rear==MAX-1){
        }
        else{
                rear=rear+1;
                Q[rear]=x;
        }
}
int dequeue(){
        int u;
        if(rear<front){
                printf("Overflow\n");
        }
        else{
                u=Q[front];
                front=front+1;
                return u;
        }
}
void BFS(int G[8][8],int s){
        int i,j,u,k;
        for(i=0;i<nv;i++){
                if(i==s){
                }
                else{
                        V[i].color='W';
                        V[i].d=999999;
                        V[i].pi=-1;
                }
        }
        V[s].color='G';
        V[s].d=0;
        V[s].pi=-1;
        enqueue(s);
        while(front <= rear){
                u=dequeue();
                for(k=0;k<nv;k++){
                        if(G[u][k]==1){
                                if(V[k].color=='W'){
                                        V[k].color='G';
                                        V[k].d=V[u].d+1;
                                        V[k].pi=u;
                                      enqueue(k);
                                }
                        }
                }
                V[u].color='B';
        }
}
void printpath(int s,int e){
        if(s==e){
                printf("%d ",s);
        }
        else{
                if(V[e].pi==-1){
                        printf("Path not found\n");
                }
                else{
                printpath(s,V[e].pi);
                printf("--->%d",e);
                }
        }
}

lab3@pc11120:~/21bced29/lab10$ vi problem1.c
lab3@pc11120:~/21bced29/lab10$ cc problem1.c
lab3@pc11120:~/21bced29/lab10$ ./a.out
Enter the number of vertices:
7
Enter the graph:
0 1 1 0 0 0 0
1 0 1 1 0 0 0
1 1 0 0 0 1 0
0 1 0 0 1 0 0
0 0 0 1 0 1 1
0 0 1 0 1 0 0
0 0 0 0 1 0 0
Enter the starting vertex:
1
Enter the destination vertex:
4
PATH:
1 --->3--->4
