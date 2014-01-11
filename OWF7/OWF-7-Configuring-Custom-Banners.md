# Custom Banner

Developers can use OwfConfig.groovy to add custom headers and footers to the OWF interface. Headers display at the top of the page. Footers display directly above the absolute bottom of the page.  

#1 Configuring Custom Banners
To configure the feature set the owf.customHeaderFooter  elements of the OwfConfig.groovy configuration file as shown below:  

    owf {
           // Optional Configuration elements for custom headers/footers 
       	customHeaderFooter {
    		header = 'location/within/web/server/root/example.html'
    		headerHeight = 0
    		footer = 'location/within/web/server/root/example.html'
    		footerHeight = 0
    		jsImports = ['location/within/web/server/root/exampleImport1.js',
                              ' location/within/web/server/root/exampleImport2.js']
    		cssImports = [' location/within/web/server/root/    exampleImport1.css',
                               ' location/within/web/server/root/exampleImport2.css']
    	}
    
    	}

#2   Enabling Custom Banners
To enable a header or footer:

1.	Define the `owf.customHeaderFooter.header` and `owf.customHeaderFooter.footer` properties. 
2.	Specify the location of the banner. It will be a Web resource that results in HTML when included in the primary interface. Possible choices include but are not limited to: HTML files, PHP files, REST calls or any other link that produces HTML.
3.	Specify the exact height in pixels:  For OWF to size the header, footer and dashboard appropriately, `owf.customHeaderFooter.headerHeight` and `owf.customHeaderFooter.footerHeight` require non-zero integer values.
4.	If the custom header or custom footer requires supporting JavaScript or CSS resources, use the `owf.customHeaderFooter.jsImports` and `owf.customHeaderFooter.cssImports` properties to specify their location. Specify locations as a list of values, where each value represents a single resource.
5.	If the custom header or footer must be initialized by a JavaScript call upon rendering, assign the `Ozone.config.customHeaderFooter.onHeaderReady` and `Ozone.config.customHeaderFooter.onFooterReady` callback variables to appropriate functions. The functions should exist in a JavaScript resource that is imported. Assumed the functions will be global. See the example below:

        Ozone.config.customHeaderFooter.onHeaderReady = function () {
    	alert(“Sample header callback”);
        }

        Ozone.config.customHeaderFooter.onFooterReady = function () {
    	alert(“Sample footer callback”);
        }a
