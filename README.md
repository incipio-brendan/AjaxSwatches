# Wigman AjaxSwatches

### version
0.2.0

### 1. Adding Ajax functionality to the product-list pages (categories) to speed up the initial page load.
In cases where you have many product-options this can speed up the pageload 10 times!

If you have many colors/swatches in your RWD shop, you need this.

More info on this functionality here, with a test-case: http://e-tailors.nl/ajaxswatches-extension/



### 2. Adding Ajax functionality on product-view pages to Magento's RWD color swatches to switch all gallery images

DEMO: http://staging.e-tailors.nl/magentodemo/121-170-ladies-wallet-chamonix.html

This Module adds an Ajax event to the new ColorSwatches in Magento 1.9.1.0
When the event ConfigurableMediaImages.updateImage fires up, the original updateImage() function is executed.
After this we make an AJAX request to [baseurl]+'ajaxswatches/ajax/update' requesting the MediaGallery images.

The ID used to fetch the MediaGallery uses the original code from the RWD theme:

	var select = $j(el);
	var label = select.find('option:selected').attr('data-label');
	var productId = optionsPrice.productId;
	        
	var pid = ConfigurableMediaImages.productImages[productId].option_labels[label].products[0];
	

Once we've retrieved the new MediaGallery images, we remove the old thumbs and large images (for the sake of memory consumption). We might argue that it would be better to keep the downloaded images, but I chose to remove them. Second time you load the images it *should* come from browser-cache anyway.

The whole code is pretty simple and does not touch any default code. All extra images are loaded after clicking the ColorSwatches, so no extra load on page-render.