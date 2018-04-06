# Cube

![install-eclipse-oxygen.jpg](https://github.com/meloeenazaire/Cube/blob/master/install-eclipse-oxygen.jpg)

Le but de cette application est d'afficher un cube 3D sur un marker papier, grâce à la librairie de réalité augmentée : 
**ARToolKit**

## Squelette du code
### ARSIMPLE.JAVA
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

### SimpleRenderer
public class SimpleRenderer extends ARRenderer
{

	private int markerID = -1;
	private Cube cube = new Cube(40.0f, 0.0f, 0.0f, 20.0f);
	
	private boolean spinning = false;
	private float angle = 0.0f;

	/**
	 * Markers can be configured here.
	 */
	@Override
	public boolean configureARScene()
	{

		markerID = ARToolKit.getInstance().addMarker("single;Data/hiro.patt;80");
		if (markerID < 0) return false;

		return true;
	}
	
	public void click()
	{
		spinning = !spinning;
	}
	

	/**
	 * Override the draw function from ARRenderer.
	 */
	@Override
	public void draw(GL10 gl)
	{

		gl.glClear(GL10.GL_COLOR_BUFFER_BIT | GL10.GL_DEPTH_BUFFER_BIT);

		// Apply the ARToolKit projection matrix
		gl.glMatrixMode(GL10.GL_PROJECTION);
		gl.glLoadMatrixf(ARToolKit.getInstance().getProjectionMatrix(), 0);
	
		gl.glEnable(GL10.GL_CULL_FACE);
        gl.glShadeModel(GL10.GL_SMOOTH);
        gl.glEnable(GL10.GL_DEPTH_TEST);        
    	gl.glFrontFace(GL10.GL_CW);
    	
    	gl.glMatrixMode(GL10.GL_MODELVIEW);
    			
		// If the marker is visible, apply its transformation, and draw a cube
		if (ARToolKit.getInstance().queryMarkerVisible(markerID))
		{
			//gl.glMatrixMode(GL10.GL_MODELVIEW);
			gl.glLoadMatrixf(ARToolKit.getInstance().queryMarkerTransformation(markerID), 0);
			
			gl.glPushMatrix();
			
			gl.glRotatef(angle, 0.0f, 0.0f, 1.0f);
			
			cube.draw(gl);
			
			gl.glPopMatrix();
			
			if (spinning) angle += 5.0f;;
			
		}

	}



![HIRO.png](https://github.com/meloeenazaire/Cube/blob/master/HIRO.PNG)
![cube.png](https://github.com/meloeenazaire/Cube/blob/master/cube.PNG)
