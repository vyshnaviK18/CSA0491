#include<semaphore.h>
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<pthread.h> 
sem_t a,b;
pthread_t tid;
pthread_t writerthreads[100],readerthreads[100]; //initialized thread 
int readercount = 0;

void *reader(void* param) //reading the file
{
   sem_wait(&a); //semaphore function
   readercount++;  //reader count
   if(readercount==1)
       sem_wait(&b);
   sem_post(&a);
   printf("%d reader is inside the critical section\n",readercount);
   usleep(3);
   sem_wait(&a);
   readercount--;
   if(readercount==0)
   {
       sem_post(&b);
   }
   sem_post(&a);
   printf("%d Reader is leaving the section\n",readercount+1);
   return NULL;
}

void *writer(void* param) //writing into the file
{
   printf("Writer is requesting to enter in the citical section\n");
   sem_wait(&b);
   printf("Writer has entered in the citical section\n");
   sem_post(&b);
   printf("Writer is leaving from the critical section\n");
   return NULL;
}
//driver code
int main()
{
   int a2,i;
   printf("Enter the number of readers:");
   scanf("%d",&a2);
   printf("\n");
   int n1[a2];
   sem_init(&a,0,1);
   sem_init(&b,0,1);
   for(i=0;i<a2;i++)
   { //Thread is running Simultaneously
       pthread_create(&writerthreads[i],NULL,reader,NULL);
       pthread_create(&readerthreads[i],NULL,writer,NULL);
   }
   for(i=0;i<a2;i++)
   {
       pthread_join(writerthreads[i],NULL);
       pthread_join(readerthreads[i],NULL);
   }

}
