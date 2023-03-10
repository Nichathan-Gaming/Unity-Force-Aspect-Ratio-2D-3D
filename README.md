# Unity Force Aspect Ratio 2D/3D
A detailed tutorial by John of Nichathan Gaming on how to force your desired aspect ratio on a camera in Unity.

If you enjoy my tutorial, please support me by : 
- Subscribing to my [YouTube](https://www.youtube.com/@nichathangaming) channel, and watching/liking my videos.
- Downloading my [Google Play](https://play.google.com/store/apps/dev?id=5505294983591200024) games and giving them 5*'s and constructive comments.

## Table of Contents
1. **[Initial Setup and Details](#Initial-Setup-and-Details)**
   1. **[Disclaimer](#Disclaimer)**
   2. **[Before continuing you should have](#Before-continuing-you-should-have)**
   3. **[Relevant Links](#Relevant-Links)**
2. **[Instructions](#Instructions)**
   1. **[Scene Setup](#Scene-Setup)**
   2. **[Steps](#Steps)**
   3. **[Final Result](#Final-Result)**

## Initial Setup and Details
### Disclaimer
To the best of my knowledge, this tutorial and all content inside of it has been typed with no errors or misinformation. That being said, neither I, nor Nichathan Gaming owns, has affiliation to, or any form of control over Unity. All information in this tutorial is subject to become obsolete at any moment and there are no guarantees that anything inside of this tutorial will work. By continuing to follow this tutorial, you understand that neither Johnathan Nichols nor Nichathan Gaming are responsible for whatever may happen. That being said, I put a lot of time and effort into this walkthrough and I sincerely hope that it can help you.
</br>**[Back To Top](#Table-of-Contents)**

### Before continuing, you should have :
- The latest [Unity Editor](https://unity.com/download)
- Some assets loaded into a project to follow along.
</br>**[Back To Top](#Table-of-Contents)**

### Relevant Links
- [YouTube Video Tutorial](https://www.youtube.com/watch?v=xZdW-avT5UA)
- [The Unity learn tutorial that supported this tutorial](https://learn.unity.com/tutorial/5c5151b9edbc2a0020694df6)
- [The forum post that inspired this tutorial](https://forum.unity.com/threads/how-do-i-force-the-game-to-run-at-a-given-aspect-ratio.1258797/)
</br>**[Back To Top](#Table-of-Contents)**

### Issue Details
When dealing with scenes in Unity, they look great in the aspect ratio that they were developed for.
**Example 1**
</br>![ex1](https://user-images.githubusercontent.com/103794085/222946804-57dbfa74-7f70-42fe-a1de-cb7769d998bf.png)

However, when the aspect ratio of the screen is changed, even a small amount, your camera will start cutting out important details, or showing parts of the screen that the developers don't wish to show. 
**Example 2**
</br>![ex2](https://user-images.githubusercontent.com/103794085/222946929-78848e32-3955-4b67-b790-4c1d7fcce7ee.png)

I have dealt with this issue by placing assets onto a canvas in the past and avoid using a Sprite Renderer in the past. Yet, this issue has still been a large hurdle for myself and many other Unity users. Furthermore, it is heartwrenching to see [Unity employees](https://forum.unity.com/threads/how-do-i-force-the-game-to-run-at-a-given-aspect-ratio.1258797/#post-8004821) belitle users for wanting a solution to this issue. I am appauled that behavior shown by employees on the forum can be accepted. Adding emoji does not make an insult any less hurtful.
</br>**[Back To Top](#Table-of-Contents)**

## Instructions
### Scene Setup
To Get this tutorial started, I will introduce you to the scene that I am working in. I will be using demo assets from an upcoming Nichathan Gaming infinite Runner game. 

In my starter scene, I have a [main camera](https://docs.unity3d.com/ScriptReference/Camera-main.html), 2 [Sprite Renderer](https://docs.unity3d.com/ScriptReference/SpriteRenderer.html) objects *which I wish to always have on camera*, a [Canvas](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UICanvas.html) with 4 [buttons](https://docs.unity3d.com/ScriptReference/UIElements.Button.html) for gameplay, an [EventSystem](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/EventSystem.html) and a GameController which has a script to control the canvas buttons.

- The Main Camera will be connected to the canvas and used to display our GUI and eventually our RawImage which will display our game area.
- The 2 Sprite Renderer objects are my game objects which will be used in my gameplay.
- The Event System and GameController objects are necessary to run functions when a button is clicked but they are not necessary for this tutorial.

**Hierarchy**
</br>![image000](https://user-images.githubusercontent.com/103794085/222947245-89367d7f-19ef-4c99-b9dd-cdda311e2767.png)

**Main Camera Settings**
</br>![image001](https://user-images.githubusercontent.com/103794085/222947596-c778ea63-903b-4aef-b6d4-d265125c3a9b.png)

**Canvas Settings**
</br>![image002](https://user-images.githubusercontent.com/103794085/222947633-36be9006-fecc-44c1-9fb3-99bf4b11535e.png)
</br>**[Back To Top](#Table-of-Contents)**

### Steps
The first step that we must take is to add a new display layer to our game. *It is perfectly fine to use a default layer as long as you can remove it from the **Main Camera** Culling Mask.*

I have added a layer called "GameLayer" which I will use to display my game objects on my camera.

**Add Layer**
</br>![image003](https://user-images.githubusercontent.com/103794085/222947825-462d1a4a-d128-426b-bdb8-4f27076ab13b.png)
</br>![image004](https://user-images.githubusercontent.com/103794085/222947858-0461bb14-5e34-416e-a8d4-c809276b0927.png)

Now that I have my new layer, I will unselect it from my **Main Camera** Culling Mask, then I will set my game objects layer to "GameLayer".

</br>**Unselect From Main Camera**
</br>![image005](https://user-images.githubusercontent.com/103794085/222948040-d039fd77-7c41-42ed-a6e8-226d2d680dde.png)
</br>**Set as the Layer on the Game Objects**
</br>![image006](https://user-images.githubusercontent.com/103794085/222948079-fa1ae80c-0505-4e8e-a145-cb99b33fefc0.png)
 
Now, the game objects should no longer appear on the **Main Camera** and Game window.

</br>**Before Layer Switch**
</br>![image007](https://user-images.githubusercontent.com/103794085/222948210-4c593899-e471-4fc4-8c80-33b76fe83fd5.png)
</br>**After Layer Switch**
</br>![image008](https://user-images.githubusercontent.com/103794085/222948252-59a20229-8b82-4265-98d8-7468c6a249b4.png)

Our next step is to add a new Camera to our Hierarchy.

**Adding a Camera**
</br>![image009](https://user-images.githubusercontent.com/103794085/222948391-3146561e-93c2-400c-8427-b136dd4dfa89.png)

When we have our new camera, we want to change some of the settings. I will change many settings to fit my game, however the only important changes are to have the new Camera Culling Mask only render the layer our Game Objects are on and to change the Target Display to an unused Display.

</br>**Camera Default Values**
</br>![image010](https://user-images.githubusercontent.com/103794085/222948495-6cc0ad5f-05e4-45ed-9f75-70857588ac04.png)
</br>**Set the Culling Mask**
</br>![image011](https://user-images.githubusercontent.com/103794085/222948521-b22f36de-4f48-456c-a4f1-c01404f28989.png)
</br>**Set the Target Display**
</br>![image012](https://user-images.githubusercontent.com/103794085/222948688-217344b2-bba9-42ab-b4c8-d44843f5ac08.png)
</br>**My Camera's Final Settings**
</br>![image013](https://user-images.githubusercontent.com/103794085/222948590-d1cbc09f-e37c-4d86-bfd7-08949743dd7b.png)

Now that we have our new camera, we need a [Render Texture](https://docs.unity3d.com/Manual/class-RenderTexture.html) for it to display onto. To create a new Render Texture, right click in your Project->Assets folder, go to Create and Render Texture.

**Create a Render Texture**
</br>![image014](https://user-images.githubusercontent.com/103794085/222948839-fd4637e2-89bd-4105-a93b-17be9240a30c.png)

On the Render Texture, we need to set the Size to the dimensions that we want our camera to be. I will be using the 16x9 ratio of 3200x1800 since I am making this for the Google Play Store which uses a 16x9 ratio. I have changed my Filter Mode to Point as well but I recommend playing with the setting to see which, if any displays your assets best.

**Set Render Texture Values**
</br>![image015](https://user-images.githubusercontent.com/103794085/222949009-faf462e5-016b-463a-a15b-3e35b1238d1b.png)

Now that we have a Render Texture, we want to assign it to our Camera Target Texture.

**Add the Render Texture to the Camera Target Texture**
</br>![image016](https://user-images.githubusercontent.com/103794085/222949079-02000614-e24b-4332-80f7-dfaf88095b9a.png)
</br>**Added Texture**
</br>![image017](https://user-images.githubusercontent.com/103794085/222949133-871314e5-ac79-4646-b361-e7b013975d65.png)

After we have our Render Texture added to our new Camera, we should be able to see what the camera see's in our Render Texture.

**Example of scene view in Render Texture**
</br>![image018](https://user-images.githubusercontent.com/103794085/222949245-e032c727-9323-4e1b-aa5c-aeb9a1f25b0e.png)

Our next step is to add a new empty GameObject to our Canvas. This GameObject will contain a RawImage which is used to display our Render Texture.

**Adding a Game Object to the Canvas**
</br>![image019](https://user-images.githubusercontent.com/103794085/222949325-3947c9ef-0433-45b7-bc7f-0147d15091b0.png)
</br>**Rect Transform of the new Game Object**
</br>![image020](https://user-images.githubusercontent.com/103794085/222949408-54f9c1f4-7cac-4935-9dc2-db959b943fc6.png)

With our new GameObject created, we will want to add a [RawImage](https://docs.unity3d.com/2018.3/Documentation/ScriptReference/UI.RawImage.html) to it.

**Adding a Raw Image to the new Game Object**
</br>![image021](https://user-images.githubusercontent.com/103794085/222949467-b7bde23f-9545-49ea-a624-4443dd075079.png)

With the new Raw Image, I highly recommend setting the Rect Transform to a set Width/Height instead of using a Stretch Anchor Preset. We also need to add the Render Texture that we added to our new camera to the Raw Image that we just created. *If you add a Stretch Anchor Preset, then the camera displayed on your RawImage will stretch or contract with different screen sizes in a single direction instead of scaling up or down in both directions.*

**Adding the Render Texture and setting the Rect Transform of the new Raw Image**
</br>![image022](https://user-images.githubusercontent.com/103794085/222949756-dc001ad7-d4a6-426b-9fe3-484a8b668c89.png)

With that last step, we are finally done!
</br>**[Back To Top](#Table-of-Contents)**

### Final Result
**Before adding steps**
</br>![ex2](https://user-images.githubusercontent.com/103794085/222946929-78848e32-3955-4b67-b790-4c1d7fcce7ee.png)
</br>**Thin Screen Result**
</br>![image023](https://user-images.githubusercontent.com/103794085/222949839-7412baba-2d33-44ee-8023-6fdc458331ca.png)
</br>**Wide Screen Result**
</br>![image024](https://user-images.githubusercontent.com/103794085/222949869-19a180fa-186d-4d02-b88e-afe681a3c794.png)
</br>**[Back To Top](#Table-of-Contents)**
