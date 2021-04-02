#ifndef HEADER_H
#define HEADER_H
#include <stdlib.h>
#include <stdio.h>
#include "SDL/SDL.h"
#include <SDL/SDL_image.h>
#include <SDL/SDL_ttf.h>
#include <SDL/SDL_mixer.h>


typedef struct MINIMAP
{ 
SDL_Surface *line;
SDL_Surface *circle;
SDL_Rect positioncircle;
}MINIMAP;

typedef struct Temps
{
Uint32 temps;
} Temps;

typedef struct randomposition
{ 
int randomxstar[11],randomystar[11],randomxrock[11],randomyrock[11];
}randomposition ;
typedef struct Time {
	SDL_Surface *msg,*txt;
	TTF_Font *font;
	int time;
	SDL_Rect r;
	char timeString[10];

} Time;

void intialiser_maskgrav(BACKGROUND *mg);
SDL_Color GetPixel(SDL_Surface *bg,int x,int y);
int collision_background(BACKGROUND *back,perso *p );
void init_minimap(MINIMAP *mm);void afficher_minimap(MINIMAP *mm,SDL_Surface *screen);
void initializerTemps(Time *time);
void afficherTemps(Time *time, SDL_Surface **screen);
void jeu () ;


#endif 





SDL_Color GetPixel(SDL_Surface *bg,int x,int y)
{
 SDL_Color color;
Uint32 col=0;
char* pPosition=(char*) bg->pixels;
pPosition+=(bg->pitch*y);
pPosition+=(bg->format->BytesPerPixel*x);
memcpy(&col,pPosition,bg->format->BytesPerPixel);
SDL_GetRGB(col,bg->format,&color.r,&color.g,&color.b);
return (color);
}


int collision_background(BACKGROUND *back,perso *p )
{
    int x,y;
  SDL_Color ca;
  /**x=p->x +s->w/2+stage1.x;
  y=p->y +s->h;**/
x=p->positionpersonnage.x;
y=p->positionpersonnage.y;
  ca=GetPixel(back->mag,x,y);
        if((ca.r==255)&&(ca.b==255)&&(ca.g==255))
        {
           return 1;
        }
        else
        {
          return 0 ;
        }
}









int collision_object (perso *p,ENTITE_SECONDAIRE_object *o)
{
int collision=1;
if(p->positionpersonnage.x + p->positionpersonnage.w< o->positionobjet. x 
|| p->positionpersonnage.x> o->positionobjet. x + o->positionobjet. w
|| p->positionpersonnage.y + p->positionpersonnage.h< o->positionobjet. y 
|| p->positionpersonnage.y> o->positionobjet. y + o->positionobjet. h )
{
collision=0;
}
else{
collision=1;
}
return collision;
}


void init_minimap(MINIMAP *mm)
{
mm->line=IMG_Load("line.png");
mm->circle=IMG_Load("circle.png");
mm->positioncircle.x=0;
mm->positioncircle.y=0;
mm->positioncircle.h=1200;
mm->positioncircle.w=1200;

}

void afficher_minimap(MINIMAP *mm,SDL_Surface *screen)
{SDL_BlitSurface( mm->line,NULL,screen,NULL);
SDL_BlitSurface( mm->circle,NULL,screen,&mm->positioncircle);
}


void loadFont()
{TTF_Font *font ;
TTF_Init();
    if(TTF_Init()==-1)
    {
        fprintf(stderr,"ERREUR INIT: %s \n",TTF_GetError());
        exit(EXIT_FAILURE);
    }
	font = TTF_OpenFont("angelina.TTF", 56);
	if (font == NULL)
        {
	printf("Can not to open Font : %s\n", TTF_GetError());
		exit(1);
	}
}


void initializerTemps(Time *time)
{
	time->font = TTF_OpenFont("angelina.TTF", 18);
	
	sprintf(time->timeString,"TIME: 00:00:00");
	//sprintf(time->scoreString,"SCORE: 0000");
	SDL_Color color = {255,255,255};
	SDL_Color color2 = {255,255,255};
	time->msg = TTF_RenderText_Shaded(time->font,time->timeString,color,color2);
	//time->txt = TTF_RenderText_Solid(time->font,time->scoreString,color);
}

void afficherTemps(Time *time, SDL_Surface **screen)
{
	SDL_Color color = {255,255,255};
	SDL_Color color2 = {255,208,119};
	SDL_Rect r;
	r.x=100;
	r.y=0;
       r.w=350;
	r.h=550;
	
      		
	time->time+=100;
	//time->score+=2;
	if(time->time % 60 == 0)
        {
		sprintf(time->timeString," %d:%d:%d\n",time->time/60/60/60,time->time/60/60,(time->time/60)%100);
		time->msg = TTF_RenderText_Shaded(time->font,time->timeString,color,color2);
		/*if((time->time /60/60 %5)==0)
		{
			
			sprintf(time->scoreString,"SCORE: %02d%02d\n",time->score/100,time->score%100);
		time->txt = TTF_RenderText_Solid(time->font,time->scoreString,color2);
	         }*/
        }
	SDL_BlitSurface(time->msg,NULL,*screen,&r);
	
}


}
}
ttttttttttttttttttttttttttttttttttttttttttttttttttt maiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiin hahaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa





#include <stdlib.h>
#include <stdio.h>
#include "SDL/SDL.h"
#include <SDL/SDL_image.h>
#include <SDL/SDL_ttf.h>
#include <SDL/SDL_mixer.h>
#include "fonction.h"

void jeu () {
SDL_Surface *screen;
SDL_Surface *OPTION;
SDL_Surface *on;
Time time;
SDL_Rect positionOPTION,positionobjett;


ENTITE_SECONDAIRE_object o;
int cont=1;int per=1;
screen= SDL_SetVideoMode(350,550,32,SDL_HWSURFACE | SDL_DOUBLEBUF);
if (screen==NULL){
printf("Unable to set video mode:%s\n",SDL_GetError());
return(-1);
}
OPTION=IMG_Load("option.png");
if (OPTION==NULL){
printf("Unable to load bitmap:%s\n",SDL_GetError());
return 1;
}
BACKGROUND back;
//          

int directionSDL;

//
randomposition rp;
MINIMAP mm;
init_minimap(&mm);
init_pos(&rp);


initializerTemps(&time);

afficher_minimap(&mm,screen);

//collision_object (&hero,&o);
//collision_star (&hero,&s);
//gest_vie (v/*,&hero,&o*/);
afficherTemps(&time,&screen);
calculate(score,&back);
DrawScore(screen,score);
SDL_Flip(screen);
SDL_Delay(15);
scrolling(&back,&mm,&s);
}//while vie
closeFont();
SDL_FreeSurface(back.f);
SDL_FreeSurface(screen);
return 0;
}











































