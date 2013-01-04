GRMustache
==========

GRMustache is a flexible and production-ready implementation of [Mustache](http://mustache.github.com/) templates for MacOS Cocoa and iOS.

GRMustache targets MacOS down to 10.6 Snow Leopard, iOS down to version 4.3, and only depends on the Foundation framework.

**November 28, 2012: GRMustache 6.1.3 is out.** [Release notes](GRMustache/blob/master/RELEASE_NOTES.md)

Don't miss a single release: follow [@GRMustache](http://twitter.com/GRMustache) on Twitter.

How To
------

### 1. Setup your Xcode project

**Option 1: CocoaPods**

Dear [CocoaPods](https://github.com/CocoaPods/CocoaPods) users, append `pod 'GRMustache', '~> 6.1'` to your Podfile.

**Option 2: Static Library**

The distribution includes pre-built static libraries:

Clone the repository with the `git clone https://github.com/groue/GRMustache.git` command.

- For MacOS development, add `include/GRMustache.h` and `lib/libGRMustache6-MacOS.a` to your project.
- For iOS development, add `include/GRMustache.h` and `lib/libGRMustache6-iOS.a` to your project.

If you have GRMustache files *copied* in your project, you'll need to copy all header files of the `include` directory, not only `GRMustache.h`.

**Option 3: Compiling the raw sources**

You may also embed the raw GRMustache sources in your project:

    $ git clone https://github.com/groue/GRMustache.git
    $ cd GRMustache
    $ git submodule update --init src/vendor/groue/jrswizzle

Add all files of `src/classes` plus `src/vendor/groue/jrswizzle/JRSwizzle.*` to your project. In your own sources, avoid importing header files whose name ends with `_private.h`: those are private headers that may change, without notice, in future releases.

**armv6 architecture**: The last GRMustache static library that embeds the armv6 slice is [GRMustache 5.0.1](https://github.com/groue/GRMustache/tree/v5.0.1). You now have to compile GRMustache yourself, or to use [CocoaPods](https://github.com/CocoaPods/CocoaPods).

### 2. Start rendering templates

```objc
#import "GRMustache.h"

// Renders "Hello Arthur!"
NSString *rendering = [GRMustacheTemplate renderObject:[Person personWithName:@"Arthur"]
                                            fromString:@"Hello {{name}}!"
                                                 error:NULL];

// Renders a document from the `Profile.mustache` resource
NSString *rendering = [GRMustacheTemplate renderObject:[Person personWithName:@"Arthur"]
                                          fromResource:@"Profile"
                                                bundle:nil
                                                 error:NULL];
```


Documentation
-------------

### Mustache syntax

- http://mustache.github.com/mustache.5.html

### Guides

Introduction:

- [Introduction](GRMustache/blob/master/Guides/introduction.md): a tour of the library features, and most common use cases.

Loading templates:

- [Templates](GRMustache/blob/master/Guides/templates.md): how to load templates from common sources.
- [Partials](GRMustache/blob/master/Guides/partials.md): how to embed templates in other templates.
- [Templates Repositories](GRMustache/blob/master/Guides/template_repositories.md): load templates from less common sources.

Rendering templates:

- [Runtime](GRMustache/blob/master/Guides/runtime.md): how to provide data to templates

Advanced Mustache:

- [Filters](GRMustache/blob/master/Guides/filters.md): how to process data before it is rendered with "filters".
- [Tag Delegates](GRMustache/blob/master/Guides/delegate.md): how to observe and alter template rendering.
- [Rendering Objects](GRMustache/blob/master/Guides/rendering_objects.md): how to provide your custom rendering code.
- [Protected Contexts](GRMustache/blob/master/Guides/protected_contexts.md): how to have some keys always evaluate to the same value.

### Sample code

- [Number Formatting](GRMustache/blob/master/Guides/sample_code/number_formatting.md): how to format numbers
- [Collection Indexes](GRMustache/blob/master/Guides/sample_code/indexes.md): how to render array indexes, render sections for the first or the last element, for odd or even elements, etc.
- [Localization](GRMustache/blob/master/Guides/sample_code/localization.md): how to localize portions of your templates

### Reference

- [Reference](http://groue.github.com/GRMustache/Reference/): the GRMustache reference, automatically generated from inline documentation, for fun and profit, by [appledoc](http://gentlebytes.com/appledoc/).

### Internals

- [Forking](GRMustache/blob/master/Guides/forking.md): the forking guide tells you everything about GRMustache organization.

FAQ
---

- **Q: How do I render array indexes?**
    
    A: Check the [Collection Indexes Sample Code](GRMustache/blob/master/Guides/sample_code/indexes.md)

- **Q: How do I format numbers and dates?**
    
    A: Check the [Number Formatting Sample Code](GRMustache/blob/master/Guides/sample_code/number_formatting.md)

- **Q: How do I render partial templates whose name is only known at runtime?**

    A: Check the [Rendering Objects Guide](GRMustache/blob/master/Guides/rendering_objects.md)

- **Q: Does GRMustache provide any layout or template inheritance facility?**
    
    A: Check the [Partials Guide](GRMustache/blob/master/Guides/partials.md).

- **Q: How do I localize templates?**

    A: Check the [Localization Sample Code](GRMustache/blob/master/Guides/sample_code/localization.md)

- **Q: How do I render default values for missing keys?**

    A: Check the [Tag Delegate Guide](GRMustache/blob/master/Guides/delegate.md).

- **Q: What is this NSUndefinedKeyException stuff?**

    A: When GRMustache has to try several objects until it finds the one that provides a `{{key}}`, several NSUndefinedKeyException are raised and caught. Let us double guess you: it's likely that you wish Xcode would stop breaking on those exceptions. This use case is covered in the [Runtime Guide](GRMustache/blob/master/Guides/runtime.md).

- **Q: Why does GRMustache need JRSwizzle?**

    A: GRMustache does not need it. However, *you* may happy having GRMustache [swizzle](http://www.mikeash.com/pyblog/friday-qa-2010-01-29-method-replacement-for-fun-and-profit.html) `valueForUndefinedKey:` in the NSObject and NSManagedObject classes when you invoke `[GRMustache preventNSUndefinedKeyExceptionAttack]`. The use case is described in the [Runtime Guide](GRMustache/blob/master/Guides/runtime.md).

What other people say
---------------------

[@JeffSchilling](https://twitter.com/jeffschilling/status/142374437776408577):

> I'm loving grmustache

[@basilshkara](https://twitter.com/basilshkara/status/218569924296187904):

> Oh man GRMustache saved my ass once again. Awesome lib.

[@guiheneuf](https://twitter.com/guiheneuf/status/249061029978460160):

> GRMustache filters extension saved us from great escaping PITAs. Thanks @groue.

[@orj](https://twitter.com/orj/status/195310301820878848):

> Thank fucking christ for decent iOS developers who ship .lib files in their Github repos. #GRMustache


Popular projects & apps using GRMustache
----------------------------------------

* [tomaz/appledoc](https://github.com/tomaz/appledoc): Objective-c code Apple style documentation set generator
* [mapbox/mapbox-ios-sdk](https://github.com/mapbox/mapbox-ios-sdk): MapBox iOS SDK, an open source alternative to MapKit
* [CarterA/Tribo](https://github.com/CarterA/Tribo): Extremely fast static site generator written in Objective-C
* [AutoLib](http://itunes.com/apps/autolib) uses GRMustache and [spullara/mustache.java](https://github.com/spullara/mustache.java) for rendering an identical set of Mustache templates on iOS and Android.
* [CinéObs](http://itunes.com/apps/cineobs) uses GRMustache for RSS feeds rendering
* [Fotopedia](http://itunes.com/apps/fotonautsinc)
* [FunGolf GPS](http://itunes.com/apps/fungolf)


Contribution wish-list
----------------------

Please look for an [open issue](GRMustache/issues) that smiles at you!

... And I wish somebody would review the non-native English of the documentation and guides.


Forking
-------

Please fork. You'll learn useful information in the [Forking Guide](GRMustache/blob/master/Guides/forking.md).


License
-------

Released under the [MIT License](GRMustache/blob/master/LICENSE).
