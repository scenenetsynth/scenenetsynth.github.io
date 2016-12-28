Last month saw  celebrated release of OpenAI universe, DeepMindLabs and TorchCraft from OpenAI, DeepMind and Facebook AI Research (FAIR). All of them are heavily investing on synthetic environments to develop and understand general intelligence systems that are on par or able to beat humans in such settings. Synthetic and gaming environments are appealing, with interest galvanised by the pioneering work of DeepMind in 2014, as they allow to factor out any chaos which might be present in the real world and provide simplified rulebook to interact, navigate and play. Moreover, built with a reward in the form of success or failure upon completing a task, they provide a natural way to measure and quantify performance and in a long-term intelligence, something that is a lot harder to do in real world. However, the hope is that experiments in synthetic environments will enlighten us to develop systems.


* Talk about what is SceneNet and what is new with SceneNet RGB-D.
* Raytracing - what is it? Why do we need it? What are the best ray tracers today and list each one of them with their limitations and benefits. Photon Mapping and why is it interesting? 
* Talk about camera response function, motion blur, lighting.
* How such images are going to be useful?


##What is SceneNet?

##What is photon mapping?
When light reaches a surface, it will bounce or get transmitted in a way that is dependent on the surface: given an incoming light direction and wave length, it is possible to determine the amount of light received in any outgoing direction. This mapping is called the surface's BRDF (Bidirectional Reflectance Distribution Function). It assumes the ray will come out of the same point it reached the surface (no successions of micro bounces caused it to leave the surface at another point).

In traditional backwards ray tracing it is not practical to simulate diffuse bounces (when the ray leaves the surface in a random direction), simply because the lights rays are traced backwards (from the eye to the light). This makes ray tracing limited in the images it can produce. Any effect that involves a diffuse bounce before the light reaches the eye is not possible in standard ray tracing. Light rays have to be sent from both the eye and the light.

Photon mapping is an elegant way to solve this: before any standard raytracing is done, light (discretized as "photons") is sent from the light sources in the scene and allowed to bounce around, then stored in a "photon map". The photon map stores final positions of the photons as well as color and incoming direction. After the map is built, standard raytracing is done, and for each bounce the photons near the location of the bounce are essentially treated as small light sources. This allows to "complete" light paths that would not normally be considered. Photon maps are usually implemented using a kd-Tree (a form of axis aligned BSP-tree), to allow fast retrieval of neighbors around a point.

~~~c
for each pixel do
	compute ray for that pixel
	for each object in the scene do
		if ray interesects objects and is the nearest intersection so far then
		record intersection distance and object colour
		
	set pixel colour to nearest object colour
~~~


##