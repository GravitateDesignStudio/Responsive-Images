# Responsive-Images  with LazyLoad Option
Version 4.1.0  
Resizes Images based on Browser width

##How to Use##
Include the plugin from source.min.js into your project.  
* Requires jQuery

Then add the following to your project  
```
jQuery(document).ready(function($){
	$(this).responsiveImages();
});
```

With Options  (Defaults)

```
jQuery(document).ready(function($){
	$(this).responsiveImages({
		throttle: 100,
		downscale: false,
		downsize: false,
		onload: true,
		lazyload: true,
		lazyload_threshold: 100,
		sizes: [
			{
			    name: 'small',
			    size: 320
			},
			{
			    name: 'medium',
			    size: 500
			},
			{
			    name: 'medium_large',
			    size: 768
			},
			{
			    name: 'large',
			    size: 1024
			},
			{
			    name: 'xlarge',
			    size: 1440
			},
			{
			    name: 'full',
			    size: 99999
			}
		]
	});
});
```

On an Image  
Recommended to declare the smallest size as your src or use a data-uri filler to make sure the image fills out correctly and works properly with Lazyload.  
```  
<img 
src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==" 
data-rimg-small="1-small.jpg"   
data-rimg-medium="1-med.jpg"   
data-rimg-large="1-lrg.jpg"   
data-rimg-full="1-full.jpg"   
alt="" />
```
*(Tha data:image seen above is an extremely small image that may be needed as a placeholder to render the page layout correctly.)*

Background Image (If no full size is declared it will default to the closest size)    
```
<div   
data-rimg-small="1-small.jpg"   
data-rimg-medium="1-med.jpg"   
data-rimg-large="1-lrg.jpg">   
</div>
```

CSS Classes will be added to your elements  
* "rimg" - To all tags with the data-rimg-* attribute
* "rimg-lazy" - To all tags that are lazy loaded (below the fold) and when lazyload is enabled.
* "rimg-loaded" - Added after the image src is fully loaded.


##Throttling Browser Resize##
By default the resize throttling is set to 100 milliseconds. This reduces the lag when resizing the browser.
However, if you want the images to load much faster on resize then you can set this to 0 to turn off throttling or adjust it to a smaller number.  

##Onload##
You may want to set this to false.  When declaring your own srcs and don't want the script to run until the user resizes the browser or scrolls if Lazyload is enabled.

##Downscaling##
This will use the lower resolution image size instead of the higher resolution image size. Similar to floor() instead of ceil().  This may reduce bandwidth, but images may tend to be a bit more blury.

##Downsize##
If set to true then when resizing the window to smaller it will load the smaller images.  This can increase bandwidth, but may help with images looking crammed in smaller windows.

##LazyLoad##
This will prevent the images from loading unless they are close to the viewport.  Then they will be faded in.  This helps reduce network bandwidth when images are not needed to be displayed.

##LazyLoad Threshold##
This is the number of pixels from the viewport that images will start to load.  You can increase this to reduce flickering images when scrolling, but the higher the number the more images that will be loaded by default.


##Adding Effects on Lazyload##
CSS Fade Example:
```
.rimg-lazy {
	transition: opacity .5s ease-out;
	opacity: 0;
}
.rimg-lazy.rimg-loaded
{
	opacity: 1;
}
```

CSS Fade and Slide Up <img> tags Example:
```
.rimg-lazy {
	transition: all .5s ease-out;
	opacity: 0;
}
.rimg-lazy.rimg-loaded
{
	transform: translateY(0);
	opacity: 1;
}
img.rimg-lazy  {  /* Only slide up <img> tags and not other tags */
	transform: translateY(100px);
}
```
