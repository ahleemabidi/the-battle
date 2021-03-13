# the-battle   SDL_Rect MAJMinimap( SDL_Rect posJoueur, int redimensionnement);
posJoueurABS.x = posJoueur.x + camera.x;
posJoueurABS.y = posJoueur.y + camera.y;
            posbonhomme.x=posJoueurABS.x * redimensionnement/100;
            posbonhomme.y=posJoueurABS.y * redimensionnement/100;
void afficher (minimap m, SDL_Surface *);
void Liberer (minimap *)
