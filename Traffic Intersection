#include <stdlib.h>
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
static const direction[]={'N','S','E','W'};
static const Turn[]={'L','R','S'};
static void straight(int, int);
static void leftturn(int, int);
static void rightturn(int, int);
static void * criticalsection(void*);
pthread_mutex_t NW ;
pthread_mutex_t NE ;
pthread_mutex_t SE ;
pthread_mutex_t SW ;
void lock(CAR, MUTEX) 
{do 
{         
if (pthread_mutex_lock(&MUTEX)) { 
printf("CAR %d is locked\n\n", CAR);     
} 
} while(0);
}
void unlock(CAR, MUTEX) 
{do 
{     
 if (pthread_mutex_unlock(&MUTEX)) { 
printf("CAR %d is unlocked\n\n", CAR);  
} 
} while(0);}
void intersection(){
	printf("------------Car is in Traffic Intersection------------\n\n");
}
static void straight(int carorigin, int cn){
if (carorigin==0){
lock(cn,NE);
lock(cn,SE);
printf("Car %d is moving from South to North\n\n", cn);
intersection();
unlock(cn,SE);
unlock(cn,NE);
}
else if (carorigin==1){
lock(cn,NW);
lock(cn,SW);
printf("Car %d is moving from North to South\n\n", cn);
intersection();
unlock(cn,SW);
unlock(cn,SW);
}
else if (carorigin==2){
lock(cn,SE);
lock(cn,SW);
printf("Car %d is moving from West to East\n\n", cn);
intersection();
unlock(cn,SW);
unlock(cn,SE);
}
else if (carorigin==3){
lock(cn,NW);
lock(cn,NE);
printf("Car %d is moving from East to West\n\n", cn);
intersection();
unlock(cn,NE);
unlock(cn,NW);
}
}
static void leftturn(int carorigin, int cn){
if(carorigin==0){
lock(cn,NE);
lock(cn,SE);
lock(cn,SW);
printf("Car %d is moving from South to West\n", cn);
intersection();
unlock(cn,SW);
unlock(cn,SE);
unlock(cn,NE);
}
else if(carorigin==1){
lock(cn,NW);
lock(cn,NE);
lock(cn,SW);
printf("Car %d is moving from North to East\n", cn);
intersection();
unlock(cn,SW);
unlock(cn,NE);
unlock(cn,NW);
}
else if(carorigin==2){
lock(cn,NW);
lock(cn,SE);
lock(cn,SW);
printf("Car %d is moving from West to North\n", cn);
intersection();
unlock(cn,SE);
unlock(cn,NE);
unlock(cn,NW);
}
else if(carorigin==3){
lock(cn,NW);
lock(cn,SE);
lock(cn,SW);
printf("Car %d is moving from East to South\n", cn);
intersection();
unlock(cn,SE);
unlock(cn,NE);
unlock(cn,NW);
}
}
static void rightturn(int carorigin, int cn){
if(carorigin==0){
lock(cn,NE);
printf("Car %d is moving from South to East\n", cn);
intersection();
unlock(cn,NE);
}
else if(carorigin==1){
lock(cn,SW);
printf("Car %d is moving from North to West\n", cn);
intersection();
unlock(cn,NE);
}
else if(carorigin==2){
lock(cn,SW);
printf("Car %d is moving from West to South\n", cn);
intersection();
unlock(cn,NE);
}
else if(carorigin==3){
lock(cn,SE);
printf("Car %d is moving from East to North\n", cn);
intersection();
unlock(cn,NW);
}
}
static void * criticalsection(void* arg){
int * carnumberptr;
int cn;
int carorigin = random()%4;
int turn = random()%3;
printf("Vehicle is Approaching intersection..\n\n");
printf("direction is %c and Turn is %c \n",direction[carorigin],Turn[turn]);
carnumberptr = (int*) arg;
cn = (int) *carnumberptr;
if(turn==0){
leftturn(carorigin, cn);
} else if(turn==1){
rightturn(carorigin, cn);
} else {
straight(carorigin, cn);
}
}
main()
{
	int n,i;
  	printf("+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++\n");
  	printf("               Traffic Intersection Problem                  \n");
  	printf("+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++\n");
  	printf("North :N\nSouth :S\nEast :E\nWest :W \n\n");
  	pthread_mutex_init(&NW,NULL);
  	pthread_mutex_init(&NE,NULL);
  	pthread_mutex_init(&SE,NULL);
  	pthread_mutex_init(&SW,NULL);
printf("Enter No Of Cars\n");
scanf("%d",&n);
int cid[n];
pthread_t c[n];
for(i = 0; i <n; i++)
{
cid[i] = i;
 pthread_create(&c[i], NULL, criticalsection,(void*)&cid[i]);
 sleep(1);
}
for(i=0;i<n;i++)
{
pthread_join(c[i],NULL);
}
}
