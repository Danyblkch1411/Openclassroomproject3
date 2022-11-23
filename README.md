# Openclassroomproject3


. Boutons 
● Au survol, la couleur de fond des boutons principaux devra légèrement s’éclaircir. L’ombre portée devra également être plus visible.

fichiers scss → Bouton.scss

class : Button

a/ Bouton réalisé avec la classe button 
.button {
      border: none;
      color: white;
      padding: 20px 34px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 20px;
      margin: 4px 2px;
      cursor: pointer;
      border-radius: 25px;
      @include dégradé($purple-color,$purple-dark-color); 
    }

b/ éclaircissement couleur de fond au hover --> Utilisation de 2 mixin  dégradé  shadow

   .button:hover  { 
         @include dégradé(lighten($purple-color,10%), lighten($purple-dark-color,10%)); 
        @include shadow(0, 5px, 5px, rgb(0, 0, 0,.5));
 
    }

 mixin  dégradé  violet clair  →    violet foncé
@mixin dégradé($from, $to) { 
  /* Couleur de secours pour les vieux navigateurs */
  background-color: $to;
  background-image: linear-gradient(to bottom, $from, $to);
}

 mixin  shadow création ombre

    @mixin shadow($x, $y, $blur, $color) {
      -webkit-box-shadow: $x $y $blur $color;
      -moz-box-shadow:$x $y $blur $color; 
      box-shadow: $x $y $blur $color; }


	.  "J’aime" en forme de cœur Boutons, Sauvegarde du  menus préférés,  
 ● au survol  faire  apparaître un coeur

fichiers scss → coeur.scss

container : .hearthStars

class :


a/ Encapsulation de 2 icones dans 
    .hearthStars {

      height: 25px;
      width: 25px;
      position: relative;
      cursor: pointer;
    }

    .hearthStars i:nth-child(1) {
     position: absolute;
      top: 15px;
      right:4px;
      
    }

    .hearthStars i:nth-child(2) {
     position: absolute;
     top: 15px;
     right:4px;
      display: none;
    } 
  
   
b/ lors du hover .hearthStars  icône 1 caché au profit de  icône 2, icône 2 passe  au violet vià mixin animation  PurpleHeart.

.hearthStars:hover {

  i:nth-child(1) {
   display: none;
  }

  i:nth-child(2) {
   display: inline;
   @include PurpleHeart;
 }
} 



c/ mixin animation  PurpleHeart
       @mixin PurpleHeart {

        animation: affPurpleHeart;
        animation-duration: 3s;
        animation-fill-mode: forwards;
  

  
        @keyframes affPurpleHeart {
  
          0%{
            opacity:0;
      
          }
          
         100%{
            opacity:1;
            color: $purple-dark-color;
          }  
      } 
  
    } 

Page d’accueil  Loader

 ● aperçu de la fonction “loading spinner” sera nécessaire : pendant 1 à 3 secondes quand on arrive sur la page d'accueil, couvrir l'intégralité de l'écran, et utiliser les animations CSS (pas de librairie).
 Le design de ce loader n’est pas défini, toute proposition est donc la bienvenue tant qu’elle est cohérente avec la charte graphique du site. 

fichiers scss : loader.scss
container : containerLoader, .itemLoader, .affOhmyfood 

a/ Encapsulation de 3 éléments .item1 .item2 .item3 de la  class itemLoader 

.containerLoader {
  position: absolute;
  top:30%;
  left:50%;
  transform: translate(-50%, -50%);
  display: flex;
  gap: 15px;
}

.itemLoader {
  max-width: max-content;
  height: max-content;
  border-radius: 50%;
  margin: 10px;
}

b/ animation des éléments  .item1 .item2 .item3 de la  class itemLoader 
translation sur axe y avec l'animation loader
.item1 {
  background-color: $primary-color;
   animation: loader 20 0.3s alternate;

}

.item2 {
  background-color: $secondary-color;
    animation: loader 20 0.3s 0.05s alternate;

}
.item3 {
  background-color: $third-color;
  animation: loader 15 0.3s 0.1s alternate;

}


@keyframes loader {
  100% {
    transform: translateY(-30px)
  }
}

c/ section affOhmyfood est affichée 3 secondes après → fait appel à l'animation Print 

.affOhmyfood {

  opacity: 0;
  animation: print;
  animation-delay: 3s;
  animation-duration: 3s;
  animation-fill-mode: forwards;
} 

@keyframes print {

  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}




Pages de menu
 ● Apparition progressive des plats à l’arrivée sur la page, avec un léger décalage dans le temps. Ils pourront soit apparaître un par un, soit par groupe “Entrée”, “Plat” et “Dessert”.
 
Solution : MenuAnimation.scss
container : menuCard

vià animation couleur

a/ chaque élément  .menuCard:nth-child(n) est en opacity 0


       .Menu__cardGroup .menuCard:nth-child(1) {
           animation-name: couleur; 
            animation-fill-mode: forwards; 
            animation-duration: 3s;
        } 

.Menu__cardGroup .menuCard {
    opacity:0;
}

couleur : au sein de chaque menu est fait appel à l'animation couleur :
b/ rend visible menuCard:nth-child(n) 1s  après le précédent 
en 3s :
c/ le positionne  à 10 px sur l'axe des y
d/ puis le fait remonter, une translation à 0 sur l'axe des y 


@keyframes couleur {

    0% {
        opacity: 0;
        transform: translateY(10px); 
    }

    100% {
 
        background: $white-color;
        transform: translateY(0px); 
        opacity: 1;
    }

}



        .Menu__cardGroup .menuCard:nth-child(2) {
             animation-name: couleur; 
             animation-fill-mode: forwards; 
             animation-duration: 3s;
             animation-delay: 1s;
          } 



        .Menu__cardGroup .menuCard:nth-child(3) {
               animation-name: couleur; 
              animation-fill-mode: forwards;
              animation-duration: 3s;
              animation-delay: 2s; 
          } 


          .Menu__cardGroup .menuCard:nth-child(4) {
            animation-name: couleur; 
           animation-fill-mode: forwards;
           animation-duration: 3s;
           animation-delay: 3s;
       }        


● Apparition d' une petite coche à droite du plat.
 Cette coche devra coulisser de la droite vers la gauche.



Solution : menu.scss



container : MenuCard → animIcon → Icon 

a/ Icon  opacity 0 et animIcon  width : 0px  

.Icon{
  opacity:0;
  color:  $white-color;
} 



b/ hover Icon  opacity 1, transition rotation sur 360 degré  et animIcon  width : 80px  

.menuCard:hover {

  .animIcon {

    width: 80px;
    }

  .Icon {
    opacity:1;
    transform-origin: center; 
     transform: rotate(360deg);
     transition-duration: 2s;
   
   }

}

  
.animIcon  {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 0;
  height:  auto;
  background-color:  $green-color;
  transition: 0.5s;

}

.decalPrice  {
   /* position:relative; */
    display: flex;
    justify-content: flex-end;
}




● Si l’intitulé du plat est trop long, il devra être rogné avec des points de suspension.

Solution : menu.scss


class : utilisation de la syntaxe  {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  }
 sur les classes contenant du texte :
.menuCard__details_NamePrice-name et .menuCard__details_NamePrice-subname


