---
description: Você deve separar a lógica da interface do usuário do seu reprodutor do processo que gerencia os cliques de anúncio. Uma maneira de fazer isso é implementar vários fragmentos para uma atividade.
title: Separe o processo de anúncio clicável
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Separe o processo de anúncio clicável {#separate-the-clickable-ad-process}

Você deve separar a lógica da interface do usuário do seu reprodutor do processo que gerencia os cliques de anúncio. Uma maneira de fazer isso é implementar vários fragmentos para uma atividade.

1. Implemente um fragmento para conter o `MediaPlayer`.

   Esse fragmento deve chamar `notifyClick()` e será responsável pela reprodução do vídeo.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implemente um fragmento diferente para exibir um elemento da interface do usuário que indica que um anúncio é clicável, monitorar esse elemento da interface do usuário e comunicar os cliques do usuário ao fragmento que contém o `MediaPlayer`.

   Esse fragmento deve declarar uma interface para comunicação de fragmento. O fragmento captura a implementação da interface durante seu método de ciclo de vida `onAttach()` e pode chamar os métodos da interface para se comunicar com a atividade.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container,  
                                Bundle savedInstanceState) { 
           // the custom fragment is defined by a custom button 
           viewGroup = (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad,  
                                                    container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);     
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
                   + " must implement OnAdUserInteraction"); 
           }     
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```
