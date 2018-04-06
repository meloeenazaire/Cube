# Cube

![install-eclipse-oxygen.jpg](https://github.com/meloeenazaire/Cube/blob/master/install-eclipse-oxygen.jpg)

Le but de cette application est d'afficher un cube 3D sur un marker papier, grâce à la librairie de réalité augmentée : 
**ARToolKit**

## Squelette du code
package org.artoolkit.ar.samples.ARSimple;

import org.artoolkit.ar.base.ARActivity;
import org.artoolkit.ar.base.rendering.ARRenderer;
import org.artoolkit.ar.samples.ARSimple.R;

import android.os.Bundle;

import android.widget.FrameLayout;

/**
 * A very simple example of extending ARActivity to create a new AR application.
 */
public class ARSimple extends ARActivity
{

	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);      
		setContentView(R.layout.main); 
	}
 
	/**
	 * Provide our own SimpleRenderer.
	 */
	@Override
	protected ARRenderer supplyRenderer()
	{
		return new SimpleRenderer();
	}
	
	/**
	 * Use the FrameLayout in this Activity's UI.
	 */
	@Override
	protected FrameLayout supplyFrameLayout()
	{
		return (FrameLayout)this.findViewById(R.id.mainLayout);    	
	}

}


![HIRO.png](https://github.com/meloeenazaire/Cube/blob/master/HIRO.PNG)
![cube.png](https://github.com/meloeenazaire/Cube/blob/master/cube.PNG)
