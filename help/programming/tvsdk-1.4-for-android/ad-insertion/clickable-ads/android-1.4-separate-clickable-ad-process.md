---
description: Você deve separar a lógica da interface do seu player do processo que gerencia e clica. Uma maneira de fazer isso é implementar vários Fragmentos para uma Atividade.
seo-description: Você deve separar a lógica da interface do seu player do processo que gerencia e clica. Uma maneira de fazer isso é implementar vários Fragmentos para uma Atividade.
seo-title: Separe o processo de anúncio clicável
title: Separe o processo de anúncio clicável
uuid: 00537191-8997-418d-add2-8e86d818c76e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Separe o processo de anúncio clicável{#separate-the-clickable-ad-process}

Você deve separar a lógica da interface do seu player do processo que gerencia e clica. Uma maneira de fazer isso é implementar vários Fragmentos para uma Atividade.

1. Implemente um fragmento para conter o `MediaPlayer` e que será responsável pela reprodução do vídeo.

   Este fragmento deve chamar `notifyClick`.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implemente um fragmento diferente para exibir um elemento de interface que indica que um anúncio pode ser clicado, monitore esse elemento de interface e comunique os cliques do usuário ao fragmento que contém o `MediaPlayer`.

   Esse fragmento deve declarar uma interface para a comunicação do fragmento. O fragmento captura a implementação da interface durante seu método de ciclo de vida onAttach e pode chamar os métodos da interface para se comunicar com a Atividade.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
   
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container, Bundle 
                                savedInstanceState) { 
   
           // the custom fragment is defined by a custom button 
           viewGroup =  
             (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad, container, false); 
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

