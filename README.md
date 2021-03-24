

typedef struct
{
SDL_Surface* imagemini;
SDL_Rect posmini;
SDL_Surface* imagenokta;
SDL_Rect posnokta;
}mini;



void init_positions(mini *e,int x,int y);
void init_positions1(mini *e,int x,int y);
void init_affich(mini *e,SDL_Surface* s);
void key_event (mini *e,SDL_Surface* s,int x);
void key_event1 (mini *e,SDL_Surface* s,int x);


void init_positions(mini *e,int x,int y)
{
e->posmini.x=x;
e->posmini.y=y;
e->posnokta.x=0;
e->posnokta.y=100;
}

void init_positions1(mini *e,int x,int y)
{
e->posmini.x=x;
e->posmini.y=y;
e->posnokta.x=550;
e->posnokta.y=100;
}

void init_affich(mini *e,SDL_Surface* s)
{
e->imagemini=IMG_Load("mini.png");
e->imagenokta=IMG_Load("nokta.png");
SDL_BlitSurface(e->imagemini,NULL,s,&e->posmini);
SDL_BlitSurface(e->imagenokta,NULL,s,&e->posnokta);
}


void key_event (mini *e,SDL_Surface* s,int x)
{

e->posnokta.x=x/14;
 SDL_BlitSurface(e->imagemini,NULL,s,&e->posmini);
 SDL_BlitSurface(e->imagenokta,NULL,s,&e->posnokta);
}
void key_event1 (mini *e,SDL_Surface* s,int x)
{

e->posnokta.x=550+x/14;
 SDL_BlitSurface(e->imagemini,NULL,s,&e->posmini);
 SDL_BlitSurface(e->imagenokta,NULL,s,&e->posnokta);
}


























