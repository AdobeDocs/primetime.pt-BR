---
description: Você deve separar a lógica da interface do usuário do player do processo que gerencia os cliques de anúncio. Uma maneira de fazer isso é implementar vários fragmentos de uma atividade.
title: Separe o processo de anúncio clicável
exl-id: 9b6fad9b-d46d-4965-8770-0bb85c052e0e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Separe o processo de anúncio clicável {#separate-the-clickable-ad-process}

Você deve separar a lógica da interface do usuário do player do processo que gerencia os cliques de anúncio. Uma maneira de fazer isso é implementar vários fragmentos de uma atividade.

1. Implementar um fragmento para conter a variável `MediaPlayer`.

   Este fragmento deve chamar `notifyClick()` e serão responsáveis pela reprodução do vídeo.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implemente um fragmento diferente para exibir um elemento da interface do usuário que indique que um anúncio é clicável, monitore esse elemento da interface do usuário e comunique os cliques do usuário para o fragmento que contém o `MediaPlayer`.

   Esse fragmento deve declarar uma interface para comunicação de fragmento. O fragmento captura a implementação da interface durante sua `onAttach()` ciclo de vida e podem chamar os métodos de interface para se comunicarem com a atividade.

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
