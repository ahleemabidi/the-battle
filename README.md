# the-battle   SDL_Rect MAJMinimap( SDL_Rect posJoueur, int redimensionnement);
posJoueurABS.x = posJoueur.x + camera.x;
posJoueurABS.y = posJoueur.y + camera.y;
            posbonhomme.x=posJoueurABS.x * redimensionnement/100;
            posbonhomme.y=posJoueurABS.y * redimensionnement/100;
void afficher (minimap m, SDL_Surface *);
void Liberer (minimap *)
&edef struct maps
{
	SDL_Surface *calque;
	int speed_camera;
	SDL_Rect camera;
	int buttoncameraup;
	SDL_Surface *affichage_map;
int buttoncameradown;
int buttoncameraleft;
int buttoncameraright;

int mouvement_personnage;

}maps; 


typedef struct temps
{
	int heur1;
	int heur2;
	int minute1;
	int minute2;
	int seconde1;
	int seconde2;
	SDL_Surface *temp;
	SDL_Rect position_temp;
	TTF_Font *police;
	int tempactuel;
	int tempprecedent;
	char chaine[20];

	
}temps;

typedef struct rect_collision 
{

 int hauteur ; 
int largeur ; 
SDL_Rect position; 
} rect_collision;



//void initialiserennemi(ennemis *ennemi);
//void afficherennemi(ennemis *ennemi,SDL_Surface *ecran,SDL_Surface *background);
//ennemis MoveEnemy(ennemis e/*,SDL_Rect personnage */);
void initialiserperso(perso *p);
//void afficherperso(perso *p,SDL_Surface *ecran,SDL_Surface *background);
 /*perso*/void mouvement(perso p);
//int collision_Parfaite(SDL_Surface *calque , perso p ,int d);
//SDL_Color getpixel(SDL_Surface *surface,int x,int y);
//int  collision(SDL_Surface *obstacle, SDL_Rect *position_perso, SDL_Surface *img);
//int  collisionennemi(SDL_Rect *posperso,SDL_Rect *posenemi);
//void initialiserscore(score *score);
//void afficherscore(score *score , SDL_Surface *ecran,TTF_Font *police);
//void calculerScore(score *score,int d);
//void initialiservie(score *score);
//void affichervie(SDL_Surface *vie1,SDL_Surface *vie2,SDL_Surface *vie3 , SDL_Surface *ecran,SDL_Rect posvie); 
perso bouger( perso p);
void afficherperso(perso *p,SDL_Surface *ecran,SDL_Surface *background,maps map);
maps Initialiser_map (maps map);
temps inisaliser_temp (temps temp);
void afficher_tmp(temps temp,SDL_Color noir,SDL_Surface *ecran);
void affichevie(vie *v,SDL_Surface *ecran);
void initvie( vie *v);
int collision(perso *perso,maps map);
SDL_Color GetPixel (SDL_Surface* pSurface, int x, int y);
//void affenigme(enigme en,SDL_Surface *ecran,SDL_Surface *img);
enigme Init_Enigme();
char * Replace_Hyphen(char *str);
enigme Generate_Enigme(enigme e);
int Resolution(enigme e,int x);
void affichage_Enigme(enigme e,SDL_Surface *ecran);
int Collision_Bounding_Box (SDL_Rect rec1 ,SDL_Rect position_obstacle) ;
void initialiserennemi(ennemis *e);
ennemis MoveEnemy(ennemis e);
void afficherennemi(ennemis *ennemi,SDL_Surface *ecran,SDL_Surface *background);
int collision2entite(SDL_Surface *imgperso,SDL_Surface *imgennemi,SDL_Rect posperso,SDL_Rect posennemi);
void gestvie(vie *v,int c,perso *p);
temps inisaliser_temp (temps temp)
{
temp.heur1=0;
temp.minute1=0;
temp.seconde1=0;
temp.heur2=0;
temp.minute2=0;
temp.seconde2=0;
temp.tempactuel=0;
temp.temp=NULL;
temp.tempprecedent=0;
temp.position_temp.x=400;
temp.position_temp.y=0;
temp.police=TTF_OpenFont("arial.ttf",22);

	return temp;
}


/*void afficher_tmp(temps temp,SDL_Color noir,SDL_Surface *ecran)
{

temp.temp=TTF_RenderText_Blended(temp.police,temp.chaine,noir);

temp.tempactuel=SDL_GetTicks();

if (temp.tempactuel- temp.tempprecedent >1000  )
{
temp.seconde1++;
temp.tempprecedent= temp.tempactuel;

}
if (temp.seconde1>9)
{
	temp.seconde1=0;
	temp.seconde2++;
}
if (temp.seconde2>=6)
{
	temp.seconde2=0;
	temp.minute1++;
}
if (temp.minute1>=9)
{
	temp.minute1=0;
	temp.minute2++;
}
if (temp.minute2>=6)
{
	temp.minute2=0;
	temp.heur1++;
}
if (temp.heur1>=9)
{
	temp.heur1=0;
	temp.heur2++;
}






sprintf(temp.chaine,"%d %d : %d %d : %d %d ",temp.heur2,temp.heur1,temp.minute2,temp.minute1,temp.seconde2,temp.seconde1);

SDL_BlitSurface(temp.temp,NULL,ecran,&temp.position_temp);
}*/

SDL_Color GetPixel (SDL_Surface* pSurface, int x, int y)
{
    SDL_Color color;
    Uint32 col = 0 ;

    //determine position
    char* pPosition = ( char* ) pSurface->pixels ;

    //offset by y
    pPosition += ( pSurface->pitch * y ) ;

    //offset by x
    pPosition += ( pSurface->format->BytesPerPixel * x ) ;

    //copy pixel data
    memcpy ( &col, pPosition, pSurface->format->BytesPerPixel ) ;

    //convert color
    SDL_GetRGB ( col, pSurface->format, &color.r, &color.g, &color.b ) ;
    return ( color ) ;
}

int collision(perso *perso,maps map)
{
int i;
int decalage=1;
  SDL_Color col;
  if(perso->d==6)//ymin
  {
    col=GetPixel(map.calque,perso->position.x+perso->imager[0]->w+decalage+map.camera.x,perso->position.y+(perso->imager[0]->h)+map.camera.y);
  }
else  if(perso->d==4)//issar
  {
    col=GetPixel(map.calque,perso->position.x +decalage+map.camera.x,perso->position.y+(perso->imager[0]->h)+map.camera.y);
  }
else  if(perso->d==8)//lfou9
  {
    col=GetPixel(map.calque,perso->position.x+(perso->imager[0]->w/2)+decalage+map.camera.x,perso->position.y+map.camera.y);
  }
else  if(perso->d==2)//louta hahaha
  {
    col=GetPixel(map.calque,perso->position.x+(perso->imager[0]->w/2)+decalage+map.camera.x,perso->position.y+perso->imager[0]->h+map.camera.y);
  }
  printf("%d    %d   %d\n",col.r,col.b,col.g );
if ((col.r==255)&&(col.b==255)&&(col.g==255))
{
  i=1;
}
else i=0;


return i;
}
