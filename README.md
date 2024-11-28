# Performance Optimization Techniques for BabylonJS
First off performance depends on a users machine, therefore it is expected that for a given heavy duty application that requires performance there should be a bare minimun of system resources in terms of Memory, CPU and sometimes GPU. For instance trying to render a 4gb 3d model in a < 4gb machine will most likely not work except if we are to build our custom 3d engine and renderer.

That said below are some optimizations I think we can employ:
- **Use models with fewer faces**:
    calling this `sphere.getTotalIndices() / 3` gives us 4624 faces while the same method on a `box` model gives 12 faces. Therefore using boxes in place of spheres saves us from rendering x385 times the number of faces.
    You can test this here https://iyusuf40.github.io/babylon/
    Try to change the numbers based on hardware capabilities and change the shapes, you'd notice boxes perform way faster than spheres, at 100 rows by 100 columns i could still render boxes while my spheres crashed my browser.

- **Adapt the frame rate to what the machine is capable of handling:**
    My humble research could not find where / how to modify the frame rate of the rendring, It is hardcoded to 60fps ie every 16ms, you can find that here https://github.com/BabylonJS/Babylon.js/blob/3725abaed67d26b5a8de053f3aa336deae4373b1/packages/dev/core/src/Engines/abstractEngine.ts#L75
    so I came up with a code that adapts the rendering rate to what the rendering machine can handle. click on the `adaptive fps` button in https://iyusuf40.github.io/babylon/ to enable that.
    with this update, ones system is less likely to be unresponsive due to rendering. below is the code.