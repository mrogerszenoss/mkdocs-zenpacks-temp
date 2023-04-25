# RaphaelJS

@lb[](img/zenpack-raphaeljs-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Authors:

Daniel Robbins

### Maintainers:

Daniel Robbins

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.RaphaelJS

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.RaphaelJS){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.RaphaelJS.git){.external-link}

## RaphaelJS ZenPack

This ZenPack provides the RaphaelJS SVG/VML JavaScript rendering
framework, which can be used by other ZenPacks.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 2.1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.RaphaelJS/2.1.0/ZenPacks.zenoss.RaphaelJS-2.1.0.egg){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x, Zenoss
    Resource Manager 4.1.x, Zenoss Resource Manager 4.2.x:   Incompatible with Zenoss Core 2.5.x

## Background

The RaphaelJS ZenPack brings VML/SVG ([Scalable Vector Graphics](http://en.wikipedia.org/wiki/Scalable_Vector_Graphics "wikipedia:Scalable Vector Graphics"){.external-link})
rendering and animation capabilities to Zenoss. From the [Raphael Web Site](http://raphaeljs.com){.external-link}:

> Raphaël is a small JavaScript library that should simplify your work
> with vector graphics on the web. If you want to create your own
> specific chart or image crop and rotate widget, for example, you can
> achieve it simply and easily with this library.
>
> Raphaël \['ræfeɪəl\] uses the SVG W3C Recommendation and VML as a base
> for creating graphics. This means every graphical object you create is
> also a DOM object, so you can attach JavaScript event handlers or
> modify them later. Raphaël&rsquo;s goal is to provide an adapter that will
> make drawing vector art compatible cross-browser and easy.
>
> Raphaël currently supports Firefox 3.0+, Safari 3.0+, Chrome 5.0+,
> Opera 9.5+ and Internet Explorer 6.0+.

#### Why RaphaelJS?

The primary benefit of using Raphael over pure SVG is that Microsoft
Internet Explorer started supporting SVG in Internet Explorer 9. If you
want to maintain compatibility with IE8 and earlier, you cannot use SVG.

Raphael allows you to deliver rich vector-based experiences that are
compatible with IE6 and later by providing a JavaScript API that will
target SVG on SVG-compatible browsers such as Firefox, Chrome and
Safari, while using Microsoft's VML to target IE8 and earlier.

## Usage

To use RaphaelJS for rendering in Zenoss, add the following JavaScript
code to your ZenPack:

    Ext.ux.Raphael = Ext.extend(Ext.BoxComponent, {         onRender: function(ct) {             var p = this.paper = Raphael(ct.dom), v;             this.el = Ext.get(p.canvas);           // Export all methods from this paper object which will not override our native     // methods like setSize etc.             for (var prop in p) {                 v = p[prop];
                if (!this[prop] && Ext.isFunction(v)) {                     this[prop] = v.createDelegate(p);
                }
            }

    // We always cache our size
            this.cacheSizes = true;
        },

        getWidth: function() {             return this.lastSize.width;         },

        getHeight: function() {             return this.lastSize.height;         },

        onResize: function(w, h) {             this.paper.setSize(w, h);         }
    });
    Ext.reg('raphael', Ext.ux.Raphael);
    // end of file

This code extends Ext.BoxComponent so that it displays a Raphael VML/SVG
rendering area that is the size of the component.

You will now be able to define new Ext.ux.Raphael components, which
provide Raphael rendering capabilities within Zenoss, via the
component's paper property:

    var r = new Ext.ux.Raphael();
    var myrect = r.paper.rect(0,0,r.getWidth(),r.getHeight()/2).attr({"fill" : "90-#000000:0-#5100ad:99.70238095238095"});

## Resources

-   [RaphaelJS reference](http://raphaeljs.com/reference.html){.external-link}
-   [RaphaelJS polar clock demo](http://raphaeljs.com/polar-clock.html){.external-link}

## Attachments:

-   [raphaeljs-zenpack.png](img/zenpack-raphaeljs-zenpack.png)
-   [raphaeljs-zenpack.png](img/zenpack-raphaeljs-zenpack.png)
-   [raphaeljs-zenpack.png](img/zenpack-raphaeljs-zenpack.png)
-   [raphaeljs-zenpack.png](img/zenpack-raphaeljs-zenpack.png)

