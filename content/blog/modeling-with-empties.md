---
title: "Sapiens Modding with Empties"
date: 2025-03-26
description: An explanation of the empty-based workflow for Sapiens, and my workflow for it.
draft: false
tags:
 - "modding"
 - "blender"
---

![alt text](/images/modeling-with-empties/cover-image.png)

[Sapiens](https://store.steampowered.com/app/1060230/Sapiens/) is a prehistoric village simulation game, created by [Majic Jungle](https://majicjungle.com/). As Sapiens is largely a solo endeavor, it has a number of charming quirks, both in game design, and also in tooling/development practices. In this article I will explain how the sausage is made, and how I built mod tools that in many ways surpass the developers own internal tooling.

The workflow I will share, while specific to Sapiens, is interesting enough that it might be worth applying in other gamedev related scenarios. Use your best judgement!

## Modding

To cut a long story short, the modding scene in Sapiens is great. The developer is very supportive, and included a built in [lua scripting interface for Sapiens](https://wiki.sapiens.dev/guide/shadowing.html). I have a number of popular mods on the workshop, including the [Hammerstone Modding Framework](https://steamcommunity.com/sharedfiles/filedetails/?id=2840825226), [Furniture](https://steamcommunity.com/sharedfiles/filedetails/?id=2966227716), [Vanilla Tweaks](https://steamcommunity.com/sharedfiles/filedetails/?id=2841763465) and a bunch more.

## Models in Sapiens

As you can imagine, one of the common requirements in these mods is the ability to add new "stuff" (especially buildings). To do this, we need to interact with Sapiens very *unique* model format. Here is some stairs, when opened directly in Sapiens:

![alt text](/images/modeling-with-empties/empties.png)

Each cross here is a different sapiens game object (e.g., a `SplitLog`), with the empty dimensions representing roughly the size of the model that will be used in game. During game-time, the sapiens will attach various compatible resources into these slots (e.g., `BambooSplitLog`, or `BirchSplitLog`) in order to construct the building. This is a very neat system as it allows every in-game building to be constructed very naturally, with a diverse set of resources, all of them reflected in the visuals of the final product. 

The developer experience for it is *bad* though.

## Cleaning up the Model

If we manually apply size of 1 to all empties (for some reason GLTF format doesn't store this information, so blender randomizes the size on import), and change the preview to something relevant, the model starts to take shape. Hopefully you can see the stairs now.

![alt text](/images/modeling-with-empties/clean-empties.png)

This is much easier to understand, but it's still difficult to work with. Sapiens has literally hundreds of primitive models that could be used inside of the composite building pieces, and it's very hard to visualize how they will appear in-game from this view. For example how would it look if we used Logs instead of Split Logs? Or perhaps Planks?

## Scripting Part 1: Importing Model Libraries

As a modder (and perhaps as a developer 😉), my desired workflow is to build a model in blender, representing the in-game object, and then *export as empties*. The first step in achieving that is importing all of Sapiens primitive models into some form of library, so I can kitbash new buildings. Thankfully blender has a built in [asset browser](https://docs.blender.org/manual/en/latest/editors/asset_browser.html), so all I need to do is create some a `.blend` file containing all of Sapiens models, marked as assets.

This is pretty achievable with Blenders [Python API](https://docs.blender.org/api/current/index.html).

Paired down, the code looks something like this:

```python
root = Path("C:\Program Files (x86)\Steam\steamapps\common\Sapiens\GameResources\models")

def main():
    for f in root.glob('**/*'):
        import_glb(f)
    
def delete_empties():
    for object in C.scene.objects:
        if object.type != "MESH":
            bpy.data.objects.remove(object, do_unlink=True)
            
    
def import_glb(import_path):
    path = str(import_path)
    bpy.ops.import_scene.gltf(filepath=path)
    delete_empties()
    
    new_object = C.scene.object
    
    if new_object:
        stem = import_path.stem
        
        new_object.name = stem
        new_object.asset_mark()
        new_object.asset_generate_preview()
        new_object.asset_data.author = "Majic Dave"
    
main()
```

The idea is to iterate over the games installation folder, import and extract all models, and mark them as assets. Of course the script I'm using in production has to handle a few more cases (such as not importing duplicate models), but the entire script is just 70 lines of easy Python.

The results are pretty fun too: It stacks all the items on top of each other in quite a glorious mess.

![alt text](/images/modeling-with-empties/import-mess.png)

## Creating Buildings with Imported Assets

Once I've marked the resultant `library.blend` file as an asset source in blender, I have access to all of the many hundreds of primitive models directly in blender. I can simply drag+drop them into place to build complex composite models in-situ, with 1:1 preview.

![alt text](/images/modeling-with-empties/asset-browser.png)


## Exporting the Composite Models

The last step of the process is to export these composite models into a format the Sapiens understands. That's as simple as converting all the models into empties, applying transforms, and exporting. For various reasons, I chose to make this code operate on a "collection" of assets, that would create a sibling collection with empties, which I could then manually export:

```python
def add_empty(object_ref):
    new_empty = bpy.data.objects.new('Empty', None)
    
    new_empty.name = object_ref.name
    new_empty.location = object_ref.location
    new_empty.rotation_mode = object_ref.rotation_mode
    new_empty.rotation_quaternion = object_ref.rotation_quaternion
    
    return new_empty

def main():
    current_collection = bpy.context.collection
    print("Current Collection: ", current_collection)
    
    export_collection = bpy.data.collections.new("ExportCollection")
    bpy.context.scene.collection.children.link(export_collection)
        
    objects = current_collection.all_objects
    
    for object in objects:
        empty = add_empty(object)
        export_collection.objects.link(empty)

main()
```


I used this technique, along with my own custom primitives (which I imported as a library, of course) to create all kinds of fun content for the game, such as:

![alt text](/images/modeling-with-empties/bone-stuff.png)

![alt text](/images/modeling-with-empties/chairs.png)

## Closing Thoughts

For me, the most interesting part of building these tools is that the *game author did not*. From our conversations, he seems entirely happy hand-editing the empties in Blender, and simply visualizing the result in this head until he has a chance to test in game. This isn't a knock against the developer either! It's a strange and wondrous thing to be so deep into a project that your workflow looks totally insane to any onlookers, but doesn't bug you one bit.

I'm pretty much done with Sapiens modding, but I wanted to share this fun little workflow before I forget. Happy coding!